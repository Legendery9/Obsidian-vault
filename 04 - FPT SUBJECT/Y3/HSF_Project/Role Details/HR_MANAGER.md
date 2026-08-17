# 2️⃣ HR_MANAGER — Quản Lý Nhân Sự

> [!abstract] Tổng Quan Vai Trò
> **Tên vai trò:** $Role_{HR\_MANAGER}$
> **Phạm vi:** Quản lý tuyển dụng
>
> HR Manager chịu trách nhiệm toàn bộ quy trình tuyển dụng: đăng tin, xem xét ứng viên, gán phỏng vấn và theo dõi báo cáo pipeline. **Không** có quyền quản lý hệ thống người dùng.

---

## 🧩 Đặc Điểm

- 📋 **Quản lý** toàn bộ quy trình tuyển dụng
- 👥 **Xem / quản lý** ứng viên theo từng job
- 📝 **Tạo / sửa** job posting
- 🚫 **Không** quản lý user, **không** xem activity log

---

## 🛣️ Truy Cập (Routes)

> [!info] Danh Sách Route $P_{HR\_MANAGER}$
>
> | Method | Endpoint | Chức năng |
> |--------|----------|-----------|
> | `GET`  | `/hr/dashboard` | Dashboard tuyển dụng (metric tổng quan) |
> | `GET`  | `/hr/jobs/{jobId}/applications` | Danh sách ứng viên theo job |
> | `GET`  | `/hr/report/{jobId}` | Báo cáo pipeline recruitment |
> | `GET`  | `/jobs` | Danh sách job (management view) |
> | `POST` | `/jobs` | Tạo job posting mới |
> | `GET`  | `/jobs/{id}` | Chi tiết job |
> | `POST` | `/jobs/{id}` | Cập nhật job |
> | `GET`  | `/profile` | Xem profile cá nhân |

---

## ✅ Quyền Chi Tiết

- ✅ Xem **dashboard recruitment** (tóm tắt ứng viên, active jobs)
- ✅ Lọc ứng viên theo trạng thái: `APPLIED`, `SCREENING`, `INTERVIEW`, `OFFER`, `HIRED`, `REJECTED`, `WITHDRAWN`
- ✅ Xem **báo cáo pipeline** (thống kê theo trạng thái)
- ✅ **Quản lý job posting** (tạo / sửa / delete)
- ✅ Hỗ trợ **HTMX real-time updates**
- ❌ **Không** quản lý user
- ❌ **Không** xem activity log
- ❌ **Không** khóa / unlock tài khoản

---

## 🔐 Code Kiểm Tra

> [!warning] Yêu Cầu Xác Thực Role
> Endpoint của $HR\_MANAGER$ chấp nhận cả $ADMIN$ vì $ADMIN$ có quyền kế thừa toàn hệ thống.
> Thiếu kiểm tra này có thể cho phép $CANDIDATE$ hoặc $INTERVIEWER$ truy cập trái phép.

```java
authService.requireAnyRole(currentUser, UserRole.ADMIN, UserRole.HR_MANAGER);
```

> [!note] Ví Dụ Kịch Bản Sử Dụng
> **Scenario:** HR xem pipeline tuyển dụng cho vị trí "Backend Developer".
> 1. Truy cập `GET /hr/dashboard` → xem tổng quan số ứng viên
> 2. Chọn job `jobId = 42` → `GET /hr/jobs/42/applications`
> 3. Lọc theo `status = SCREENING` → xem CV từng ứng viên
> 4. Update trạng thái → gán phỏng vấn cho $INTERVIEWER$ ✅