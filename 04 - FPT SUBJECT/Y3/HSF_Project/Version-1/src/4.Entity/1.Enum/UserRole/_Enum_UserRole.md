# 🏷️ Enum: UserRole

> [!abstract] Phân loại
> **Loại:** `Enum` — Định nghĩa các vai trò trong hệ thống TalentHub.
> **Package:** `com.example.groupproject.entity.enums`

---

## 📋 Các giá trị

| Value | Mô tả | Quyền truy cập |
|-------|--------|---------------|
| `ADMIN` | Quản trị viên hệ thống | Tất cả mọi trang (`/**`) |
| `HR_MANAGER` | Nhân viên tuyển dụng | `/profile`, `/hr/**`, `/jobs/**` |
| `INTERVIEWER` | Người phỏng vấn | `/profile` (giới hạn) |
| `CANDIDATE` | Ứng viên | `/profile` (giới hạn) |

> [!note] CHECK Constraint trong DB
> `role IN ('ADMIN','HR_MANAGER','INTERVIEWER','CANDIDATE')` — Enum được lưu dưới dạng String trong DB.

---

## 🔗 Sử dụng trong dự án

- `User.role` — field trong User entity
- `AuthInterceptor` — kiểm tra role để phân quyền URL
- `AuthService` — `requireRole()`, `hasRole()`, `hasAnyRole()`
- `GlobalModelAdvice` — tạo các flag `isAdmin`, `canAccessHr`
- `DashboardService` — lọc data theo role
- `UserManagementService` — `CREATABLE_ROLES = {HR_MANAGER, INTERVIEWER}`
