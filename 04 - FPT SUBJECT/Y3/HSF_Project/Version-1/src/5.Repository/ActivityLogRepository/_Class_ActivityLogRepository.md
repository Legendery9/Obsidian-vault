# 🗄️ Interface: ActivityLogRepository

> [!abstract] Phân loại
> **Loại:** `Repository Interface` — JPA Repository chỉ dùng để WRITE log.
> **Package:** `com.example.groupproject.repository`
> **Extends:** `JpaRepository<ActivityLog, Long>`

---

> [!note] Điểm đặc biệt
> Chỉ dùng để **ghi log** (save). Việc **đọc log** được thực hiện qua `ActivityLogDisplayViewRepository` (đọc từ DB VIEW `v_activity_log_display` có thêm cột `actor_display_name`).

Không có custom method — chỉ dùng `save()` kế thừa từ `JpaRepository`.
