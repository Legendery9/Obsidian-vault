# Package: dto

> [!abstract]
> Package `dto` (Data Transfer Object) chứa các class trung gian dùng để **truyền dữ liệu** giữa View (form HTML), Controller và Service. DTO tách biệt hoàn toàn với Entity — không ánh xạ trực tiếp với database, giúp kiểm soát chính xác dữ liệu nào được nhận vào và trả ra.

---

## 📁 Danh sách DTOs

| DTO | Hướng dữ liệu | Mục đích |
|---|---|---|
| `LoginDTO` | Form → Controller | Nhận username + password khi đăng nhập |
| `RegisterDTO` | Form → Controller | Nhận thông tin đăng ký tài khoản mới |
| `ChangePasswordDTO` | Form → Controller | Nhận old/new/confirm password |
| `ForgotPasswordDTO` | Form → Controller | Nhận email để gửi OTP reset |
| `ResetPasswordDTO` | Form → Controller | Nhận OTP + mật khẩu mới |
| `CreateUserForm` | Form → Controller | Tạo user mới (HR_MANAGER / INTERVIEWER) |
| `JobFormDTO` | Form ↔ Controller | Tạo/sửa tin tuyển dụng |
| `ApplicationForm` | Form → Controller | Candidate nộp đơn ứng tuyển |
| `ApplicationDetailDTO` | Service → View | Chi tiết đầy đủ của một đơn ứng tuyển |
| `InterviewAssignmentDTO` | Form → Controller | Phân công phỏng vấn (interviewer, date, time, location) |
| `JobListRow` | Service → View | Một dòng trong danh sách job (admin/hr view) |
| `ActiveJobRow` | Service → View | Một dòng job đang active trong HR dashboard |
| `AdminDashboardData` | Service → View | Tổng hợp metrics cho admin dashboard |
| `RecruitmentSummary` | Service → View | Tổng hợp số liệu tuyển dụng cho HR dashboard |

---

## 📌 Phân loại theo chiều dữ liệu

### 📥 Input DTOs (Form → Controller)
Các DTO nhận input từ HTML form, thường được validate với `@Valid`:

- **`LoginDTO`** — `username`, `password`
- **`RegisterDTO`** — `fullName`, `username`, `email`, `password`, `confirmPassword`
- **`ChangePasswordDTO`** — `oldPassword`, `newPassword`, `confirmPassword`
- **`ForgotPasswordDTO`** — `email`
- **`ResetPasswordDTO`** — `email`, `otp`, `newPassword`, `confirmPassword`
- **`CreateUserForm`** — `fullName`, `username`, `email`, `password`, `role` (`HR_MANAGER` / `INTERVIEWER` only)
- **`JobFormDTO`** — `title`, `department`, `location`, `description`, `requirements`, `salaryRange`, `deadline`, `status`
- **`ApplicationForm`** — thông tin nộp đơn ứng tuyển của candidate
- **`InterviewAssignmentDTO`** — `applicationId`, `interviewerId`, `interviewDate`, `interviewTime`, `locationOrLink`

### 📤 Output DTOs (Service → View)
Các DTO đóng gói dữ liệu để hiển thị lên Thymeleaf:

- **`AdminDashboardData`** — Tổng số user, job, application, user mới trong tháng...
- **`RecruitmentSummary`** — Số job active, tổng application, interview đang chờ...
- **`ActiveJobRow`** — Tên job, số application, deadline, trạng thái
- **`JobListRow`** — Dữ liệu đầy đủ 1 dòng job trong bảng quản lý
- **`ApplicationDetailDTO`** — Thông tin candidate, job, danh sách interview, trạng thái đơn

---

## 🔧 Validation

> [!info]
> Các Input DTO sử dụng annotation từ `spring-boot-starter-validation`:
> - `@NotBlank` — Trường không được để trống
> - `@Email` — Phải đúng định dạng email
> - `@Size(min, max)` — Giới hạn độ dài chuỗi
>
> Controller dùng `@Valid` + `BindingResult` để bắt lỗi:
> ```java
> public String create(@Valid @ModelAttribute("form") CreateUserForm form,
>                      BindingResult result) {
>     if (result.hasErrors()) { return "admin/users"; }
>     ...
> }
> ```
