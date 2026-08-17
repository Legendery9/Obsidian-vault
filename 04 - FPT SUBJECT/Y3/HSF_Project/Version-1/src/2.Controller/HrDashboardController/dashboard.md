# 🎮 Method: dashboard (GET /hr/dashboard)

> [!abstract] Phân loại
> **Class:** `HrDashboardController` | **Loại:** `Controller Method` — HR/Admin GET handler
> **Package:** `com.example.groupproject.controller`
> **Base mapping:** `@RequestMapping("/hr")`

## 🗺️ Ánh xạ
- **HTTP Method:** `GET`
- **URL:** `/hr/dashboard`
- **Trả về view:** `hr/dashboard`
- **Quyền truy cập:** `ADMIN` hoặc `HR_MANAGER`

## 🎯 Tác dụng
Hiển thị trang HR Dashboard với:
- Thống kê tuyển dụng (scoped theo HR Manager nếu không phải ADMIN)
- Danh sách Active Job Postings

> [!note] Scoping theo role
> Nếu user là `HR_MANAGER` → chỉ xem data của job do mình tạo.
> Nếu user là `ADMIN` → xem tất cả job trong hệ thống.

## 💉 Dependencies
- `DashboardService dashboardService` — lấy summary và active jobs (có scope)
- `AuthService authService` — kiểm tra role ADMIN hoặc HR_MANAGER

## 📥 Parameters & 📤 Return

```java
public String dashboard(Model model, HttpSession session)
// Return: "hr/dashboard"
```

**Model attributes được add:**
- `summary` → `RecruitmentSummary` (activeJobCount, appliedCandidateCount, upcomingInterviewCount)
- `activeJobs` → `List<ActiveJobRow>` (danh sách job đang active)

**Return:** `String` — `"hr/dashboard"`
