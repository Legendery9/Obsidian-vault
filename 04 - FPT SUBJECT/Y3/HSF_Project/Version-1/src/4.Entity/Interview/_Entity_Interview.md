# 🏛️ Entity: Interview

> [!abstract] Định nghĩa
> **Loại:** `Entity Class` — Ánh xạ đến bảng `interviews` trong database.
> **Package:** `com.example.groupproject.entity`
> **Annotation:** `@Entity @Table(name = "interviews")`

---

## 🗄️ Ánh xạ Database

```sql
-- Bảng: interviews
CREATE TABLE interviews (
    id                INT AUTO_INCREMENT PRIMARY KEY,
    application_id    INT         NOT NULL REFERENCES applications(id),
    interviewer_id    INT         NOT NULL REFERENCES users(id),
    interview_date    DATE        NOT NULL,
    interview_time    TIME        NOT NULL,
    location_or_link  VARCHAR(500),
    status            ENUM('SCHEDULED','COMPLETED','CANCELLED','NO_SHOW') NOT NULL DEFAULT 'SCHEDULED',
    rating            SMALLINT,
    feedback          TEXT,
    evaluated_at      TIMESTAMP,
    assigned_by       INT         NOT NULL REFERENCES users(id),
    created_at        TIMESTAMP   NOT NULL,
    updated_at        TIMESTAMP   NOT NULL
);
```

---

## 📋 Thuộc tính (Fields)

| Field Java | Column DB | Kiểu | Ràng buộc | Mô tả |
|-----------|-----------|------|-----------|-------|
| `id` | `id` | `Integer` | PK, Auto Increment | Khóa chính |
| `application` | `application_id` | `Application` (FK) | NOT NULL, LAZY | Đơn ứng tuyển liên quan |
| `interviewer` | `interviewer_id` | `User` (FK) | NOT NULL, LAZY | Người phỏng vấn |
| `interviewDate` | `interview_date` | `LocalDate` | NOT NULL | Ngày phỏng vấn |
| `interviewTime` | `interview_time` | `LocalTime` | NOT NULL | Giờ phỏng vấn |
| `locationOrLink` | `location_or_link` | `String` | nullable, max 500 | Địa điểm hoặc link online |
| `status` | `status` | `InterviewStatus` (enum) | NOT NULL, default SCHEDULED | Trạng thái phỏng vấn |
| `rating` | `rating` | `Short` | nullable | Điểm đánh giá ứng viên |
| `feedback` | `feedback` | `String` | nullable, TEXT | Phản hồi sau phỏng vấn |
| `evaluatedAt` | `evaluated_at` | `Instant` | nullable | Thời điểm hoàn thành đánh giá |
| `assignedBy` | `assigned_by` | `User` (FK) | NOT NULL, LAZY | Người phân công phỏng vấn |
| `createdAt` | `created_at` | `Instant` | NOT NULL, not updatable | Thời điểm tạo |
| `updatedAt` | `updated_at` | `Instant` | NOT NULL | Thời điểm cập nhật cuối |

---

## 🔗 Được sử dụng trong dự án

- **`InterviewRepository`** — đếm interview sắp diễn ra trong 7 ngày tới (dashboard stats)
- **`DashboardService`** — cung cấp số liệu `upcomingInterviewCount`
