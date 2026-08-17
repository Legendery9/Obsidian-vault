# 🏛️ Entity: ActivityLog

> [!abstract] Định nghĩa
> **Loại:** `Entity Class` — Ánh xạ đến bảng `activity_log` trong database.
> **Package:** `com.example.groupproject.entity`
> **Annotation:** `@Entity @Table(name = "activity_log")`

---

## 🗄️ Ánh xạ Database

```sql
-- Bảng: activity_log
CREATE TABLE activity_log (
    id             BIGINT AUTO_INCREMENT PRIMARY KEY,
    actor_id       INT        REFERENCES users(id),  -- nullable (anonymous)
    actor_username VARCHAR(50) NOT NULL,
    event_type     ENUM('SIGN_IN_SUCCESS','SIGN_IN_FAILURE','ACCOUNT_CREATED','ACCOUNT_DEACTIVATED',
                        'ACCOUNT_UNLOCKED','ACCOUNT_LOCKED','APPLICATION_STATUS_CHANGED',
                        'CV_DOWNLOADED','EVALUATION_SUBMITTED') NOT NULL,
    description    TEXT,
    ip_address     VARCHAR(45),
    created_at     TIMESTAMP   NOT NULL
);
```

---

## 📋 Thuộc tính (Fields)

| Field Java | Column DB | Kiểu | Ràng buộc | Mô tả |
|-----------|-----------|------|-----------|-------|
| `id` | `id` | `Long` | PK, Auto Increment | Khóa chính (Long vì log có thể rất nhiều) |
| `actor` | `actor_id` | `User` (FK) | nullable, LAZY | Người thực hiện hành động (null nếu anonymous) |
| `actorUsername` | `actor_username` | `String` | NOT NULL, max 50 | Username lưu dự phòng (tránh mất log khi xóa user) |
| `eventType` | `event_type` | `ActivityEventType` (enum) | NOT NULL, max 50 | Loại sự kiện |
| `description` | `description` | `String` | nullable, TEXT | Mô tả chi tiết sự kiện |
| `ipAddress` | `ip_address` | `String` | nullable, max 45 | IP của người thực hiện |
| `createdAt` | `created_at` | `Instant` | NOT NULL, not updatable | Thời điểm ghi log |

---

## 🔗 Được sử dụng trong dự án

- **`ActivityLogRepository`** — ghi log (WRITE only). Read dùng VIEW thay thế.
- **`ActivityLogDisplayView`** — VIEW `v_activity_log_display` dùng để đọc log với thông tin bổ sung
- **`UserManagementService`** — tự động ghi log sau mỗi thao tác quản lý tài khoản
