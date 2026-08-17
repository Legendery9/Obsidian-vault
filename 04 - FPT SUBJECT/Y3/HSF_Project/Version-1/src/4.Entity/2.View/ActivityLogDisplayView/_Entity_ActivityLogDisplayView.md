# 🗄️ Entity (View): ActivityLogDisplayView

> [!abstract] Phân loại
> **Loại:** `View Entity` — Ánh xạ đến DB VIEW `v_activity_log_display`.
> **Package:** `com.example.groupproject.entity.view`
> **Annotation:** `@Entity @Immutable @Table(name = "v_activity_log_display")`

---

## 📄 DB View: `v_activity_log_display`

> [!info] Mục đích
> VIEW này join bảng `activity_log` với `users` để bổ sung cột `actor_display_name` (hiển thị "FirstName LastName" thay vì chỉ username). Read-only (`@Immutable`).

## 📋 Fields

| Field | Column | Kiểu | Mô tả |
|-------|--------|------|-------|
| `id` | `id` | `Long` | PK (từ activity_log.id) |
| `actorId` | `actor_id` | `Integer` | ID người thực hiện |
| `actorUsername` | `actor_username` | `String` | Username |
| `eventType` | `event_type` | `ActivityEventType` | Loại sự kiện |
| `description` | `description` | `String` | Mô tả |
| `ipAddress` | `ip_address` | `String` | IP address |
| `createdAt` | `created_at` | `Instant` | Thời điểm xảy ra |
| `actorDisplayName` | `actor_display_name` | `String` | Tên hiển thị (từ JOIN với users) |

---

## 🔗 Dùng bởi
- `ActivityLogDisplayViewRepository.findTop10ByOrderByCreatedAtDesc()` → Admin Dashboard
