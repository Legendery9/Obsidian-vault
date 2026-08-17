# 🏛️ Entity: JobPosting

> [!abstract] Định nghĩa
> **Loại:** `Entity Class` — Ánh xạ trực tiếp đến bảng `job_postings` trong database.
> **Package:** `com.example.groupproject.entity`
> **Annotation:** `@Entity @Table(name = "job_postings")`

---

## 🗄️ Ánh xạ Database

```sql
-- Bảng: job_postings
CREATE TABLE job_postings (
    id                   INT AUTO_INCREMENT PRIMARY KEY,
    title                VARCHAR(200) NOT NULL,
    department           VARCHAR(100) NOT NULL,
    location             VARCHAR(100) NOT NULL,
    description          TEXT         NOT NULL,
    requirements         TEXT,
    salary_range         VARCHAR(100),
    application_deadline DATE,
    status               ENUM('DRAFT','ACTIVE','CLOSED') NOT NULL DEFAULT 'DRAFT',
    created_by           INT          NOT NULL REFERENCES users(id),
    created_at           TIMESTAMP    NOT NULL,
    updated_at           TIMESTAMP    NOT NULL
);
```

---

## 📋 Thuộc tính (Fields)

| Field Java | Column DB | Kiểu | Ràng buộc | Mô tả |
|-----------|-----------|------|-----------|-------|
| `id` | `id` | `Integer` | PK, Auto Increment | Khóa chính |
| `title` | `title` | `String` | NOT NULL, max 200 | Tiêu đề tin tuyển dụng |
| `department` | `department` | `String` | NOT NULL, max 100 | Phòng ban tuyển dụng |
| `location` | `location` | `String` | NOT NULL, max 100 | Địa điểm làm việc |
| `description` | `description` | `String` | NOT NULL, TEXT | Mô tả công việc |
| `requirements` | `requirements` | `String` | nullable, TEXT | Yêu cầu ứng viên |
| `salaryRange` | `salary_range` | `String` | nullable, max 100 | Khoảng lương |
| `applicationDeadline` | `application_deadline` | `LocalDate` | nullable | Hạn nộp hồ sơ |
| `status` | `status` | `JobStatus` (enum) | NOT NULL, default DRAFT | Trạng thái: DRAFT/ACTIVE/CLOSED |
| `createdBy` | `created_by` | `User` (FK) | NOT NULL, LAZY | Người tạo job (HR Manager/Admin) |
| `createdAt` | `created_at` | `Instant` | NOT NULL, not updatable | Thời điểm tạo |
| `updatedAt` | `updated_at` | `Instant` | NOT NULL | Thời điểm cập nhật cuối |

---

## 🔗 Quan hệ

```java
@ManyToOne(fetch = FetchType.LAZY)
@JoinColumn(name = "created_by", nullable = false)
private User createdBy;
```

> [!note] ManyToOne với User
> Nhiều JobPosting có thể được tạo bởi một User. Dùng `LAZY` fetching để tránh N+1 query.

---

## 🔗 Được sử dụng trong dự án

- **`JobPostingRepository`** — truy vấn job theo status, người tạo, đếm số lượng
- **`DashboardService`** — lấy danh sách active jobs cho HR/Admin dashboard
- **`Application`** — FK `job_id` → JobPosting (đơn ứng tuyển thuộc job nào)
- **`JobApplicationCountView`** — VIEW đếm số application theo job
