# 🏛️ Entity: User

> [!abstract] Định nghĩa
> **Loại:** `Entity Class` — Ánh xạ trực tiếp đến bảng `users` trong database.
> **Package:** `com.example.groupproject.entity`
> **Annotation:** `@Entity @Table(name = "users")`

---

## 🗄️ Ánh xạ Database

```sql
-- Bảng: users
CREATE TABLE users (
    id               INT AUTO_INCREMENT PRIMARY KEY,
    full_name        VARCHAR(255) NOT NULL,
    username         VARCHAR(50)  NOT NULL UNIQUE,
    email            VARCHAR(255) NOT NULL UNIQUE,
    password         VARCHAR(255) NOT NULL,
    role             ENUM('ADMIN','HR_MANAGER','INTERVIEWER','CANDIDATE') NOT NULL,
    status           ENUM('ACTIVE','INACTIVE','LOCKED') NOT NULL DEFAULT 'ACTIVE',
    failed_login_count SMALLINT   NOT NULL DEFAULT 0,
    locked_at        TIMESTAMP,
    created_at       TIMESTAMP    NOT NULL,
    updated_at       TIMESTAMP    NOT NULL
);
```

---

## 📋 Thuộc tính (Fields)

| Field Java | Column DB | Kiểu | Ràng buộc | Mô tả |
|-----------|-----------|------|-----------|-------|
| `id` | `id` | `Integer` | PK, Auto Increment | Khóa chính tự tăng |
| `fullName` | `full_name` | `String` | NOT NULL | Họ và tên đầy đủ |
| `username` | `username` | `String` | NOT NULL, UNIQUE, max 50 | Tên đăng nhập, duy nhất |
| `email` | `email` | `String` | NOT NULL, UNIQUE | Email, duy nhất |
| `password` | `password` | `String` | NOT NULL | Mật khẩu (lưu plain-text) |
| `role` | `role` | `UserRole` (enum) | NOT NULL, max 20 | Vai trò: ADMIN/HR_MANAGER/INTERVIEWER/CANDIDATE |
| `status` | `status` | `UserStatus` (enum) | NOT NULL, default ACTIVE | Trạng thái tài khoản |
| `failedLoginCount` | `failed_login_count` | `Short` | NOT NULL, default 0 | Số lần đăng nhập thất bại |
| `lockedAt` | `locked_at` | `Instant` | nullable | Thời điểm tài khoản bị khóa |
| `createdAt` | `created_at` | `Instant` | NOT NULL, not updatable | Thời điểm tạo tài khoản |
| `updatedAt` | `updated_at` | `Instant` | NOT NULL | Thời điểm cập nhật cuối |

---

## ⚡ JPA Lifecycle Callbacks

```java
@PrePersist
protected void onCreate() {
    Instant now = Instant.now();
    this.createdAt = now;
    this.updatedAt = now;
}

@PreUpdate
protected void onUpdate() {
    this.updatedAt = Instant.now();
}
```

> [!note] Tự động gán timestamp
> `@PrePersist` gọi trước khi INSERT — tự set `createdAt` và `updatedAt`.
> `@PreUpdate` gọi trước khi UPDATE — tự cập nhật `updatedAt`.

---

## 🔗 Được sử dụng trong dự án

- **`AuthService`** — load User khi đăng nhập, kiểm tra status, lưu userId vào session
- **`UserManagementService`** — tạo, unlock, deactivate tài khoản
- **`UserRepository`** — truy vấn theo username, email, role, status
- **`JobPosting`** — FK `created_by` → User (người tạo job)
- **`Application`** — FK `candidate_id` → User (ứng viên)
- **`Interview`** — FK `interviewer_id`, `assigned_by` → User
- **`ActivityLog`** — FK `actor_id` → User (người thực hiện hành động)
- **`PasswordResetToken`** — FK `user_id` → User
- **`GlobalModelAdvice`** — inject `currentUser` vào tất cả Model
- **`DataInitializer`** — tạo tài khoản admin mặc định khi start
