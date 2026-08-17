# 🗄️ Interface: ActivityLogDisplayViewRepository

> [!abstract] Phân loại
> **Loại:** `Repository Interface` — Đọc từ DB VIEW `v_activity_log_display`.
> **Package:** `com.example.groupproject.repository`
> **Extends:** `JpaRepository<ActivityLogDisplayView, Long>`

---

## 📊 Methods

### `findTop10ByOrderByCreatedAtDesc()`
**Tác dụng:** Lấy 10 log sự kiện mới nhất (sorted by `created_at` DESC). Dùng cho Admin Dashboard.
```java
List<ActivityLogDisplayView> findTop10ByOrderByCreatedAtDesc()
```
**Return:** `List<ActivityLogDisplayView>`
