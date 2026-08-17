# Package: repository

> [!abstract]
> Package `repository` là tầng **truy cập dữ liệu** (Data Access Layer). Mỗi Repository là một interface extend `JpaRepository` — Spring Data JPA tự động cung cấp các phương thức CRUD cơ bản. Các phương thức custom được định nghĩa thêm bằng **JPQL query** (`@Query`) hoặc **method naming convention**.

---

## 📄 Danh sách Repositories

### `UserRepository`
> [!info]
> **Entity:** `User` | **ID type:** `Integer`
>
> | Method | Mô tả |
> |---|---|
> | `findByUsername(username)` | Tìm user theo username (dùng login) |
> | `findByEmail(email)` | Tìm user theo email (dùng reset password) |
> | `countByRole(role)` | Đếm user theo role (dùng DataInitializer) |
> | `findByRoleAndStatusOrderByFullNameAsc(role, status)` | Lấy danh sách interviewer active |
> | `searchUsers(search, role, status)` | Tìm kiếm user với filter tổng hợp |

---

### `JobPostingRepository`
> [!info]
> **Entity:** `JobPosting` | **ID type:** `Integer`
>
> | Method | Mô tả |
> |---|---|
> | `findJobsForAdmin(keyword, department, status)` | Lấy tất cả job (ADMIN view) |
> | `findJobsForHr(hrManagerId, keyword, department, status)` | Lấy job của HR cụ thể |
> | `findPublicJobs(department, location)` | Job ACTIVE dành cho public/candidate |
> | `findDistinctDepartments(userId, role)` | Dropdown filter phòng ban |
> | `countByStatus(role, userId, status)` | Đếm job theo trạng thái |

---

### `ApplicationRepository`
> [!info]
> **Entity:** `Application` | **ID type:** `Integer`
>
> | Method | Mô tả |
> |---|---|
> | `findByJobId(jobId)` | Lấy tất cả đơn của một job |
> | `findByJobIdAndStatus(jobId, status)` | Filter đơn theo status |
> | `findByCandidateId(candidateId)` | Đơn của một candidate |
> | `existsByJobIdAndCandidateId(jobId, candidateId)` | Kiểm tra đã apply chưa |
> | `countApplicationsByStatusAndJobId(jobId)` | Thống kê đơn theo status/job |
> | `getApplicationCountsByStage(jobId)` | Số đơn theo từng stage (Map) |

---

### `InterviewRepository`
> [!info]
> **Entity:** `Interview` | **ID type:** `Integer`
>
> | Method | Mô tả |
> |---|---|
> | `findByApplicationId(applicationId)` | Lấy phỏng vấn của một application |
> | `findByInterviewerId(interviewerId)` | Lịch phỏng vấn của một interviewer |

---

### `ActivityLogRepository`
> [!info]
> **Entity:** `ActivityLog` | **ID type:** `Long`
>
> Chủ yếu dùng phương thức `save()` kế thừa từ `JpaRepository` để ghi log.

---

### `ActivityLogDisplayViewRepository`
> [!info]
> **Entity:** `ActivityLogDisplayView` (read-only view) | **ID type:** `Long`
>
> | Method | Mô tả |
> |---|---|
> | `searchLogs(search, eventType, dateFrom, dateTo, pageable)` | Tìm kiếm log với filter + phân trang |

---

### `JobApplicationCountViewRepository`
> [!info]
> **Entity:** `JobApplicationCountView` (read-only view) | **ID type:** `Integer`
>
> Cung cấp số lượng đơn ứng tuyển theo từng job — dùng trong HR dashboard.

---

## 🔧 Kỹ thuật sử dụng

> [!info]
> - **Method Naming Convention:** Spring tự sinh SQL từ tên method. Ví dụ: `findByEmailAndStatus` → `SELECT * FROM users WHERE email=? AND status=?`
> - **`@Query` (JPQL):** Dùng cho các câu truy vấn phức tạp với nhiều điều kiện dynamic (search, filter đa tiêu chí)
> - **`Page<T>`:** Một số method nhận `Pageable` để hỗ trợ phân trang — dùng trong activity log
> - **View Repositories:** `ActivityLogDisplayViewRepository`, `JobApplicationCountViewRepository` map đến database view — **chỉ đọc**, không `save()`/`delete()`
