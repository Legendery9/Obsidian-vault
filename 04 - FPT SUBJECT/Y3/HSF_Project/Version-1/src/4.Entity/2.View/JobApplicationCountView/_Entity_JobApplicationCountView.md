# 🗄️ Entity (View): JobApplicationCountView

> [!abstract] Phân loại
> **Loại:** `View Entity` — Ánh xạ đến DB VIEW `v_job_application_counts`.
> **Package:** `com.example.groupproject.entity.view`
> **Annotation:** `@Entity @Immutable @Table(name = "v_job_application_counts")`

---

## 📄 DB View: `v_job_application_counts`

> [!info] Mục đích
> VIEW này tổng hợp số application theo từng trạng thái cho mỗi job. Thay cho việc query phức tạp trong Java code. Read-only (`@Immutable`).

## 📋 Fields

| Field | Column | Kiểu | Mô tả |
|-------|--------|------|-------|
| `jobId` | `job_id` | `Integer` | PK: ID của JobPosting |
| `total` | `total` | `Long` | Tổng số application |
| `applied` | `applied` | `Long` | Đơn ở trạng thái APPLIED |
| `screening` | `screening` | `Long` | Đơn ở trạng thái SCREENING |
| `interview` | `interview` | `Long` | Đơn ở trạng thái INTERVIEW |
| `offer` | `offer` | `Long` | Đơn ở trạng thái OFFER |
| `hired` | `hired` | `Long` | Đơn ở trạng thái HIRED |
| `rejected` | `rejected` | `Long` | Đơn ở trạng thái REJECTED |
| `withdrawn` | `withdrawn` | `Long` | Đơn ở trạng thái WITHDRAWN |

---

## 🔗 Dùng bởi
- `JobApplicationCountViewRepository.findAll()` → `DashboardService.getActiveJobRows()` → HR Dashboard table
