# 1️⃣ ADMIN — Quản Trị Viên Hệ Thống

> [!abstract] Tổng Quan Vai Trò
> **Tên vai trò:** $Role_{ADMIN}$
> **Phạm vi:** Toàn bộ hệ thống
>
> Quản trị viên là cấp quyền **cao nhất** trong hệ thống HSF. Có toàn quyền kiểm soát người dùng, hoạt động hệ thống và quản lý quy trình tuyển dụng.

---

## 🧩 Đặc Điểm

- 🔑 **Quyền cao nhất** trong hệ thống
- 👥 Có thể **quản lý toàn bộ người dùng**
- 📋 Xem được **tất cả hoạt động** hệ thống
- 🔒 **Khóa / Mở khóa / Deactivate** tài khoản người dùng

---

## 🛣️ Truy Cập (Routes)

> [!info] Danh Sách Route $P_{ADMIN}$
>
> | Method | Endpoint | Chức năng |
> |--------|----------|-----------|
> | `GET`  | `/admin/dashboard` | Dashboard quản lý hệ thống |
> | `GET`  | `/admin/activity-log` | Xem log hoạt động hệ thống |
> | `GET`  | `/admin/users` | Danh sách tất cả user |
> | `POST` | `/admin/users` | Tạo user mới ($HR\_MANAGER$, $INTERVIEWER$) |
> | `POST` | `/admin/users/{id}/unlock` | Mở khóa tài khoản (`LOCKED` → `ACTIVE`) |
> | `POST` | `/admin/users/{id}/deactivate` | Khóa vĩnh viễn (`ACTIVE` → `INACTIVE`) |
> | `GET`  | `/hr/dashboard` | Dashboard tuyển dụng *(shared với $HR\_MANAGER$)* |
> | `GET`  | `/hr/jobs/{jobId}/applications` | Xem ứng viên theo job |
> | `GET`  | `/hr/report/{jobId}` | Xem báo cáo pipeline |
> | `GET`  | `/profile` | Xem profile cá nhân |

---

## ✅ Quyền Chi Tiết

- ✅ Xem / quản lý **tất cả user** ($ADMIN$, $HR\_MANAGER$, $INTERVIEWER$, $CANDIDATE$)
- ✅ **Tạo user mới** (chỉ $HR\_MANAGER$ và $INTERVIEWER$)
- ✅ **Khóa / Mở khóa / Deactivate** tài khoản
- ✅ Xem toàn bộ **activity log** (tìm kiếm, lọc theo ngày)
- ✅ **Quản lý job posting**
- ✅ Xem **báo cáo recruitment**
- ✅ Tạo / sửa / xóa **job posting**

---

## 🔐 Code Kiểm Tra

> [!warning] Yêu Cầu Xác Thực Role
> Mọi endpoint yêu cầu quyền $ADMIN$ **bắt buộc** phải kiểm tra role trước khi xử lý logic.
> Thiếu bước này có thể dẫn đến **leo quyền trái phép** (privilege escalation).

```java
authService.requireRole(authService.getCurrentUser(session), UserRole.ADMIN);
```

> [!note] Ví Dụ Kịch Bản Sử Dụng
> **Scenario:** Admin mở khóa tài khoản HR bị khóa nhầm.
> 1. Truy cập `GET /admin/users` → tìm user bị `LOCKED`
> 2. Gọi `POST /admin/users/{id}/unlock`
> 3. Trạng thái chuyển: `LOCKED` → `ACTIVE`
> 4. User có thể đăng nhập lại bình thường ✅