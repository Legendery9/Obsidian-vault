# 2️⃣ HrDashboardController — `/hr/**`

> [!abstract]
> Controller cho **HR Dashboard**, quản lý **Application pipeline** theo từng job, và **Pipeline Report**. Phục vụ cả `ADMIN` lẫn `HR_MANAGER`. Hỗ trợ **HTMX** cho phép cập nhật danh sách ứng viên mà không cần reload toàn trang.

---

## 📌 Endpoints

### `GET /hr/dashboard`

```
Request → HrDashboardController.dashboard()
    ↓
AuthService.getCurrentUser(session)
    ↓
AuthService.requireAnyRole(user, ADMIN, HR_MANAGER)   ← ADMIN hoặc HR_MANAGER
    ↓
DashboardService.getRecruitmentSummary(currentUser)
    └── Trả về RecruitmentSummary:
        ├── activeJobCount    — Số job đang ACTIVE
        ├── totalApplications — Tổng đơn ứng tuyển
        ├── pendingInterviews — Phỏng vấn đang chờ
        └── hiredCount        — Đã tuyển thành công
    ↓
DashboardService.getActiveJobRows(currentUser)
    └── Danh sách ActiveJobRow (job ACTIVE của user này nếu HR_MANAGER,
        hoặc tất cả nếu ADMIN)
    ↓
model.addAttribute("summary", ...)
model.addAttribute("activeJobs", ...)
    ↓
return "hr/dashboard"
```

---

### `GET /hr/jobs/{jobId}/applications`

```
Request (với optional filter) → HrDashboardController.getApplications()
    │
    ├── @PathVariable jobId        — ID của job posting
    ├── @RequestParam status       (default="ALL") — Filter theo ApplicationStatus
    └── @RequestHeader HX-Request  (boolean) — Phát hiện HTMX request
    ↓
AuthService.requireAnyRole(user, ADMIN, HR_MANAGER)
    ↓
JobService.getJobById(jobId)
    └── job == null? → redirect:/hr/dashboard
    ↓
ApplicationService.getApplicationsForJob(jobId, status, currentUser)
    └── Trả về List<Application> đã filter theo status
        (status="ALL" → lấy tất cả)
    ↓
ApplicationService.getApplicationCountsByStage(jobId)
    └── Map<String, Long>:
        ├── "APPLIED"    → số đơn
        ├── "SCREENING"  → số đơn
        ├── "INTERVIEW"  → số đơn
        ├── "OFFER"      → số đơn
        ├── "HIRED"      → số đơn
        └── "REJECTED"   → số đơn
    ↓
model.addAttribute("job", ...)
model.addAttribute("applications", ...)
model.addAttribute("counts", ...)
model.addAttribute("currentStatus", status.toUpperCase())
    ↓
if (hxRequest)
    └── return "hr/applications :: applicantList"  ← HTMX: chỉ trả fragment
else
    └── return "hr/applications"                    ← Full page load
```

> [!info]
> **HTMX Integration:** Khi user click tab filter status, browser gửi request với header `HX-Request: true`. Controller phát hiện và trả về **chỉ phần fragment** `applicantList` thay vì reload toàn trang — UX mượt mà như SPA.

---

### `GET /hr/report/{jobId}`

```
Request → HrDashboardController.showPipelineReport()
    │
    └── @PathVariable jobId
    ↓
ApplicationRepository.countApplicationsByStatusAndJobId(jobId)
    └── List<Object[]> — [status, count] cho mỗi trạng thái
    ↓
ApplicationRepository.findByJobId(jobId)
    └── List<Application> — tất cả đơn của job này
    ↓
model.addAttribute("statusCounts", ...)
model.addAttribute("applications", ...)
    ↓
return "hr/report"
```

> [!warning]
> Method `showPipelineReport()` **không kiểm tra quyền** (`requireAnyRole`) — dựa hoàn toàn vào `AuthInterceptor` chặn `/hr/**`. Nếu sau này thêm endpoint công khai trong `/hr/`, cần chú ý thêm kiểm tra quyền thủ công.

---

## ⚙️ Dependencies

| Dependency | Mục đích |
|---|---|
| `AuthService` | Lấy user từ session, validate quyền |
| `DashboardService` | Dữ liệu dashboard tổng hợp |
| `ApplicationService` | Lấy & filter application |
| `JobService` | Validate job tồn tại |
| `ApplicationRepository` | Truy vấn trực tiếp cho report |

---

## 📝 Key Responsibilities

- **Recruitment pipeline overview** — tổng quan tuyển dụng
- **Application management by status** — quản lý đơn theo từng stage
- **Real-time HTMX fragment updates** — filter không reload trang
- **Pipeline analytics** — báo cáo phân phối đơn theo trạng thái