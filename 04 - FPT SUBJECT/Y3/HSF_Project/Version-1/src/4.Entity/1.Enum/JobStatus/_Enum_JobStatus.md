# 🏷️ Enum: JobStatus

> [!abstract] Phân loại
> **Loại:** `Enum` — Trạng thái tin tuyển dụng.
> **Package:** `com.example.groupproject.entity.enums`

---

## 📋 Các giá trị

| Value | Mô tả |
|-------|--------|
| `DRAFT` | Tin đang soạn thảo, chưa công bố. Giá trị mặc định khi tạo. |
| `ACTIVE` | Tin đang được đăng tuyển, chấp nhận ứng tuyển. |
| `CLOSED` | Tin đã đóng, không nhận thêm ứng viên. |

> [!note] Dùng trong
> `JobPosting.status`, `JobPostingRepository.countByStatus()`, `JobPostingRepository.findActiveJobs()`, `DashboardService`
