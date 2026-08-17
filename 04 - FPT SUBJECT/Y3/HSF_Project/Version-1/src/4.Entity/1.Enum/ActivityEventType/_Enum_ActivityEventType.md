# 🏷️ Enum: ActivityEventType

> [!abstract] Phân loại
> **Loại:** `Enum` — Các loại sự kiện được ghi vào `activity_log`.
> **Package:** `com.example.groupproject.entity.enums`

---

## 📋 Các giá trị

| Value | Khi nào được ghi |
|-------|------------------|
| `SIGN_IN_SUCCESS` | Đăng nhập thành công |
| `SIGN_IN_FAILURE` | Đăng nhập thất bại |
| `ACCOUNT_CREATED` | Admin tạo tài khoản mới |
| `ACCOUNT_DEACTIVATED` | Admin vô hiệu hóa tài khoản |
| `ACCOUNT_UNLOCKED` | Admin mở khóa tài khoản |
| `ACCOUNT_LOCKED` | Hệ thống khóa tài khoản (sắp implement) |
| `APPLICATION_STATUS_CHANGED` | Thay đổi trạng thái đơn ứng tuyển |
| `CV_DOWNLOADED` | Tải CV ứng viên |
| `EVALUATION_SUBMITTED` | Nộp kết quả phỏng vấn |

> [!note] CHECK Constraint trong DB
> `event_type IN ('SIGN_IN_SUCCESS','SIGN_IN_FAILURE','ACCOUNT_CREATED','ACCOUNT_DEACTIVATED','ACCOUNT_UNLOCKED','ACCOUNT_LOCKED','APPLICATION_STATUS_CHANGED','CV_DOWNLOADED','EVALUATION_SUBMITTED')`
