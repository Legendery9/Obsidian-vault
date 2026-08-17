# 3️⃣ UserManagementController — `/admin/users/**`

> [!abstract]
> Controller quản lý tài khoản người dùng trong hệ thống, **chỉ ADMIN** mới được phép truy cập toàn bộ. Cung cấp khả năng tìm kiếm, tạo, khóa và vô hiệu hóa tài khoản HR/Interviewer.

---

## 📌 Endpoints

### `GET /admin/users` — Danh sách & Tìm kiếm

```
Request → UserManagementController.listUsers()
    │
    ├── @RequestParam search   (nullable) — Tìm theo username hoặc email
    ├── @RequestParam role     (nullable) — Filter theo UserRole enum
    └── @RequestParam status   (nullable) — Filter theo UserStatus enum
    ↓
AuthService.requireRole(user, ADMIN)
    ↓
UserManagementService.searchUsers(search, role, status)
    └── Trả về List<User> đã filter
    ↓
addActionFlags(model, users)
    ├── canUnlock map    — userId → boolean (user có đang LOCKED không?)
    └── canDeactivate map — userId → boolean (user có đang ACTIVE không?)
    ↓
model.addAttribute:
    ├── "users"          — Danh sách user đã filter
    ├── "search"         — Giá trị tìm kiếm
    ├── "selectedRole"   — Role đang filter
    ├── "selectedStatus" — Status đang filter
    ├── "roles"          — UserRole.values() (dropdown)
    ├── "statuses"       — UserStatus.values() (dropdown)
    ├── "createUserForm" — Form object rỗng để tạo user
    ├── "creatableRoles" — [HR_MANAGER, INTERVIEWER] (không tạo được ADMIN/CANDIDATE)
    ├── "canUnlock"      — Map<Integer, Boolean>
    └── "canDeactivate"  — Map<Integer, Boolean>
    ↓
return "admin/users"
```

---

### `POST /admin/users` — Tạo tài khoản mới

```
Request → UserManagementController.createUser()
    │
    └── @Valid @ModelAttribute CreateUserForm form
    ↓
AuthService.requireRole(user, ADMIN)
    ↓
bindingResult.hasErrors()?
    └── true → populateListModel() + return "admin/users"  ← Hiển thị lỗi validation
    ↓
User actor = AuthService.getCurrentUser(session)
    ↓
UserManagementService.createUser(form, actor)
    └── Tạo user với role HR_MANAGER hoặc INTERVIEWER
        (throw IllegalArgumentException nếu role không hợp lệ)
    ↓
Thành công:
    └── redirectAttributes.addFlashAttribute("successMessage", "User created successfully")
        → redirect:/admin/users
Thất bại (IllegalArgumentException):
    └── bindingResult.reject(...) + populateListModel() + return "admin/users"
```

> [!warning]
> Chỉ có thể tạo tài khoản với role `HR_MANAGER` hoặc `INTERVIEWER`. Tài khoản `ADMIN` chỉ được tạo qua `DataInitializer` khi khởi động. Tài khoản `CANDIDATE` chỉ tạo qua `/register`.

---

### `POST /admin/users/{id}/unlock` — Mở khóa tài khoản

```
Request → UserManagementController.unlock()
    │
    └── @PathVariable id   — User ID cần unlock
    ↓
AuthService.requireRole(user, ADMIN)
    ↓
UserManagementService.unlockUser(id, actor)
    ├── Đổi status: LOCKED → ACTIVE
    ├── Reset failedLoginCount = 0
    └── Ghi ActivityLog: "Unlocked account [username]"
    ↓
Thành công → Flash "Account unlocked" → redirect:/admin/users
Thất bại   → Flash errorMessage     → redirect:/admin/users
```

---

### `POST /admin/users/{id}/deactivate` — Vô hiệu hóa tài khoản

```
Request → UserManagementController.deactivate()
    │
    └── @PathVariable id   — User ID cần deactivate
    ↓
AuthService.requireRole(user, ADMIN)
    ↓
UserManagementService.deactivateUser(id, actor)
    ├── Đổi status: ACTIVE → INACTIVE
    └── Ghi ActivityLog: "Deactivated account [username]"
    ↓
Thành công → Flash "Account deactivated" → redirect:/admin/users
Thất bại   → Flash errorMessage         → redirect:/admin/users
```

---

## 🔧 Private Helpers

### `addActionFlags(model, users)`
> [!info]
> Tính toán flag cho từng user để template biết nên hiển thị nút nào:
> - **canUnlock** — `true` nếu user đang `LOCKED` (hiện nút "Unlock")
> - **canDeactivate** — `true` nếu user đang `ACTIVE` (hiện nút "Deactivate")

### `populateListModel(model, search, role, status)`
> [!info]
> Helper tái sử dụng khi cần re-render danh sách (sau lỗi validation POST).

---

## ⚙️ Dependencies

| Dependency | Mục đích |
|---|---|
| `AuthService` | Validate quyền ADMIN, lấy actor |
| `UserManagementService` | CRUD operations + action flags |

---

## 📝 Key Responsibilities

- **User listing** với tìm kiếm và filter đa chiều (username/email + role + status)
- **User creation** — tạo tài khoản HR_MANAGER và INTERVIEWER
- **Account unlock** — mở khóa tài khoản bị block do sai password
- **Account deactivation** — vô hiệu hóa tài khoản tạm thời
- **Activity logging** — ghi log toàn bộ hành động admin
- **Action permission per user state** — nút hành động thay đổi theo trạng thái user