# 🎮 Method: dashboard (GET /admin/dashboard)

> [!abstract] Phân loại
> **Class:** `AdminDashboardController` | **Loại:** `Controller Method` — Admin-only GET handler
> **Package:** `com.example.groupproject.controller`
> **Base mapping:** `@RequestMapping("/admin")`

## 🗺️ Ánh xạ
- **HTTP Method:** `GET`
- **URL:** `/admin/dashboard`
- **Trả về view:** `admin/dashboard` (render `templates/admin/dashboard.html`)
- **Quyền truy cập:** Chỉ `ADMIN` role

## 🎯 Tác dụng
Hiển thị trang Admin Dashboard với:
- Số lượng users theo từng role
- Số tài khoản bị khóa
- Thống kê tuyển dụng hệ thống (active jobs, applied candidates, upcoming interviews)
- 10 sự kiện activity log gần nhất

## 💉 Dependencies
- `DashboardService dashboardService` — cung cấp dữ liệu tổng hợp dashboard
- `AuthService authService` — kiểm tra role ADMIN

## 📥 Parameters & 📤 Return

```java
public String dashboard(Model model, HttpSession session)
// Return: "admin/dashboard"
```

| Tham số | Kiểu | Mô tả |
|---------|------|-------|
| `model` | `Model` | Spring MVC model để truyền data sang view |
| `session` | `HttpSession` | Session để lấy current user |

**Model attributes được add:**
- `dashboard` → `AdminDashboardData` (userCountByRole, lockedAccountCount, recruitmentSummary)
- `recentActivity` → `List<ActivityLogDisplayView>` (10 sự kiện mới nhất)

**Return:** `String` — `"admin/dashboard"`
