# Package: controller

> [!abstract]
> Package `controller` là tầng tiếp nhận **HTTP request** từ browser. Mỗi Controller xử lý một nhóm chức năng, gọi các `Service` để thực hiện business logic, rồi trả về **Thymeleaf view** hoặc **redirect**. Toàn bộ 13 controller phủ kín mọi màn hình của hệ thống TalentHub.

---

## 📋 Danh sách Controllers

| Controller | Base Path | Role yêu cầu | Chức năng |
|---|---|---|---|
| `HomeController` | `/` | Public | Trang chủ / redirect |
| `LoginController` | `/login`, `/logout` | Public | Đăng nhập / Đăng xuất |
| `RegisterController` | `/register`, `/verify` | Public | Đăng ký & xác thực email |
| `ResetPasswordController` | `/forgot-password`, `/reset-password` | Public | Quên/reset mật khẩu |
| `ChangePasswordController` | `/change-password` | Any Auth | Đổi mật khẩu |
| `ProfileController` | `/profile` | Any Auth | Xem hồ sơ cá nhân |
| `AdminDashboardController` | `/admin/**` | ADMIN | Dashboard & Activity Log |
| `UserManagementController` | `/admin/users/**` | ADMIN | Quản lý tài khoản |
| `HrDashboardController` | `/hr/**` | ADMIN, HR_MANAGER | Dashboard HR & Applications |
| `JobController` | `/jobs/**` | ADMIN, HR_MANAGER (+ public) | Quản lý tin tuyển dụng |
| `ApplicationDetailController` | `/applications/**` | ADMIN, HR_MANAGER, INTERVIEWER | Chi tiết đơn ứng tuyển |
| `CandidateController` | `/candidate/applications/**` | CANDIDATE | Quản lý đơn ứng tuyển của ứng viên |
| `InterviewController` | `/interview/**` | ADMIN, HR_MANAGER | Phân công & đánh giá phỏng vấn |

---

## 🔍 Chi tiết từng Controller

### `HomeController` — `/`
- `GET /` → Nếu đã login: redirect `/profile` | Nếu chưa: render `user/index`

---

### `LoginController` — `/login`, `/logout`
- `GET /login` → Hiển thị form (nếu đã login → redirect theo role)
- `POST /login` → Gọi `AuthService.login()`, redirect theo role:
  - `ADMIN` → `/admin/dashboard`
  - `HR_MANAGER` → `/hr/dashboard`
  - `INTERVIEWER` → `/interviewer/applications`
  - `CANDIDATE` → `/candidate/applications`
- `POST /logout` → `AuthService.doLogout()` → redirect `/login`
- **Exception handling:** `AccountLockedException`, `AdminLockedException`, `IllegalArgumentException`

---

### `RegisterController` — `/register`, `/verify`
- `GET /register` → Hiển thị form đăng ký
- `POST /register` → Validate `RegisterDTO`, gọi `AuthService.register()`, gửi email xác thực
- `GET /verify?token=...` → `AuthService.verifyEmail(token)` → redirect `/login`

---

### `ResetPasswordController` — `/forgot-password`, `/reset-password`
- `GET/POST /forgot-password` → Nhập email, tạo OTP, gửi email
- `GET/POST /reset-password` → Nhập OTP + mật khẩu mới, gọi `AuthService.resetPassword()`

---

### `ChangePasswordController` — `/change-password`
- `GET /change-password` → Hiển thị form (redirect login nếu chưa auth)
- `POST /change-password` → `AuthService.changePassword()`, `session.invalidate()` → redirect `/login`

---

### `ProfileController` — `/profile`
- `GET /profile` → Lấy user từ session, render `user/profile` (redirect `/login` nếu null)

---

### `AdminDashboardController` — `/admin/dashboard`, `/admin/activity-log`
- `GET /admin/dashboard` → `DashboardService.getAdminDashboardData()` + `getRecentActivityEvents()`
- `GET /admin/activity-log` → `DashboardService.searchActivityLogs(search, eventType, dateFrom, dateTo, page)` — hỗ trợ filter + pagination

---

### `UserManagementController` — `/admin/users/**`
- `GET /admin/users` → Danh sách user với search/filter + flag `canUnlock`, `canDeactivate`
- `POST /admin/users` → Tạo user mới (chỉ `HR_MANAGER`, `INTERVIEWER`)
- `POST /admin/users/{id}/unlock` → LOCKED → ACTIVE
- `POST /admin/users/{id}/deactivate` → ACTIVE → INACTIVE

---

### `HrDashboardController` — `/hr/**`
- `GET /hr/dashboard` → Recruitment summary + active jobs
- `GET /hr/jobs/{jobId}/applications` → Danh sách application theo jobId + filter status. Hỗ trợ **HTMX** fragment response
- `GET /hr/report/{jobId}` → Pipeline analytics theo jobId

---

### `JobController` — `/jobs/**`
- `GET /jobs` → **Phân nhánh**: Guest/CANDIDATE → public list | ADMIN/HR → admin list
- `GET /jobs/{id}` → **Phân nhánh**: Staff → detail with applications | Public → public-detail
- `GET /jobs/create`, `GET /jobs/edit/{id}` → Form tạo/sửa job (ADMIN, HR_MANAGER)
- `POST /jobs/save` → Lưu job (save draft hoặc publish)
- `POST /jobs/{id}/publish`, `/close`, `/delete` → Thay đổi trạng thái job
- `POST /jobs/{id}/apply` → Candidate nộp đơn ứng tuyển

---

### `ApplicationDetailController` — `/applications/**`
- `GET /applications/{id}` → Chi tiết application (ADMIN, HR_MANAGER, INTERVIEWER)
- `GET /applications/user/{userId}` → Bridge redirect: userId → appId → chi tiết

---

### `CandidateController` — `/candidate/applications/**`
- `GET /candidate/applications` → Danh sách đơn ứng tuyển của candidate + filter status
- `POST /candidate/applications/{id}/withdraw` → Rút đơn ứng tuyển

---

### `InterviewController` — `/interview/**`
- `GET /interview/assign/{applicationId}` → Form phân công phỏng vấn
- `POST /interview/assign` → Lưu interview record (date, time, location, interviewer)
- `GET /interview/evaluate/{interviewId}` → Form đánh giá phỏng vấn
- `POST /interview/evaluate` → Lưu đánh giá (rating, feedback) + log `EVALUATION_SUBMITTED`
