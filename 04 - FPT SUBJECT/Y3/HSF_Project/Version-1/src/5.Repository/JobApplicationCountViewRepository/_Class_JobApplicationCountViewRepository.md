# 🗄️ Interface: JobApplicationCountViewRepository

> [!abstract] Phân loại
> **Loại:** `Repository Interface` — Đọc từ DB VIEW `v_job_application_counts`.
> **Package:** `com.example.groupproject.repository`
> **Extends:** `JpaRepository<JobApplicationCountView, Integer>`

---

> [!note] VIEW `v_job_application_counts`
> VIEW này tổng hợp số application theo từng trạng thái cho mỗi job. Các cột: `job_id`, `total`, `applied`, `screening`, `interview`, `offer`, `hired`, `rejected`, `withdrawn`.

Dùng `findAll()` kế thừa từ `JpaRepository` — `DashboardService` gọi để lấy số application từng job.
