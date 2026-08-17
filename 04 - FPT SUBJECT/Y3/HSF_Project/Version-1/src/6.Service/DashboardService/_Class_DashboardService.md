# ⚙️ Class: DashboardService

> [!abstract] Phân loại
> **Loại:** `Service Class` — Tổng hợp dữ liệu thống kê cho Admin và HR Dashboard.
> **Package:** `com.example.groupproject.service`
> **Annotation:** `@Service @Transactional(readOnly = true)`

---

## 💉 Dependencies (Inject)

- `JobPostingRepository jobPostingRepository` — đếm/lấy job postings
- `ApplicationRepository applicationRepository` — đếm application theo status
- `InterviewRepository interviewRepository` — đếm upcoming interviews
- `JobApplicationCountViewRepository jobApplicationCountViewRepository` — số application theo job (từ VIEW)
- `UserRepository userRepository` — đếm users theo role/status
- `ActivityLogDisplayViewRepository activityLogDisplayViewRepository` — lấy activity log gần nhất (từ VIEW)

---

## 📊 Methods

### `getRecruitmentSummary(User currentUser)`

```java
public RecruitmentSummary getRecruitmentSummary(User currentUser)
```

**Logic scope:**
$$\text{scopeCreatedBy} = \begin{cases} \text{currentUser.id} & \text{if role = HR\_MANAGER} \\ \text{null} & \text{otherwise (ADMIN = xem tất cả)} \end{cases}$$

- Đếm: `activeJobs`, `appliedCandidates`, `upcomingInterviews` (7 ngày tới)
- **Return:** `RecruitmentSummary`

---

### `getActiveJobRows(User currentUser)`

```java
public List<ActiveJobRow> getActiveJobRows(User currentUser)
```

Lấy danh sách ACTIVE jobs, join với VIEW `v_job_application_counts` để đếm số application mỗi job. Map sang `ActiveJobRow` DTO.
- **Return:** `List<ActiveJobRow>`

---

### `getAdminDashboardData()`

```java
public AdminDashboardData getAdminDashboardData()
```

Tổng hợp dữ liệu cho Admin Dashboard:
- Đếm users theo từng role (Map<UserRole, Long>)
- Số tài khoản bị LOCKED
- `RecruitmentSummary` toàn hệ thống (null user = xem tất cả)
- **Return:** `AdminDashboardData`

---

### `getRecentActivityEvents()`

```java
public List<ActivityLogDisplayView> getRecentActivityEvents()
```

Lấy 10 sự kiện activity mới nhất từ VIEW `v_activity_log_display`.
- **Return:** `List<ActivityLogDisplayView>`
