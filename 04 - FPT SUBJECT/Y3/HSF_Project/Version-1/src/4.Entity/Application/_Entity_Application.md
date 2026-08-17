# 🏛️ Entity: Application

> [!abstract] Định nghĩa
> **Loại:** `Entity Class` — Ánh xạ đến bảng `applications` trong database.
> **Package:** `com.example.groupproject.entity`
> **Annotation:** `@Entity @Table(name = "applications")` với unique constraint `(job_id, candidate_id)`

---

## 🗄️ Ánh xạ Database

```sql
-- Bảng: applications
CREATE TABLE applications (
    id                INT AUTO_INCREMENT PRIMARY KEY,
    job_id            INT          NOT NULL REFERENCES job_postings(id),
    candidate_id      INT          NOT NULL REFERENCES users(id),
    cover_letter      TEXT,
    cv_filename       VARCHAR(255) NOT NULL,
    cv_storage_path   VARCHAR(500) NOT NULL,
    status            ENUM('APPLIED','SCREENING','INTERVIEW','OFFER','HIRED','REJECTED','WITHDRAWN') NOT NULL DEFAULT 'APPLIED',
    status_changed_at TIMESTAMP    NOT NULL,
    submitted_at      TIMESTAMP    NOT NULL,
    updated_at        TIMESTAMP    NOT NULL,
    UNIQUE (job_id, candidate_id)  -- uq_application: mỗi candidate chỉ apply 1 lần cho 1 job
);
```

---

## 📋 Thuộc tính (Fields)

| Field Java | Column DB | Kiểu | Ràng buộc | Mô tả |
|-----------|-----------|------|-----------|-------|
| `id` | `id` | `Integer` | PK, Auto Increment | Khóa chính |
| `job` | `job_id` | `JobPosting` (FK) | NOT NULL, LAZY | Job được ứng tuyển |
| `candidate` | `candidate_id` | `User` (FK) | NOT NULL, LAZY | Ứng viên nộp đơn |
| `coverLetter` | `cover_letter` | `String` | nullable, TEXT | Thư xin việc |
| `cvFilename` | `cv_filename` | `String` | NOT NULL | Tên file CV gốc |
| `cvStoragePath` | `cv_storage_path` | `String` | NOT NULL, max 500 | Đường dẫn lưu CV trên storage |
| `status` | `status` | `ApplicationStatus` (enum) | NOT NULL, default APPLIED | Trạng thái đơn |
| `statusChangedAt` | `status_changed_at` | `Instant` | NOT NULL | Thời điểm thay đổi trạng thái gần nhất |
| `submittedAt` | `submitted_at` | `Instant` | NOT NULL, not updatable | Thời điểm nộp đơn |
| `updatedAt` | `updated_at` | `Instant` | NOT NULL | Thời điểm cập nhật cuối |

---

## 🔗 Được sử dụng trong dự án

- **`ApplicationRepository`** — đếm application theo status (có scope theo job creator)
- **`DashboardService`** — thống kê applied candidates cho dashboard
- **`Interview`** — FK `application_id` → Application (phỏng vấn thuộc đơn nào)
