# 🏷️ Enum: UserStatus

> [!abstract] Phân loại
> **Loại:** `Enum` — Trạng thái tài khoản người dùng.
> **Package:** `com.example.groupproject.entity.enums`

---

## 📋 Các giá trị

| Value | Mô tả | Chuyển trạng thái |
|-------|--------|-------------------|
| `ACTIVE` | Tài khoản đang hoạt động | ← từ LOCKED (unlock) |
| `INACTIVE` | Tài khoản bị vô hiệu hóa | ← từ ACTIVE/LOCKED (deactivate) |
| `LOCKED` | Tài khoản bị khóa do đăng nhập sai nhiều lần | → ACTIVE (admin unlock) |

> [!note] Lưu trữ
> Lưu dưới dạng String trong DB (`status` column). Giá trị mặc định khi tạo user: `ACTIVE`.
