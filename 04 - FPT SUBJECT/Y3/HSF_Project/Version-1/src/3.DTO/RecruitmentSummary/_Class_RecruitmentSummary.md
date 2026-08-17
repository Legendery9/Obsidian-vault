# 📝 Class: RecruitmentSummary (DTO)

> [!abstract] Phân loại
> **Loại:** `DTO Class` — Số liệu thống kê tuyển dụng cho dashboard.
> **Package:** `com.example.groupproject.dto`

---

## 📋 Fields

| Field | Kiểu | Mô tả |
|-------|------|-------|
| `activeJobCount` | `long` | Số job đang active |
| `appliedCandidateCount` | `long` | Số đơn ứng tuyển ở trạng thái APPLIED |
| `upcomingInterviewCount` | `long` | Số cuộc phỏng vấn trong 7 ngày tới |

---

## 🔗 Sử dụng trong
- **`DashboardService.getRecruitmentSummary()`** → tạo instance
- **`AdminDashboardData`** → chứa `RecruitmentSummary` để dùng trong Admin Dashboard
- **`HrDashboardController`** → add vào Model (`model.addAttribute("summary", ...)`)
- **`templates/hr/dashboard.html`** → `${summary.activeJobCount}`, `${summary.appliedCandidateCount}`, `${summary.upcomingInterviewCount}`
