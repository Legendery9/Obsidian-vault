# 📊 Phân Tích Schema TalentHub (MySQL)

> **Nguồn:** `talenthub_schema-mysql.sql`  
> **Hệ quản trị CSDL:** MySQL 8+  
> **Mô tả:** TalentHub Recruitment Management System

---

## 📋 Mục Lục

1. [CREATE DATABASE](#1-create-database)
2. [CREATE TABLE: users](#2-create-table-users)
3. [CREATE TABLE: password_reset_tokens](#3-create-table-password_reset_tokens)
4. [CREATE TABLE: job_postings](#4-create-table-job_postings)
5. [CREATE TABLE: applications](#5-create-table-applications)
6. [CREATE TABLE: application_notes](#6-create-table-application_notes)
7. [CREATE TABLE: interviews](#7-create-table-interviews)
8. [CREATE TABLE: activity_log](#8-create-table-activity_log)
9. [CREATE INDEX](#9-create-index)
10. [CREATE VIEW](#10-create-view)
11. [Sơ Đồ Quan Hệ](#11-so-do-quan-he)

---

## 1. CREATE DATABASE

```sql
CREATE DATABASE IF NOT EXISTS talenthub
    CHARACTER SET utf8mb4
    COLLATE utf8mb4_unicode_ci;
```

| Thuộc tính | Giá trị |
|---|---|
| Tên CSDL | `talenthub` |
| Character Set | `utf8mb4` (hỗ trợ Unicode đầy đủ, kể cả emoji) |
| Collation | `utf8mb4_unicode_ci` (so sánh chuỗi không phân biệt chữ hoa/thường) |

> **Lưu ý:** `IF NOT EXISTS` tránh lỗi nếu database đã tồn tại.

---

## 2. CREATE TABLE: `users`

```sql
CREATE TABLE users (
    id                  INT             AUTO_INCREMENT PRIMARY KEY,
    full_name           VARCHAR(255)    NOT NULL,
    username            VARCHAR(50)     NOT NULL UNIQUE,
    email               VARCHAR(255)    NOT NULL UNIQUE,
    password_hash       VARCHAR(255)    NOT NULL,
    role                VARCHAR(20)     NOT NULL,
    status              VARCHAR(20)     NOT NULL DEFAULT 'ACTIVE',
    failed_login_count  SMALLINT        NOT NULL DEFAULT 0,
    locked_at           TIMESTAMP(6)    NULL,
    created_at          TIMESTAMP(6)    NOT NULL DEFAULT CURRENT_TIMESTAMP(6),
    updated_at          TIMESTAMP(6)    NOT NULL DEFAULT CURRENT_TIMESTAMP(6) ON UPDATE CURRENT_TIMESTAMP(6),
    CONSTRAINT chk_users_role   CHECK (role IN ('ADMIN', 'HR_MANAGER', 'INTERVIEWER', 'CANDIDATE')),
    CONSTRAINT chk_users_status CHECK (status IN ('ACTIVE', 'LOCKED', 'INACTIVE')),
    CONSTRAINT chk_username_format CHECK (username REGEXP '^[A-Za-z0-9_]{4,50}$')
);
```

### Các Cột

| Cột | Kiểu dữ liệu | Ràng buộc | Mô tả |
|---|---|---|---|
| `id` | `INT` | `AUTO_INCREMENT PRIMARY KEY` | Khóa chính tự tăng |
| `full_name` | `VARCHAR(255)` | `NOT NULL` | Họ và tên đầy đủ |
| `username` | `VARCHAR(50)` | `NOT NULL UNIQUE` | Tên đăng nhập (duy nhất) |
| `email` | `VARCHAR(255)` | `NOT NULL UNIQUE` | Email (duy nhất) |
| `password_hash` | `VARCHAR(255)` | `NOT NULL` | Mật khẩu đã được hash |
| `role` | `VARCHAR(20)` | `NOT NULL` | Vai trò người dùng |
| `status` | `VARCHAR(20)` | `NOT NULL DEFAULT 'ACTIVE'` | Trạng thái tài khoản |
| `failed_login_count` | `SMALLINT` | `NOT NULL DEFAULT 0` | Số lần đăng nhập thất bại |
| `locked_at` | `TIMESTAMP(6)` | `NULL` | Thời điểm bị khóa tài khoản |
| `created_at` | `TIMESTAMP(6)` | `NOT NULL DEFAULT CURRENT_TIMESTAMP(6)` | Thời điểm tạo |
| `updated_at` | `TIMESTAMP(6)` | `NOT NULL DEFAULT CURRENT_TIMESTAMP(6) ON UPDATE` | Thời điểm cập nhật cuối |

### Constraints

| Tên Constraint | Loại | Quy tắc |
|---|---|---|
| `chk_users_role` | CHECK | `role` thuộc `{'ADMIN', 'HR_MANAGER', 'INTERVIEWER', 'CANDIDATE'}` |
| `chk_users_status` | CHECK | `status` thuộc `{'ACTIVE', 'LOCKED', 'INACTIVE'}` |
| `chk_username_format` | CHECK | `username` khớp regex `^[A-Za-z0-9_]{4,50}$` (4–50 ký tự, chỉ chữ/số/gạch dưới) |

---

## 3. CREATE TABLE: `password_reset_tokens`

```sql
CREATE TABLE password_reset_tokens (
    id          INT             AUTO_INCREMENT PRIMARY KEY,
    user_id     INT             NOT NULL,
    token       VARCHAR(255)    NOT NULL UNIQUE,
    expires_at  TIMESTAMP(6)    NOT NULL,
    used_at     TIMESTAMP(6)    NULL,
    created_at  TIMESTAMP(6)    NOT NULL DEFAULT CURRENT_TIMESTAMP(6),
    CONSTRAINT fk_prt_user FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

### Các Cột

| Cột | Kiểu dữ liệu | Ràng buộc | Mô tả |
|---|---|---|---|
| `id` | `INT` | `AUTO_INCREMENT PRIMARY KEY` | Khóa chính |
| `user_id` | `INT` | `NOT NULL` | FK → `users(id)` |
| `token` | `VARCHAR(255)` | `NOT NULL UNIQUE` | Token reset mật khẩu (duy nhất) |
| `expires_at` | `TIMESTAMP(6)` | `NOT NULL` | Thời điểm hết hạn token |
| `used_at` | `TIMESTAMP(6)` | `NULL` | Thời điểm token đã được sử dụng |
| `created_at` | `TIMESTAMP(6)` | `NOT NULL DEFAULT CURRENT_TIMESTAMP(6)` | Thời điểm tạo |

### Constraints

| Tên Constraint | Loại | Quy tắc |
|---|---|---|
| `fk_prt_user` | FOREIGN KEY | `user_id` → `users(id)` với `ON DELETE CASCADE` |

> **Lưu ý:** `ON DELETE CASCADE` — khi user bị xóa, tất cả token reset của họ cũng bị xóa theo.

---

## 4. CREATE TABLE: `job_postings`

```sql
CREATE TABLE job_postings (
    id                   INT             AUTO_INCREMENT PRIMARY KEY,
    title                VARCHAR(200)    NOT NULL,
    department           VARCHAR(100)    NOT NULL,
    location             VARCHAR(100)    NOT NULL,
    description          TEXT            NOT NULL,
    requirements         TEXT            NULL,
    salary_range         VARCHAR(100)    NULL,
    application_deadline DATE            NULL,
    status               VARCHAR(20)     NOT NULL DEFAULT 'DRAFT',
    created_by           INT             NOT NULL,
    created_at           TIMESTAMP(6)    NOT NULL DEFAULT CURRENT_TIMESTAMP(6),
    updated_at           TIMESTAMP(6)    NOT NULL DEFAULT CURRENT_TIMESTAMP(6) ON UPDATE CURRENT_TIMESTAMP(6),
    CONSTRAINT fk_jobs_created_by FOREIGN KEY (created_by) REFERENCES users(id),
    CONSTRAINT chk_jobs_status CHECK (status IN ('DRAFT', 'ACTIVE', 'CLOSED'))
);
```

### Các Cột

| Cột | Kiểu dữ liệu | Ràng buộc | Mô tả |
|---|---|---|---|
| `id` | `INT` | `AUTO_INCREMENT PRIMARY KEY` | Khóa chính |
| `title` | `VARCHAR(200)` | `NOT NULL` | Tiêu đề vị trí tuyển dụng |
| `department` | `VARCHAR(100)` | `NOT NULL` | Phòng/Ban |
| `location` | `VARCHAR(100)` | `NOT NULL` | Địa điểm làm việc |
| `description` | `TEXT` | `NOT NULL` | Mô tả công việc |
| `requirements` | `TEXT` | `NULL` | Yêu cầu ứng viên (tùy chọn) |
| `salary_range` | `VARCHAR(100)` | `NULL` | Khoảng lương (tùy chọn) |
| `application_deadline` | `DATE` | `NULL` | Hạn chót nộp hồ sơ |
| `status` | `VARCHAR(20)` | `NOT NULL DEFAULT 'DRAFT'` | Trạng thái tin tuyển dụng |
| `created_by` | `INT` | `NOT NULL` | FK → `users(id)` — người tạo |
| `created_at` | `TIMESTAMP(6)` | `NOT NULL DEFAULT CURRENT_TIMESTAMP(6)` | Thời điểm tạo |
| `updated_at` | `TIMESTAMP(6)` | `NOT NULL DEFAULT CURRENT_TIMESTAMP(6) ON UPDATE` | Thời điểm cập nhật |

### Constraints

| Tên Constraint | Loại | Quy tắc |
|---|---|---|
| `fk_jobs_created_by` | FOREIGN KEY | `created_by` → `users(id)` |
| `chk_jobs_status` | CHECK | `status` thuộc `{'DRAFT', 'ACTIVE', 'CLOSED'}` |

> **Lưu ý:** Việc kiểm tra `application_deadline >= CURDATE()` được thực hiện ở tầng ứng dụng vì MySQL CHECK không dùng được hàm `CURDATE()`.

---

## 5. CREATE TABLE: `applications`

```sql
CREATE TABLE applications (
    id                INT                 AUTO_INCREMENT PRIMARY KEY,
    job_id            INT                 NOT NULL,
    candidate_id      INT                 NOT NULL,
    cover_letter      TEXT                NULL,
    cv_filename       VARCHAR(255)        NOT NULL,
    cv_storage_path   VARCHAR(500)        NOT NULL,
    status            VARCHAR(20)         NOT NULL DEFAULT 'APPLIED',
    status_changed_at TIMESTAMP(6)        NOT NULL DEFAULT CURRENT_TIMESTAMP(6),
    submitted_at      TIMESTAMP(6)        NOT NULL DEFAULT CURRENT_TIMESTAMP(6),
    updated_at        TIMESTAMP(6)        NOT NULL DEFAULT CURRENT_TIMESTAMP(6) ON UPDATE CURRENT_TIMESTAMP(6),
    CONSTRAINT fk_apps_job       FOREIGN KEY (job_id)       REFERENCES job_postings(id),
    CONSTRAINT fk_apps_candidate FOREIGN KEY (candidate_id) REFERENCES users(id),
    CONSTRAINT uq_application    UNIQUE (job_id, candidate_id),
    CONSTRAINT chk_apps_status   CHECK (status IN (
        'APPLIED', 'SCREENING', 'INTERVIEW', 'OFFER', 'HIRED', 'REJECTED', 'WITHDRAWN'
    ))
);
```

### Các Cột

| Cột | Kiểu dữ liệu | Ràng buộc | Mô tả |
|---|---|---|---|
| `id` | `INT` | `AUTO_INCREMENT PRIMARY KEY` | Khóa chính |
| `job_id` | `INT` | `NOT NULL` | FK → `job_postings(id)` |
| `candidate_id` | `INT` | `NOT NULL` | FK → `users(id)` — ứng viên |
| `cover_letter` | `TEXT` | `NULL` | Thư xin việc (tùy chọn) |
| `cv_filename` | `VARCHAR(255)` | `NOT NULL` | Tên file CV |
| `cv_storage_path` | `VARCHAR(500)` | `NOT NULL` | Đường dẫn lưu trữ CV |
| `status` | `VARCHAR(20)` | `NOT NULL DEFAULT 'APPLIED'` | Trạng thái đơn ứng tuyển |
| `status_changed_at` | `TIMESTAMP(6)` | `NOT NULL DEFAULT CURRENT_TIMESTAMP(6)` | Thời điểm thay đổi trạng thái |
| `submitted_at` | `TIMESTAMP(6)` | `NOT NULL DEFAULT CURRENT_TIMESTAMP(6)` | Thời điểm nộp hồ sơ |
| `updated_at` | `TIMESTAMP(6)` | `NOT NULL DEFAULT CURRENT_TIMESTAMP(6) ON UPDATE` | Thời điểm cập nhật |

### Constraints

| Tên Constraint | Loại | Quy tắc |
|---|---|---|
| `fk_apps_job` | FOREIGN KEY | `job_id` → `job_postings(id)` |
| `fk_apps_candidate` | FOREIGN KEY | `candidate_id` → `users(id)` |
| `uq_application` | UNIQUE | `(job_id, candidate_id)` — mỗi ứng viên chỉ nộp 1 lần cho mỗi vị trí |
| `chk_apps_status` | CHECK | `status` thuộc `{'APPLIED', 'SCREENING', 'INTERVIEW', 'OFFER', 'HIRED', 'REJECTED', 'WITHDRAWN'}` |

### Vòng đời trạng thái đơn ứng tuyển

```
APPLIED → SCREENING → INTERVIEW → OFFER → HIRED
                                        ↘ REJECTED
                   ↘ REJECTED
         ↘ REJECTED
WITHDRAWN (bất kỳ giai đoạn nào)
```

---

## 6. CREATE TABLE: `application_notes`

```sql
CREATE TABLE application_notes (
    id              INT             AUTO_INCREMENT PRIMARY KEY,
    application_id  INT             NOT NULL,
    author_id       INT             NOT NULL,
    content         TEXT            NOT NULL,
    created_at      TIMESTAMP(6)    NOT NULL DEFAULT CURRENT_TIMESTAMP(6),
    CONSTRAINT fk_notes_application FOREIGN KEY (application_id) REFERENCES applications(id) ON DELETE CASCADE,
    CONSTRAINT fk_notes_author      FOREIGN KEY (author_id)      REFERENCES users(id)
);
```

### Các Cột

| Cột | Kiểu dữ liệu | Ràng buộc | Mô tả |
|---|---|---|---|
| `id` | `INT` | `AUTO_INCREMENT PRIMARY KEY` | Khóa chính |
| `application_id` | `INT` | `NOT NULL` | FK → `applications(id)` |
| `author_id` | `INT` | `NOT NULL` | FK → `users(id)` — người viết ghi chú |
| `content` | `TEXT` | `NOT NULL` | Nội dung ghi chú |
| `created_at` | `TIMESTAMP(6)` | `NOT NULL DEFAULT CURRENT_TIMESTAMP(6)` | Thời điểm tạo |

### Constraints

| Tên Constraint | Loại | Quy tắc |
|---|---|---|
| `fk_notes_application` | FOREIGN KEY | `application_id` → `applications(id)` với `ON DELETE CASCADE` |
| `fk_notes_author` | FOREIGN KEY | `author_id` → `users(id)` |

> **Lưu ý:** `ON DELETE CASCADE` — xóa đơn ứng tuyển thì xóa toàn bộ ghi chú liên quan.

---

## 7. CREATE TABLE: `interviews`

```sql
CREATE TABLE interviews (
    id                INT                 AUTO_INCREMENT PRIMARY KEY,
    application_id    INT                 NOT NULL,
    interviewer_id    INT                 NOT NULL,
    interview_date    DATE                NOT NULL,
    interview_time    TIME                NOT NULL,
    location_or_link  VARCHAR(500)        NULL,
    status            VARCHAR(20)         NOT NULL DEFAULT 'SCHEDULED',
    rating            SMALLINT            NULL,
    feedback          TEXT                NULL,
    evaluated_at      TIMESTAMP(6)        NULL,
    assigned_by       INT                 NOT NULL,
    created_at        TIMESTAMP(6)        NOT NULL DEFAULT CURRENT_TIMESTAMP(6),
    updated_at        TIMESTAMP(6)        NOT NULL DEFAULT CURRENT_TIMESTAMP(6) ON UPDATE CURRENT_TIMESTAMP(6),
    CONSTRAINT fk_interviews_application FOREIGN KEY (application_id) REFERENCES applications(id) ON DELETE CASCADE,
    CONSTRAINT fk_interviews_interviewer FOREIGN KEY (interviewer_id) REFERENCES users(id),
    CONSTRAINT fk_interviews_assigned_by FOREIGN KEY (assigned_by)    REFERENCES users(id),
    CONSTRAINT chk_interviews_status     CHECK (status IN ('SCHEDULED', 'EVALUATED')),
    CONSTRAINT chk_rating_range          CHECK (rating IS NULL OR (rating BETWEEN 1 AND 5)),
    CONSTRAINT chk_evaluated_fields      CHECK (
        status = 'SCHEDULED'
        OR (status = 'EVALUATED' AND rating IS NOT NULL AND feedback IS NOT NULL AND evaluated_at IS NOT NULL)
    )
);
```

### Các Cột

| Cột | Kiểu dữ liệu | Ràng buộc | Mô tả |
|---|---|---|---|
| `id` | `INT` | `AUTO_INCREMENT PRIMARY KEY` | Khóa chính |
| `application_id` | `INT` | `NOT NULL` | FK → `applications(id)` |
| `interviewer_id` | `INT` | `NOT NULL` | FK → `users(id)` — người phỏng vấn |
| `interview_date` | `DATE` | `NOT NULL` | Ngày phỏng vấn |
| `interview_time` | `TIME` | `NOT NULL` | Giờ phỏng vấn |
| `location_or_link` | `VARCHAR(500)` | `NULL` | Địa điểm hoặc link online (tùy chọn) |
| `status` | `VARCHAR(20)` | `NOT NULL DEFAULT 'SCHEDULED'` | Trạng thái buổi phỏng vấn |
| `rating` | `SMALLINT` | `NULL` | Điểm đánh giá (1–5) |
| `feedback` | `TEXT` | `NULL` | Nhận xét sau phỏng vấn |
| `evaluated_at` | `TIMESTAMP(6)` | `NULL` | Thời điểm đánh giá |
| `assigned_by` | `INT` | `NOT NULL` | FK → `users(id)` — người phân công |
| `created_at` | `TIMESTAMP(6)` | `NOT NULL DEFAULT CURRENT_TIMESTAMP(6)` | Thời điểm tạo |
| `updated_at` | `TIMESTAMP(6)` | `NOT NULL DEFAULT CURRENT_TIMESTAMP(6) ON UPDATE` | Thời điểm cập nhật |

### Constraints

| Tên Constraint | Loại | Quy tắc |
|---|---|---|
| `fk_interviews_application` | FOREIGN KEY | `application_id` → `applications(id)` với `ON DELETE CASCADE` |
| `fk_interviews_interviewer` | FOREIGN KEY | `interviewer_id` → `users(id)` |
| `fk_interviews_assigned_by` | FOREIGN KEY | `assigned_by` → `users(id)` |
| `chk_interviews_status` | CHECK | `status` thuộc `{'SCHEDULED', 'EVALUATED'}` |
| `chk_rating_range` | CHECK | `rating` là NULL hoặc từ 1 đến 5 |
| `chk_evaluated_fields` | CHECK | Nếu `status = 'EVALUATED'` thì `rating`, `feedback`, `evaluated_at` đều phải có giá trị |

> **Lưu ý:** `ON DELETE CASCADE` — xóa đơn ứng tuyển thì xóa toàn bộ lịch phỏng vấn liên quan.

---

## 8. CREATE TABLE: `activity_log`

```sql
CREATE TABLE activity_log (
    id              BIGINT              AUTO_INCREMENT PRIMARY KEY,
    actor_id        INT                 NULL,
    actor_username  VARCHAR(50)         NOT NULL,
    event_type      VARCHAR(50)         NOT NULL,
    description     TEXT                NULL,
    ip_address      VARCHAR(45)         NULL,
    created_at      TIMESTAMP(6)        NOT NULL DEFAULT CURRENT_TIMESTAMP(6),
    CONSTRAINT fk_log_actor        FOREIGN KEY (actor_id) REFERENCES users(id) ON DELETE SET NULL,
    CONSTRAINT chk_log_event_type  CHECK (event_type IN (
        'SIGN_IN_SUCCESS', 'SIGN_IN_FAILURE', 'ACCOUNT_CREATED', 'ACCOUNT_DEACTIVATED',
        'ACCOUNT_UNLOCKED', 'ACCOUNT_LOCKED', 'APPLICATION_STATUS_CHANGED',
        'CV_DOWNLOADED', 'EVALUATION_SUBMITTED'
    ))
);
```

### Các Cột

| Cột | Kiểu dữ liệu | Ràng buộc | Mô tả |
|---|---|---|---|
| `id` | `BIGINT` | `AUTO_INCREMENT PRIMARY KEY` | Khóa chính (BIGINT vì log có thể rất lớn) |
| `actor_id` | `INT` | `NULL` | FK → `users(id)` — người thực hiện hành động |
| `actor_username` | `VARCHAR(50)` | `NOT NULL` | Lưu username lại (phòng khi user bị xóa) |
| `event_type` | `VARCHAR(50)` | `NOT NULL` | Loại sự kiện |
| `description` | `TEXT` | `NULL` | Mô tả chi tiết sự kiện |
| `ip_address` | `VARCHAR(45)` | `NULL` | Địa chỉ IP (hỗ trợ cả IPv6 với 45 ký tự) |
| `created_at` | `TIMESTAMP(6)` | `NOT NULL DEFAULT CURRENT_TIMESTAMP(6)` | Thời điểm ghi log |

### Constraints

| Tên Constraint | Loại | Quy tắc |
|---|---|---|
| `fk_log_actor` | FOREIGN KEY | `actor_id` → `users(id)` với `ON DELETE SET NULL` |
| `chk_log_event_type` | CHECK | `event_type` thuộc danh sách 9 loại sự kiện |

### Các loại sự kiện được ghi log

| Event Type | Mô tả |
|---|---|
| `SIGN_IN_SUCCESS` | Đăng nhập thành công |
| `SIGN_IN_FAILURE` | Đăng nhập thất bại |
| `ACCOUNT_CREATED` | Tài khoản mới được tạo |
| `ACCOUNT_DEACTIVATED` | Tài khoản bị vô hiệu hóa |
| `ACCOUNT_UNLOCKED` | Tài khoản được mở khóa |
| `ACCOUNT_LOCKED` | Tài khoản bị khóa |
| `APPLICATION_STATUS_CHANGED` | Trạng thái đơn ứng tuyển thay đổi |
| `CV_DOWNLOADED` | CV được tải xuống |
| `EVALUATION_SUBMITTED` | Đánh giá phỏng vấn được nộp |

> **Lưu ý:** `ON DELETE SET NULL` — khi user bị xóa, `actor_id` trong log sẽ thành NULL nhưng `actor_username` vẫn còn, đảm bảo lịch sử không mất.

---

## 9. CREATE INDEX

Tổng cộng có **17 index** được tạo để tối ưu hiệu năng truy vấn.

### Index trên `users` (3 index)

| Index | Cột | Mục đích |
|---|---|---|
| `idx_users_role` | `role` | Lọc người dùng theo vai trò |
| `idx_users_status` | `status` | Lọc người dùng theo trạng thái |
| `idx_users_email` | `email` | Tìm kiếm nhanh theo email |

### Index trên `job_postings` (3 index)

| Index | Cột | Mục đích |
|---|---|---|
| `idx_jobs_status` | `status` | Lọc tin tuyển dụng theo trạng thái |
| `idx_jobs_created_by` | `created_by` | Lọc tin theo người tạo |
| `idx_jobs_department` | `department` | Lọc tin theo phòng ban |

### Index trên `applications` (4 index)

| Index | Cột | Mục đích |
|---|---|---|
| `idx_apps_job_id` | `job_id` | JOIN với job_postings |
| `idx_apps_candidate_id` | `candidate_id` | Tìm đơn của ứng viên |
| `idx_apps_status` | `status` | Lọc đơn theo trạng thái |
| `idx_apps_submitted_at` | `submitted_at` | Sắp xếp/lọc theo ngày nộp |

### Index trên `application_notes` (1 index)

| Index | Cột | Mục đích |
|---|---|---|
| `idx_notes_application_id` | `application_id` | Lấy ghi chú của một đơn |

### Index trên `interviews` (4 index)

| Index | Cột | Mục đích |
|---|---|---|
| `idx_interviews_app_id` | `application_id` | JOIN với applications |
| `idx_interviews_interviewer` | `interviewer_id` | Xem lịch của người phỏng vấn |
| `idx_interviews_status` | `status` | Lọc theo trạng thái |
| `idx_interviews_date` | `interview_date` | Lọc/sắp xếp theo ngày |

### Index trên `activity_log` (3 index)

| Index | Cột | Mục đích |
|---|---|---|
| `idx_log_event_type` | `event_type` | Lọc log theo loại sự kiện |
| `idx_log_actor_id` | `actor_id` | Xem hoạt động của người dùng |
| `idx_log_created_at` | `created_at DESC` | Xem log mới nhất trước (DESC) |

### Index trên `password_reset_tokens` (2 index)

| Index | Cột | Mục đích |
|---|---|---|
| `idx_prt_user_id` | `user_id` | Tìm token của user |
| `idx_prt_token` | `token` | Xác thực token (tra cứu nhanh) |

---

## 10. CREATE VIEW

Ba view được tạo để đơn giản hóa các truy vấn phổ biến.

### `v_job_application_counts`

```sql
CREATE VIEW v_job_application_counts AS
SELECT
    job_id,
    COUNT(*) AS total,
    SUM(CASE WHEN status = 'APPLIED'   THEN 1 ELSE 0 END) AS applied,
    SUM(CASE WHEN status = 'SCREENING' THEN 1 ELSE 0 END) AS screening,
    SUM(CASE WHEN status = 'INTERVIEW' THEN 1 ELSE 0 END) AS interview,
    SUM(CASE WHEN status = 'OFFER'     THEN 1 ELSE 0 END) AS offer,
    SUM(CASE WHEN status = 'HIRED'     THEN 1 ELSE 0 END) AS hired,
    SUM(CASE WHEN status = 'REJECTED'  THEN 1 ELSE 0 END) AS rejected,
    SUM(CASE WHEN status = 'WITHDRAWN' THEN 1 ELSE 0 END) AS withdrawn
FROM applications
GROUP BY job_id;
```

**Mục đích:** Thống kê số đơn ứng tuyển theo từng trạng thái cho mỗi vị trí tuyển dụng.

| Cột output | Mô tả |
|---|---|
| `job_id` | ID vị trí tuyển dụng |
| `total` | Tổng số đơn |
| `applied` | Số đơn đang ở trạng thái APPLIED |
| `screening` | Số đơn đang ở SCREENING |
| `interview` | Số đơn đang ở INTERVIEW |
| `offer` | Số đơn đang ở OFFER |
| `hired` | Số đơn đã HIRED |
| `rejected` | Số đơn đã REJECTED |
| `withdrawn` | Số đơn đã WITHDRAWN |

---

### `v_activity_log_display`

```sql
CREATE VIEW v_activity_log_display AS
SELECT
    al.id, al.actor_id, al.actor_username, al.event_type,
    al.description, al.ip_address, al.created_at,
    CASE
        WHEN u.status = 'INACTIVE' THEN CONCAT(al.actor_username, ' (deactivated)')
        ELSE al.actor_username
    END AS actor_display_name
FROM activity_log al
LEFT JOIN users u ON u.id = al.actor_id;
```

**Mục đích:** Hiển thị activity log với tên người dùng thân thiện — nếu tài khoản đã bị vô hiệu hóa, thêm nhãn `(deactivated)` vào tên.

| Cột output | Mô tả |
|---|---|
| `actor_display_name` | Tên hiển thị: `username` bình thường, hoặc `username (deactivated)` nếu tài khoản INACTIVE |

---

### `v_applications_with_days_in_stage`

```sql
CREATE VIEW v_applications_with_days_in_stage AS
SELECT
    a.*,
    TIMESTAMPDIFF(DAY, a.status_changed_at, NOW()) AS days_in_stage
FROM applications a;
```

**Mục đích:** Bổ sung cột `days_in_stage` — số ngày đơn ứng tuyển đã ở trạng thái hiện tại, dùng để theo dõi các đơn bị trì hoãn xử lý.

| Cột output | Mô tả |
|---|---|
| `a.*` | Toàn bộ cột từ `applications` |
| `days_in_stage` | Số ngày kể từ lần thay đổi trạng thái cuối cùng |

---

## 11. Sơ Đồ Quan Hệ

```
users (1) ─────────────────────────── (*) password_reset_tokens
  │                                         (ON DELETE CASCADE)
  │ (created_by)
  │
  └──(1)──────────────── (*) job_postings
                                │
                                │ (job_id)
                                │
                   users (1) ───┴──── (*) applications ──── (*) application_notes
                   (candidate_id)           │                    (ON DELETE CASCADE)
                                            │
                                            └── (*) interviews
                                                    │
                                            users (interviewer_id)
                                            users (assigned_by)

users (actor_id) ──── (*) activity_log
                           (ON DELETE SET NULL)
```

### Tóm tắt quan hệ

| Bảng | Phụ thuộc vào | Loại quan hệ |
|---|---|---|
| `password_reset_tokens` | `users` | N:1 |
| `job_postings` | `users` (created_by) | N:1 |
| `applications` | `job_postings`, `users` (candidate) | N:1, N:1 |
| `application_notes` | `applications`, `users` (author) | N:1, N:1 |
| `interviews` | `applications`, `users` x2 | N:1, N:1, N:1 |
| `activity_log` | `users` (actor, nullable) | N:1 |

---

*Tài liệu được tạo tự động từ `talenthub_schema-mysql.sql` — TalentHub Recruitment Management System*
