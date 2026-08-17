# Package: entity

> [!abstract]
> Package `entity` định nghĩa **các class ánh xạ trực tiếp với bảng trong database** (MySQL). Hibernate dùng các annotation JPA để tự động sinh và quản lý schema. Ngoài ra, package còn có 2 sub-package: `enums` (kiểu dữ liệu liệt kê) và `view` (database views dạng read-only).

---

## 📄 Entities Chính

### `User.java` — Bảng `users`
| Field | Kiểu | Mô tả |
|---|---|---|
| `id` | `Integer` | Primary Key (auto-increment) |
| `fullName` | `String` | Họ và tên |
| `username` | `String` | Tên đăng nhập (unique) |
| `email` | `String` | Email (unique) |
| `passwordHash` | `String` | Mật khẩu đã BCrypt encode |
| `role` | `UserRole` (enum) | `ADMIN`, `HR_MANAGER`, `INTERVIEWER`, `CANDIDATE` |
| `status` | `UserStatus` (enum) | `ACTIVE`, `INACTIVE`, `LOCKED` |
| `failedLoginCount` | `Short` | Số lần đăng nhập sai liên tiếp |
| `emailVerified` | `Boolean` | Đã xác thực email chưa |

---

### `JobPosting.java` — Bảng `job_postings`
| Field | Kiểu | Mô tả |
|---|---|---|
| `id` | `Integer` | Primary Key |
| `title` | `String` | Tên vị trí tuyển dụng |
| `department` | `String` | Phòng ban |
| `location` | `String` | Địa điểm làm việc |
| `description` | `String` | Mô tả công việc |
| `requirements` | `String` | Yêu cầu ứng viên |
| `salaryRange` | `String` | Mức lương |
| `applicationDeadline` | `LocalDate` | Hạn nộp đơn |
| `status` | `JobStatus` (enum) | `DRAFT`, `ACTIVE`, `CLOSED` |
| `postedBy` | `User` (`@ManyToOne`) | HR/Admin đã đăng tin |

---

### `Application.java` — Bảng `applications`
| Field | Kiểu | Mô tả |
|---|---|---|
| `id` | `Integer` | Primary Key |
| `candidate` | `User` (`@ManyToOne`) | Ứng viên nộp đơn |
| `job` | `JobPosting` (`@ManyToOne`) | Tin tuyển dụng tương ứng |
| `status` | `ApplicationStatus` (enum) | Trạng thái đơn ứng tuyển |
| `appliedAt` | `Instant` | Thời điểm nộp đơn |
| `cvFilePath` | `String` | Đường dẫn file CV |
| `coverLetter` | `String` | Thư xin việc |

---

### `Interview.java` — Bảng `interviews`
| Field | Kiểu | Mô tả |
|---|---|---|
| `id` | `Integer` | Primary Key |
| `application` | `Application` (`@ManyToOne`) | Đơn ứng tuyển được phỏng vấn |
| `interviewer` | `User` (`@ManyToOne`) | Người phỏng vấn |
| `assignedBy` | `User` (`@ManyToOne`) | HR/Admin phân công |
| `interviewDate` | `LocalDate` | Ngày phỏng vấn |
| `interviewTime` | `LocalTime` | Giờ phỏng vấn |
| `locationOrLink` | `String` | Địa điểm hoặc link meeting |
| `status` | `InterviewStatus` (enum) | `SCHEDULED`, `EVALUATED` |
| `rating` | `Short` | Điểm đánh giá (1-5) |
| `feedback` | `String` | Nhận xét của interviewer |
| `evaluatedAt` | `Instant` | Thời điểm hoàn thành đánh giá |

---

### `ActivityLog.java` — Bảng `activity_logs`
| Field | Kiểu | Mô tả |
|---|---|---|
| `id` | `Long` | Primary Key |
| `actor` | `User` (`@ManyToOne`) | Người thực hiện hành động |
| `actorUsername` | `String` | Username snapshot (không FK để bảo toàn log) |
| `eventType` | `ActivityEventType` (enum) | Loại sự kiện |
| `description` | `String` | Mô tả chi tiết hành động |
| `createdAt` | `Instant` | Thời điểm xảy ra |

---

### `PasswordResetToken.java` — Bảng `password_reset_tokens`
| Field | Kiểu | Mô tả |
|---|---|---|
| `id` | `Long` | Primary Key |
| `user` | `User` (`@ManyToOne`) | User yêu cầu reset |
| `otp` | `String` | Mã OTP 6 số |
| `expiresAt` | `Instant` | Thời hạn OTP |
| `used` | `Boolean` | Đã dùng chưa |

---

## 🔢 Sub-package: `enums`

> [!info]
> | Enum | Giá trị |
> |---|---|
> | `UserRole` | `ADMIN`, `HR_MANAGER`, `INTERVIEWER`, `CANDIDATE` |
> | `UserStatus` | `ACTIVE`, `INACTIVE`, `LOCKED` |
> | `JobStatus` | `DRAFT`, `ACTIVE`, `CLOSED` |
> | `ApplicationStatus` | `APPLIED`, `SCREENING`, `INTERVIEW`, `OFFER`, `HIRED`, `REJECTED`, `WITHDRAWN` |
> | `InterviewStatus` | `SCHEDULED`, `EVALUATED` |
> | `ActivityEventType` | `USER_LOGIN`, `USER_REGISTER`, `JOB_CREATED`, `APPLICATION_SUBMITTED`, `STATUS_CHANGED`, `EVALUATION_SUBMITTED`, ... |

---

## 👁️ Sub-package: `view`

> [!info]
> Database views — read-only, không thể `INSERT`/`UPDATE`.
>
> | View class | Bảng/View DB | Mục đích |
> |---|---|---|
> | `ActivityLogDisplayView` | `activity_log_display_view` | Hiển thị activity log kèm thông tin actor |
> | `JobApplicationCountView` | `job_application_count_view` | Số đơn ứng tuyển theo từng job |

---

## 🔗 Quan hệ giữa các Entity

```
User ──< Application >── JobPosting
         │
         └── Interview ── User (interviewer)
                       ── User (assignedBy)

User ──< ActivityLog
User ──< PasswordResetToken
User ──< JobPosting (postedBy)
```
