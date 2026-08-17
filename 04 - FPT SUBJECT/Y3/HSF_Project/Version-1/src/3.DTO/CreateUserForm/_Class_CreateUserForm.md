# 📝 Class: CreateUserForm (DTO)

> [!abstract] Phân loại
> **Loại:** `DTO / Form Class` — Data Transfer Object dùng để nhận dữ liệu từ form HTML tạo user mới.
> **Package:** `com.example.groupproject.dto`

---

## 📋 Fields & Validation Constraints

| Field | Kiểu | Constraints | Mô tả |
|-------|------|------------|-------|
| `fullName` | `String` | `@NotBlank`, `@Size(max=255)` | Họ tên đầy đủ |
| `username` | `String` | `@NotBlank`, `@Size(min=4,max=50)`, `@Pattern(^[A-Za-z0-9_]{4,50}$)` | Tên đăng nhập |
| `email` | `String` | `@NotBlank`, `@Email` | Email hợp lệ |
| `password` | `String` | `@NotBlank`, `@Size(min=8)`, `@Pattern(có uppercase + digit)` | Mật khẩu |
| `role` | `String` | `@NotBlank` | Tên role (HR_MANAGER/INTERVIEWER) |

---

## 🔄 Method: `getUserRole()`

```java
public UserRole getUserRole() {
    return UserRole.valueOf(role);
}
```

Chuyển `role` (String) sang `UserRole` enum. Dùng trong `UserManagementService.createUser()`.

---

## 🔗 Được sử dụng trong
- **`UserManagementController`** — `@ModelAttribute("createUserForm")` binding từ form POST
- **`UserManagementService`** — `createUser(form, actor)` đọc dữ liệu từ form
