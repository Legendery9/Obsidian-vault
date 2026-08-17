# 📝 Class: AdminDashboardData (DTO)

> [!abstract] Phân loại
> **Loại:** `DTO Class` — Đóng gói dữ liệu tổng hợp cho Admin Dashboard.
> **Package:** `com.example.groupproject.dto`

---

## 📋 Fields

| Field | Kiểu | Mô tả |
|-------|------|-------|
| `userCountByRole` | `Map<UserRole, Long>` | Số lượng user theo từng role |
| `lockedAccountCount` | `long` | Số tài khoản bị khóa (LOCKED) |
| `recruitmentSummary` | `RecruitmentSummary` | Thống kê tuyển dụng toàn hệ thống |

---

## 🔗 Sử dụng trong
- `DashboardService.getAdminDashboardData()` → tạo instance
- `AdminDashboardController` → add vào Model (`model.addAttribute("dashboard", ...)` )
- `templates/admin/dashboard.html` → `${dashboard.userCountByRole}`, `${dashboard.lockedAccountCount}`, `${dashboard.recruitmentSummary.*}`
