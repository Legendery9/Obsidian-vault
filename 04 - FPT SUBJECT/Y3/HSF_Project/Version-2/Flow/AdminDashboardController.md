# 1️⃣ AdminDashboardController — `/admin/**`

> [!abstract]
> Controller cho **Admin Dashboard** và **Activity Log**. Chỉ `ADMIN` mới có quyền truy cập. Toàn bộ validation phân quyền thực hiện bằng `AuthService.requireRole()` — throw exception nếu không đủ quyền.

---

## 📌 Endpoints

### `GET /admin/dashboard`

```
Request → AdminDashboardController.dashboard()
    ↓
AuthService.requireRole(user, ADMIN)          ← Bắt buộc ADMIN
    ↓
DashboardService.getAdminDashboardData()
    └── Trả về AdminDashboardData:
        ├── totalUsers       — Tổng số tài khoản
        ├── totalJobs        — Tổng số tin tuyển dụng
        ├── totalApplications — Tổng số đơn ứng tuyển
        └── newUsersThisMonth — User mới trong tháng
    ↓
DashboardService.getRecentActivityEvents()
    └── 10 activity log gần nhất (ActivityLogDisplayView)
    ↓
model.addAttribute("dashboard", ...)
model.addAttribute("recentActivity", ...)
    ↓
return "admin/dashboard"     ← Thymeleaf template
```

---

### `GET /admin/activity-log`

```
Request (với optional query params) → AdminDashboardController.activityLog()
    │
    ├── @RequestParam search        (nullable) — Tìm theo username/mô tả
    ├── @RequestParam eventType     (nullable) — Filter theo ActivityEventType enum
    ├── @RequestParam dateFrom      (nullable, ISO date) — Filter từ ngày
    ├── @RequestParam dateTo        (nullable, ISO date) — Filter đến ngày
    └── @RequestParam page          (default=0) — Số trang (0-indexed)
    ↓
AuthService.requireRole(user, ADMIN)
    ↓
DashboardService.searchActivityLogs(search, eventType, dateFrom, dateTo, page)
    └── Trả về Page<ActivityLogDisplayView> (phân trang, 20 bản ghi/trang)
    ↓
model.addAttribute:
    ├── "logsPage"         — Page<ActivityLogDisplayView>
    ├── "search"           — Giá trị tìm kiếm hiện tại
    ├── "selectedEventType" — EventType đang filter
    ├── "dateFrom"         — Ngày bắt đầu
    ├── "dateTo"           — Ngày kết thúc
    ├── "currentPage"      — Trang hiện tại (dùng cho pagination UI)
    └── "eventTypes"       — ActivityEventType.values() (dropdown)
    ↓
return "admin/activity-log"
```

---

## ⚙️ Dependencies

| Dependency | Mục đích |
|---|---|
| `AuthService` | Lấy user từ session, validate quyền ADMIN |
| `DashboardService` | Tổng hợp dữ liệu dashboard và tìm kiếm log |

---

## 📝 Key Responsibilities

- **Admin dashboard metrics** — tổng hợp số liệu hệ thống real-time
- **Activity log** — tra cứu lịch sử hành động với filter đa chiều
- **Pagination** — hỗ trợ phân trang activity log
- **Date range filter** — dùng `@DateTimeFormat(iso = ISO.DATE)` để parse query param

> [!warning]
> Nếu user không có role `ADMIN`, `AuthService.requireRole()` sẽ **throw exception** (không phải redirect) — exception này cần được xử lý ở tầng filter/advice hoặc sẽ gây 500 error. `AuthInterceptor` đã chặn trước bằng 403 Forbidden nên thực tế ít khi xảy ra.