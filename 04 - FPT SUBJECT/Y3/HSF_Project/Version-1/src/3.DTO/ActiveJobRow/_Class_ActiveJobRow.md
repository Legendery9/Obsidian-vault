# 📝 Class: ActiveJobRow (DTO)

> [!abstract] Phân loại
> **Loại:** `DTO Class` — Đại diện một dòng trong bảng "Active Jobs" trên HR/Admin Dashboard.
> **Package:** `com.example.groupproject.dto`

---

## 📋 Fields (tất cả final, chuyển qua constructor)

| Field | Kiểu | Mô tả |
|-------|------|-------|
| `id` | `Integer` | ID của JobPosting |
| `title` | `String` | Tiêu đề job |
| `department` | `String` | Phòng ban |
| `applicationCount` | `long` | Số lượng đơn ứng tuyển (từ VIEW `v_job_application_counts`) |
| `deadline` | `LocalDate` | Hạn nộp hồ sơ (nullable) |

---

## 🔗 Sử dụng trong
- **`DashboardService.getActiveJobRows()`** → tạo từ `JobPosting` + `JobApplicationCountView`
- **`HrDashboardController`** → add `List<ActiveJobRow>` vào Model
- **`templates/hr/dashboard.html`** → hiển thị bảng Active Job Postings
