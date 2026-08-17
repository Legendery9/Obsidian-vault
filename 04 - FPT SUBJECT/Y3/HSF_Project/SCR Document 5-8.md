# Phân tích Classes cho SCR-05 đến SCR-08

## Định nghĩa SCR-05 → SCR-08 (từ Group_Project.pdf)

| Priority | SCR        | Tên màn hình        | Ai truy cập              | Mục đích                                                                                                   |
| -------- | ---------- | ------------------- | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| 1        | **SCR-05** | **User Profile**    | Tất cả user đã đăng nhập | Hiển thị thông tin tài khoản (read-only), link đến đổi mật khẩu (SCR-04) và đăng xuất                      |
| 4        | **SCR-06** | **HR Dashboard**    | HR Manager, Admin        | Tổng quan tuyển dụng: số job active, số ứng viên chờ review, phỏng vấn sắp tới, bảng job đang active       |
| 3        | **SCR-07** | **Admin Dashboard** | Admin only               | Tổng quan hệ thống: số user theo role, tài khoản bị khóa, 10 activity log gần nhất, bản tóm tắt tuyển dụng |
| 2        | **SCR-08** | **User Management** | Admin only               | Tạo/vô hiệu hóa/mở khóa tài khoản HR Manager và Interviewer; tìm kiếm/lọc user                             |

---

## SCR-05 — User Profile (`/profile`, `/change-password`)

### Controllers
| Class | Package | Vai trò |
|-------|---------|---------|
| `ProfileController` | `controller` | GET `/profile` và GET `/change-password`; đẩy `User` vào model |

### Services
| Class | Package | Vai trò |
|-------|---------|---------|
| `AuthService` | `service` | `getCurrentUser(session)`, `requireAuthenticated()` |

### Entities / Enums
| Class | Package | Vai trò |
|-------|---------|---------|
| `User` | `entity` | Entity hiển thị fullName, username, email, role, status |
| `UserRole` | `entity.enums` | Badge role (Admin / HR Manager / Interviewer / Candidate) |
| `UserStatus` | `entity.enums` | Kiểm tra trạng thái tài khoản |

### Repositories
| Class | Package | Vai trò |
|-------|---------|---------|
| `UserRepository` | `repository` | `findById()` – lấy user từ ID trong session |

### Config
| Class | Package | Vai trò |
|-------|---------|---------|
| `AuthInterceptor` | `config` | Chặn request nếu chưa đăng nhập → redirect SCR-01 |

---

## SCR-06 — HR Dashboard (`/dashboard`)

### Controllers
| Class | Package | Vai trò |
|-------|---------|---------|
| `HrDashboardController` | `controller` | GET `/dashboard`; yêu cầu role ADMIN hoặc HR_MANAGER |

### Services
| Class | Package | Vai trò |
|-------|---------|---------|
| `DashboardService` | `service` | `getRecruitmentSummary(currentUser)`, `getActiveJobRows(currentUser)` |
| `AuthService` | `service` | `getCurrentUser()`, `requireAnyRole(ADMIN, HR_MANAGER)` |

### DTOs
| Class | Package | Vai trò |
|-------|---------|---------|
| `RecruitmentSummary` | `dto` | 3 card: `activeJobCount`, `appliedCandidateCount`, `upcomingInterviewCount` |
| `ActiveJobRow` | `dto` | Mỗi hàng trong bảng job active: id, title, department, applicationCount, deadline |

### Entities / Enums
| Class | Package | Vai trò |
|-------|---------|---------|
| `User` | `entity` | Scope data theo `createdBy` (HR Manager chỉ thấy job của mình) |
| `JobPosting` | `entity` | Đếm & liệt kê job có status = ACTIVE |
| `Application` | `entity` | Đếm applications có status = APPLIED |
| `Interview` | `entity` | Đếm phỏng vấn SCHEDULED trong 7 ngày tới |
| `UserRole` | `entity.enums` | Kiểm tra HR_MANAGER để scope data |
| `JobStatus` | `entity.enums` | Lọc ACTIVE jobs |
| `ApplicationStatus` | `entity.enums` | Lọc APPLIED applications |
| `InterviewStatus` | `entity.enums` | Lọc SCHEDULED interviews |

### Repositories
| Class | Package | Vai trò |
|-------|---------|---------|
| `JobPostingRepository` | `repository` | Truy vấn job active, đếm theo `createdBy` |
| `ApplicationRepository` | `repository` | Đếm APPLIED applications |
| `InterviewRepository` | `repository` | Đếm upcoming interviews |

---

## SCR-07 — Admin Dashboard (`/admin/dashboard`)

### Controllers
| Class | Package | Vai trò |
|-------|---------|---------|
| `AdminDashboardController` | `controller` | GET `/admin/dashboard`; GET `/admin/activity-log` |

### Services
| Class | Package | Vai trò |
|-------|---------|---------|
| `DashboardService` | `service` | `getAdminDashboardData()`, `getRecentActivityEvents()` |
| `AuthService` | `service` | `requireRole(ADMIN)` |

### DTOs
| Class | Package | Vai trò |
|-------|---------|---------|
| `AdminDashboardData` | `dto` | Bọc `userCountByRole` (Map), `lockedAccountCount`, `recruitmentSummary` |
| `RecruitmentSummary` | `dto` | Nhúng vào AdminDashboardData, hiển thị tóm tắt tuyển dụng toàn hệ thống |

### Entities / Enums
| Class | Package | Vai trò |
|-------|---------|---------|
| `User` | `entity` | Đếm user theo role và status |
| `ActivityLog` | `entity` | Hiển thị trong bảng Recent Activity (10 log gần nhất) |
| `UserRole` | `entity.enums` | Key trong Map đếm user theo role |
| `UserStatus` | `entity.enums` | Đếm LOCKED accounts |
| `ActivityEventType` | `entity.enums` | Loại sự kiện trong activity log |
| `JobPosting` / `Application` / `Interview` | `entity` | Dùng trong `getRecruitmentSummary(null)` – hiển thị all HR Managers |
| `JobStatus` / `ApplicationStatus` / `InterviewStatus` | `entity.enums` | Filter trong recruitment summary |

### Views / Projections
| Class | Package | Vai trò |
|-------|---------|---------|
| `ActivityLogDisplayView` | `entity.view` | DB view hiển thị activity log với username và event type |

### Repositories
| Class | Package | Vai trò |
|-------|---------|---------|
| `UserRepository` | `repository` | `countByRole()`, `countByStatus()`, `countByRoleAndStatus()` |
| `ActivityLogDisplayViewRepository` | `repository` | `findTop10ByOrderByCreatedAtDesc()` |
| `JobPostingRepository` / `ApplicationRepository` / `InterviewRepository` | `repository` | Dùng trong `getRecruitmentSummary(null)` |

---

## SCR-08 — User Management (`/admin/users`)

### Controllers
| Class | Package | Vai trò |
|-------|---------|---------|
| `UserManagementController` | `controller` | GET list+filter; POST tạo user; POST `/{id}/unlock`; POST `/{id}/deactivate` |

### Services
| Class | Package | Vai trò |
|-------|---------|---------|
| `UserManagementService` | `service` | `searchUsers()`, `createUser()`, `unlockUser()`, `deactivateUser()`, `canUnlock()`, `canDeactivate()` |
| `AuthService` | `service` | `requireRole(ADMIN)`, `getCurrentUser()` |

### DTOs
| Class | Package | Vai trò |
|-------|---------|---------|
| `CreateUserForm` | `dto` | Form bean: fullName, username, email, password, role |

### Entities / Enums
| Class | Package | Vai trò |
|-------|---------|---------|
| `User` | `entity` | Entity chính: danh sách, tạo mới, cập nhật status |
| `ActivityLog` | `entity` | Ghi audit log sau mỗi thao tác Admin |
| `UserRole` | `entity.enums` | Chỉ HR_MANAGER và INTERVIEWER được tạo qua UI |
| `UserStatus` | `entity.enums` | Kiểm tra ACTIVE/LOCKED/INACTIVE để quyết định action |
| `ActivityEventType` | `entity.enums` | `ACCOUNT_CREATED`, `ACCOUNT_UNLOCKED`, `ACCOUNT_DEACTIVATED` |

### Repositories
| Class | Package | Vai trò |
|-------|---------|---------|
| `UserRepository` | `repository` | `searchUsers()`, `findByUsername()`, `findByEmail()`, `findById()`, `save()`, `countByRole()`, `countByRoleAndStatus()` |
| `ActivityLogRepository` | `repository` | `save()` – lưu audit log |

---

## Bảng tổng hợp tất cả Classes

| Class | SCR-05 | SCR-06 | SCR-07 | SCR-08 |
|-------|:------:|:------:|:------:|:------:|
| **CONTROLLERS** | | | | |
| `ProfileController` | ✅ | | | |
| `HrDashboardController` | | ✅ | | |
| `AdminDashboardController` | | | ✅ | |
| `UserManagementController` | | | | ✅ |
| **SERVICES** | | | | |
| `AuthService` | ✅ | ✅ | ✅ | ✅ |
| `DashboardService` | | ✅ | ✅ | |
| `UserManagementService` | | | | ✅ |
| **ENTITIES** | | | | |
| `User` | ✅ | ✅ | ✅ | ✅ |
| `ActivityLog` | | | ✅ | ✅ |
| `JobPosting` | | ✅ | ✅ | |
| `Application` | | ✅ | ✅ | |
| `Interview` | | ✅ | ✅ | |
| **ENUMS** | | | | |
| `UserRole` | ✅ | ✅ | ✅ | ✅ |
| `UserStatus` | ✅ | | ✅ | ✅ |
| `JobStatus` | | ✅ | ✅ | |
| `ApplicationStatus` | | ✅ | ✅ | |
| `InterviewStatus` | | ✅ | ✅ | |
| `ActivityEventType` | | | ✅ | ✅ |
| **DTOs** | | | | |
| `RecruitmentSummary` | | ✅ | ✅ | |
| `ActiveJobRow` | | ✅ | | |
| `AdminDashboardData` | | | ✅ | |
| `CreateUserForm` | | | | ✅ |
| **VIEWS** | | | | |
| `ActivityLogDisplayView` | | | ✅ | |
| **REPOSITORIES** | | | | |
| `UserRepository` | ✅ | | ✅ | ✅ |
| `ActivityLogRepository` | | | | ✅ |
| `ActivityLogDisplayViewRepository` | | | ✅ | |
| `JobPostingRepository` | | ✅ | ✅ | |
| `ApplicationRepository` | | ✅ | ✅ | |
| `InterviewRepository` | | ✅ | ✅ | |
| **CONFIG** | | | | |
| `AuthInterceptor` | ✅ | ✅ | ✅ | ✅ |
| `GlobalModelAdvice` | ✅ | ✅ | ✅ | ✅ |
