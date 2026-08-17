# 🎨 Template: hr/dashboard.html

> [!abstract] Tổng quan
> **Đường dẫn:** `src/main/resources/templates/hr/dashboard.html`
> **Controller:** `HrDashboardController.dashboard()` (GET /hr/dashboard)
> **Vai trò:** Trang tổng quan tuyển dụng dành cho HR Manager và Admin.

---

## 🧩 Phân đoạn chính

### 1. Stats Grid
```html
<div class="stats-grid">
    <div class="stat-card">
        <div class="value" th:text="${summary.activeJobCount}">0</div>
        <div class="label">Active Jobs</div>
    </div>
    <div class="stat-card">
        <div class="value" th:text="${summary.appliedCandidateCount}">0</div>
        <div class="label">Applied Candidates</div>
    </div>
    <div class="stat-card">
        <div class="value" th:text="${summary.upcomingInterviewCount}">0</div>
        <div class="label">Interviews (7 days)</div>
    </div>
</div>
```
3 thừb thống kê: số job active, số ứng viên, số phỏng vấn sắp tới. Nếu user là HR_MANAGER thì chỉ hiển số liệu của job mình tạo.

### 2. Active Job Postings Table
```html
<table>
    <tr th:each="job : ${activeJobs}">
        <td th:text="${job.title}">Software Engineer</td>
        <td th:text="${job.department}">Engineering</td>
        <td th:text="${job.applicationCount}">5</td>
        <td th:text="${job.deadline != null ? #temporals.format(job.deadline, 'dd MMM yyyy') : '\u2014'}">\u2014</td>
    </tr>
</table>
```
- Danh sách Active Jobs với số lượng application
- Deadline hiển thị `\u2014` nếu null
- Nút **Create New Job** → `/jobs/new`

---

## 🔗 Model Variables

| Variable | Kiểu | Nguồn |
|----------|-------|--------|
| `summary` | `RecruitmentSummary` | `HrDashboardController` |
| `activeJobs` | `List<ActiveJobRow>` | `HrDashboardController` |
