# 🏢 TalentHub — Recruitment Management System

> [!abstract] Tổng quan dự án
> **Tên ứng dụng:** GroupProject — TalentHub Recruitment Management System
> **Framework:** Spring Boot 3.5.0 | **Java:** 21 | **Database:** MySQL
> **Server Port:** `10111` | **URL:** `http://localhost:10111`
> **Template Engine:** Thymeleaf | **Build:** Maven

---

## 📁 Cấu trúc Obsidian Vault này

```
HSF_Project/
├── README.md                  ← File này (mục lục dự án)
├── AppConfig/
│   ├── application-properties.md  ← Giải thích file cấu hình
│   └── pom-dependencies.md        ← Giải thích các dependency Maven
├── src/
│   ├── [Entity Classes]
│   │   ├── User/
│   │   ├── JobPosting/
│   │   ├── Application/
│   │   ├── Interview/
│   │   ├── ActivityLog/
│   │   └── PasswordResetToken/
│   ├── [Enum Classes]
│   │   ├── UserRole/
│   │   ├── UserStatus/
│   │   ├── JobStatus/
│   │   ├── ApplicationStatus/
│   │   └── ActivityEventType/
│   ├── [View Entities]
│   │   ├── ActivityLogDisplayView/
│   │   └── JobApplicationCountView/
│   ├── [Controllers]
│   │   ├── LoginController/
│   │   ├── AdminDashboardController/
│   │   ├── HrDashboardController/
│   │   ├── ProfileController/
│   │   └── JobController/
│   │       └── UserManagementController/
│   ├── [Services]
│   │   ├── AuthService/
│   │   ├── DashboardService/
│   │   ├── UserManagementService/
│   │   └── UserService/
│   ├── [Repositories]
│   │   ├── UserRepository/
│   │   ├── JobPostingRepository/
│   │   ├── ApplicationRepository/
│   │   ├── InterviewRepository/
│   │   ├── ActivityLogRepository/
│   │   ├── ActivityLogDisplayViewRepository/
│   │   └── JobApplicationCountViewRepository/
│   ├── [Config]
│   │   ├── AuthInterceptor/
│   │   ├── WebMvcConfig/
│   │   ├── GlobalModelAdvice/
│   │   └── DataInitializer/
│   ├── [DTOs]
│   │   ├── CreateUserForm/
│   │   ├── AdminDashboardData/
│   │   ├── RecruitmentSummary/
│   │   └── ActiveJobRow/
│   └── GroupProjectApplication/
└── template/
    ├── login/
    ├── profile/
    ├── change-password/
    ├── fragments/
    ├── admin/
    ├── hr/
    └── jobs/
```

---

## 🏷️ Kiến trúc tổng thể

```
Browser → Thymeleaf Template
         ↓ (render by)
    Controller (@Controller)
         ↓ (inject & call)
    Service (@Service)
         ↓ (inject & call)
    Repository (@Repository / JpaRepository)
         ↓ (JPA / Hibernate)
    Database (MySQL - talenthub schema)
```

---

## 🗄️ Các bảng Database

| Bảng | Entity Class | Mô tả |
|------|-------------|-------|
| `users` | `User` | Tài khoản người dùng |
| `job_postings` | `JobPosting` | Tin tuyển dụng |
| `applications` | `Application` | Đơn ứng tuyển |
| `interviews` | `Interview` | Lịch phỏng vấn |
| `activity_log` | `ActivityLog` | Nhật ký hoạt động |
| `password_reset_tokens` | `PasswordResetToken` | Token đặt lại mật khẩu |

**DB Views:**

| View                       | Entity                    | Mô tả                          |
| -------------------------- | ------------------------- | ------------------------------ |
| `v_activity_log_display`   | `ActivityLogDisplayView`  | Log kèm tên người dùng         |
| `v_job_application_counts` | `JobApplicationCountView` | Số đơn theo trạng thái mỗi job |

---

## 🔐 Hệ thống phân quyền (URL-based, không dùng Spring Security)

| URL Pattern | Role yêu cầu |
|-------------|---------------|
| `/login`, `/css/**`, `/js/**` | Public |
| `/profile`, `/change-password` | Bất kỳ user đã đăng nhập |
| `/hr/**`, `/jobs/**` | ADMIN, HR_MANAGER |
| `/admin/**` | ADMIN only |

> [!note] Tài khoản Admin mặc định
> `username: admin` | `password: Admin@123` — tự động tạo bởi `DataInitializer` nếu chưa có ADMIN nào trong DB.
