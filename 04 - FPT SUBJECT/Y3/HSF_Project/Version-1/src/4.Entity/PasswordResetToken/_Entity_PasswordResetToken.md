# 🏛️ Entity: PasswordResetToken

> [!abstract] Định nghĩa
> **Loại:** `Entity Class` — Ánh xạ đến bảng `password_reset_tokens` trong database.
> **Package:** `com.example.groupproject.entity`
> **Annotation:** `@Entity @Table(name = "password_reset_tokens")`

---

## 🗄️ Ánh xạ Database

```sql
-- Bảng: password_reset_tokens
CREATE TABLE password_reset_tokens (
    id         INT AUTO_INCREMENT PRIMARY KEY,
    user_id    INT       NOT NULL REFERENCES users(id),
    token      VARCHAR(255) NOT NULL UNIQUE,
    expires_at TIMESTAMP NOT NULL,
    used_at    TIMESTAMP,
    created_at TIMESTAMP NOT NULL
);
```

---

## 📋 Thuộc tính (Fields)

| Field Java | Column DB | Kiểu | Ràng buộc | Mô tả |
|-----------|-----------|------|-----------|-------|
| `id` | `id` | `Integer` | PK, Auto Increment | Khóa chính |
| `user` | `user_id` | `User` (FK) | NOT NULL, LAZY | User cần reset mật khẩu |
| `token` | `token` | `String` | NOT NULL, UNIQUE | Token bí mật (random string) dùng để xác thực |
| `expiresAt` | `expires_at` | `Instant` | NOT NULL | Thời điểm token hết hạn |
| `usedAt` | `used_at` | `Instant` | nullable | Thời điểm token đã được dùng (null = chưa dùng) |
| `createdAt` | `created_at` | `Instant` | NOT NULL, not updatable | Thời điểm tạo token |

---

## 🔗 Được sử dụng trong dự án

> [!note] Trạng thái hiện tại
> Entity này đã được định nghĩa và schema DB đã có bảng tương ứng. Tuy nhiên chức năng **Reset Password** chưa được implement trong Sprint hiện tại (được ghi chú là "coming in next sprint" trong template `change-password.html`). Entity đang chờ sẵn để phát triển.
