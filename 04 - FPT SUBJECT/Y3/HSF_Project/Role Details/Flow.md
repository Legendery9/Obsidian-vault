# 🔄 Luồng Hoạt Động — HSF System Workflows

> [!abstract] Tổng Quan
> Tài liệu này mô tả **quy trình làm việc** (workflow) của từng vai trò trong hệ thống HSF: $ADMIN$, $HR\_MANAGER$, $INTERVIEWER$, và $CANDIDATE$.
> Mỗi luồng thể hiện các bước tuần tự từ điểm vào (login/register) đến các hành động chính.

---

## 1️⃣ ADMIN Workflow

> [!note] Luồng Quản Trị Hệ Thống
> ```
> Admin Login
>   ↓
> [/admin/dashboard]       → Xem metric hệ thống
>   ↓
> [/admin/activity-log]    → Xem log hoạt động
>   ↓
> [/admin/users]           → Quản lý user
>   ├─ Tạo HR_MANAGER, INTERVIEWER
>   ├─ Unlock account
>   └─ Deactivate account
>   ↓
> [/hr/...]                → Có thể dùng HR dashboard nếu cần
> ```

---

## 2️⃣ HR_MANAGER Workflow

> [!note] Luồng Quản Lý Tuyển Dụng
> ```
> HR Login
>   ↓
> [/hr/dashboard]                      → Xem tóm tắt recruitment
>   ↓
> [/jobs]                              → Quản lý job posting
>   ├─ Tạo job mới
>   ├─ Sửa / xóa job
>   └─ Filter job
>   ↓
> [/hr/jobs/{jobId}/applications]      → Xem ứng viên
>   ├─ Lọc theo trạng thái
>   ├─ Update trạng thái
>   └─ Gán phỏng vấn cho INTERVIEWER
>   ↓
> [/hr/report/{jobId}]                 → Xem báo cáo pipeline
> ```

---

## 3️⃣ INTERVIEWER Workflow

> [!note] Luồng Thực Hiện Phỏng Vấn
> ```
> Interviewer Login
>   ↓
> [/interviews]            → Xem danh sách phỏng vấn
>   ├─ Được giao bởi HR / Admin
>   └─ Lọc theo trạng thái
>   ↓
> [/interviews/{id}]       → Xem chi tiết phỏng vấn
>   ├─ Thông tin ứng viên
>   ├─ Yêu cầu job
>   └─ Thời gian / địa điểm
>   ↓
> [/interviews/{id}/evaluate]  → Đánh giá ứng viên
>   ├─ Nhập rating (1–5)
>   ├─ Viết feedback
>   └─ Submit
>   ↓
> [/profile]               → Xem / edit profile cá nhân
> ```

---

## 4️⃣ CANDIDATE Workflow

> [!note] Luồng Ứng Tuyển Của Ứng Viên
> ```
> Candidate Register
>   ↓
> Verify Email (confirm token)
>   ↓
> Status: ACTIVE
>   ↓
> [/jobs]                      → Browse job listing
>   ├─ Filter by department / location
>   └─ Search by keyword
>   ↓
> [/jobs/{id}]                 → Xem chi tiết job
>   ↓
> POST Apply
>   ├─ Upload CV
>   ├─ Viết cover letter
>   └─ Submit
>   ↓
> [/candidate/applications]    → Track applications
>   ├─ Xem trạng thái
>   ├─ Filter by status
>   └─ Withdraw (nếu cần)
>   ↓
> Nhận thông báo email từ HR khi có phỏng vấn 📧
> ```

---

## 📊 Tổng Hợp Luồng Hệ Thống

> [!info] Ma Trận Điểm Vào Theo Vai Trò
>
> | Vai trò | Điểm vào | Dashboard chính |
> |---------|----------|-----------------|
> | $ADMIN$ | Login → `/admin/dashboard` | Quản trị hệ thống |
> | $HR\_MANAGER$ | Login → `/hr/dashboard` | Tuyển dụng |
> | $INTERVIEWER$ | Login → `/interviews` | Lịch phỏng vấn |
> | $CANDIDATE$ | Register → Verify Email → `/jobs` | Danh sách job |

> [!warning] Lưu Ý Phân Luồng
> - $CANDIDATE$ là vai trò duy nhất **tự đăng ký** — các vai trò khác do $ADMIN$ tạo.
> - $ADMIN$ có thể truy cập cả luồng của $HR\_MANAGER$ (quyền kế thừa).
> - $INTERVIEWER$ chỉ thấy phỏng vấn **được giao** — không thể xem job hay ứng viên toàn hệ thống.