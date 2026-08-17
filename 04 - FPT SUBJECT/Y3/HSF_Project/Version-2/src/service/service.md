# Package: service

> [!abstract]
> Package `service` là tầng **Business Logic** — nơi xử lý toàn bộ nghiệp vụ của ứng dụng. Controller chỉ điều phối request/response; Service chứa mọi rule, validation logic, và phối hợp các Repository. Annotated `@Service` và thường `@Transactional` để đảm bảo toàn vẹn dữ liệu.

---

## 📄 Danh sách Services

### `AuthService.java` — Authentication & Authorization
> [!info]
> Service trung tâm, được inject vào **hầu hết** mọi Controller và Config class.
>
> **Các method chính:**
>
> | Method | Mô tả |
> |---|---|
> | `login(dto, session)` | Xác thực user, lưu vào session, xử lý failed login counter |
> | `doLogout(session)` | Invalidate session |
> | `register(dto, baseUrl)` | Tạo tài khoản CANDIDATE mới, gửi email xác thực |
> | `verifyEmail(token)` | Kích hoạt tài khoản từ link email |
> | `createResetPasswordOtp(dto)` | Tạo OTP reset password, lưu vào `PasswordResetToken` |
> | `resetPassword(dto)` | Validate OTP và cập nhật mật khẩu mới |
> | `changePassword(userId, old, new, confirm)` | Đổi mật khẩu sau khi xác thực mật khẩu cũ |
> | `getCurrentUser(session)` | Lấy User object từ session |
> | `requireRole(user, role)` | Throw exception nếu user không có role yêu cầu |
> | `requireAnyRole(user, roles...)` | Throw exception nếu không có bất kỳ role nào |
> | `hasAnyRole(user, roles...)` | Trả `boolean` kiểm tra role |

---

### `DashboardService.java` — Dashboard Data
> [!info]
> | Method | Dùng bởi | Mô tả |
> |---|---|---|
> | `getAdminDashboardData()` | AdminDashboardController | Tổng hợp metrics: tổng user, job, đơn tháng này... |
> | `getRecentActivityEvents()` | AdminDashboardController | 10 activity log gần nhất |
> | `searchActivityLogs(search, type, from, to, page)` | AdminDashboardController | Tìm kiếm log có filter + phân trang |
> | `getRecruitmentSummary(user)` | HrDashboardController | Tổng hợp pipeline tuyển dụng |
> | `getActiveJobRows(user)` | HrDashboardController | Danh sách job đang active |

---

### `ApplicationService.java` — Quản lý đơn ứng tuyển
> [!info]
> | Method | Mô tả |
> |---|---|
> | `applyToJob(jobId, user, form)` | Candidate nộp đơn (kiểm tra trùng, lưu CV) |
> | `getApplicationsForJob(jobId, status, user)` | Lấy đơn theo job + filter status |
> | `getApplicationsByCandidate(candidateId)` | Đơn của một candidate |
> | `getApplicationCountsByStage(jobId)` | Số đơn theo stage (Map<String, Long>) |
> | `withdrawApplication(id, user)` | Candidate rút đơn |
> | `hasApplied(jobId, candidateId)` | Kiểm tra đã apply chưa |

---

### `ApplicationDetailService.java` — Chi tiết đơn ứng tuyển
> [!info]
> | Method | Mô tả |
> |---|---|
> | `getApplicationDetail(id, user)` | Lấy `ApplicationDetailDTO` (thông tin đầy đủ + interviews) |
> | `findAppIdByUserId(userId)` | Bridge: tìm appId từ userId (dùng cho redirect) |

---

### `JobManagementService.java` — Quản lý tin tuyển dụng (ADMIN/HR)
> [!info]
> | Method | Mô tả |
> |---|---|
> | `getJobsForList(user, status, keyword, dept)` | Danh sách job có filter (phân nhánh admin vs hr) |
> | `getJobById(id, user)` | Lấy job (kiểm tra quyền HR với job của mình) |
> | `saveJob(dto, user)` | Tạo mới hoặc cập nhật job posting |
> | `publishJob(id, user)` | Chuyển trạng thái: DRAFT → ACTIVE |
> | `closeJob(id, user)` | Chuyển trạng thái: ACTIVE → CLOSED |
> | `deleteJob(id, user)` | Xóa job (chỉ DRAFT mới được xóa) |
> | `getDistinctDepartments(user)` | Dropdown filter phòng ban |
> | `getJobCountsByStatus(user)` | Số job theo trạng thái |

---

### `JobService.java` — Public Job (Guest/Candidate)
> [!info]
> | Method | Mô tả |
> |---|---|
> | `getPublicJobList(dept, location)` | Danh sách job ACTIVE cho public |
> | `getJobById(id)` | Chi tiết job (không cần auth) |

---

### `UserManagementService.java` — Quản lý tài khoản (ADMIN)
> [!info]
> | Method | Mô tả |
> |---|---|
> | `searchUsers(search, role, status)` | Tìm kiếm user với filter |
> | `createUser(form, actor)` | Tạo HR_MANAGER hoặc INTERVIEWER mới |
> | `unlockUser(id, actor)` | LOCKED → ACTIVE (ghi activity log) |
> | `deactivateUser(id, actor)` | ACTIVE → INACTIVE (ghi activity log) |
> | `canUnlock(user)` | `boolean` — user có thể unlock không? |
> | `canDeactivate(user)` | `boolean` — user có thể deactivate không? |

---

### `UserService.java` — Tiện ích User
> [!info]
> Service nhỏ với các tiện ích phụ trợ, không chứa core logic.

---

### `EmailService.java` — Gửi Email
> [!info]
> | Method | Mô tả |
> |---|---|
> | `sendVerificationEmail(email, token)` | Gửi link xác thực tài khoản sau đăng ký |
> | `sendResetPasswordEmail(email, otp)` | Gửi OTP reset password |
>
> Dùng `JavaMailSender` (Spring Mail) với cấu hình SMTP Gmail từ `application.properties`.

---

### `FileStorageService.java` — Lưu trữ File
> [!info]
> | Method | Mô tả |
> |---|---|
> | `storeFile(file)` | Lưu file CV tải lên vào thư mục `uploads/` |
> | `loadFile(filename)` | Lấy file đã lưu |
>
> Giới hạn file: 5MB (cấu hình tại `application.properties`).

---

## 🔗 Dependencies giữa Services

```
AuthService ←── LoginController, RegisterController, ChangePasswordController
              └── ResetPasswordController
DashboardService ←── AdminDashboardController, HrDashboardController
ApplicationService ←── HrDashboardController, CandidateController, JobController
JobManagementService ←── JobController
UserManagementService ←── UserManagementController
EmailService ←── AuthService, ResetPasswordController
FileStorageService ←── ApplicationService
```
