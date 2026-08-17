# 🏷️ Enum: ApplicationStatus

> [!abstract] Phân loại
> **Loại:** `Enum` — Trạng thái đơn ứng tuyển.
> **Package:** `com.example.groupproject.entity.enums`

---

## 📋 Các giá trị theo Flow

```
APPLIED → SCREENING → INTERVIEW → OFFER → HIRED
                     ↓            ↓
                  REJECTED      WITHDRAWN
```

| Value | Mô tả |
|-------|--------|
| `APPLIED` | Vừa nộp đơn, chưa xử lý. Giá trị mặc định. |
| `SCREENING` | Đang xem xét hồ sơ ban đầu. |
| `INTERVIEW` | Được mời phỏng vấn. |
| `OFFER` | Được chắp nhận, đang chờ ký hợp đồng. |
| `HIRED` | Đã tuyển dụng thành công. |
| `REJECTED` | Bị từ chối. |
| `WITHDRAWN` | Ứng viên rút đơn. |
