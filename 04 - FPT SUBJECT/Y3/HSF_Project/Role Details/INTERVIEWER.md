# 3️⃣ INTERVIEWER — Người Phỏng Vấn

> [!abstract] Tổng Quan Vai Trò
> **Tên vai trò:** $Role_{INTERVIEWER}$
> **Phạm vi:** Phỏng vấn ứng viên
>
> Interviewer là người được **HR / Admin giao** lịch phỏng vấn. Có thể xem thông tin ứng viên, thực hiện đánh giá và viết feedback — nhưng **không can thiệp** vào quy trình tuyển dụng tổng thể.

---

## 🧩 Đặc Điểm

- 📅 Chịu trách nhiệm thực hiện **phỏng vấn ứng viên**
- 🗓️ Quản lý **lịch phỏng vấn** của chính mình
- ⭐ **Đánh giá** ứng viên sau phỏng vấn
- 🚫 **Không can thiệp** vào các quy trình tuyển dụng khác

---

## 🛣️ Truy Cập (Routes)

> [!info] Danh Sách Route $P_{INTERVIEWER}$
>
> | Method | Endpoint | Chức năng |
> |--------|----------|-----------|
> | `GET`  | `/interviews` | Danh sách phỏng vấn được giao |
> | `GET`  | `/interviews/{id}` | Chi tiết phỏng vấn |
> | `POST` | `/interviews/{id}/evaluate` | Đánh giá ứng viên (rating, feedback) |
> | `GET`  | `/profile` | Xem profile cá nhân |

---

## ✅ Quyền Chi Tiết

- ✅ Xem **danh sách phỏng vấn** được giao bởi HR / Admin
- ✅ Cập nhật trạng thái phỏng vấn: `SCHEDULED` → `EVALUATED`
- ✅ Nhập **điểm đánh giá** ($rating \in [1, 5]$)
- ✅ Viết **feedback** nhận xét cho ứng viên
- ✅ Xem **thông tin ứng viên** & job posting liên quan
- ❌ **Không** tạo / xóa phỏng vấn *(do $ADMIN$ / $HR\_MANAGER$ tạo)*
- ❌ **Không** quản lý user
- ❌ **Không** quản lý job posting
- ❌ **Không** xem ứng viên của công việc khác

---

## 📋 Dữ Liệu Phỏng Vấn

> [!info] Các Tham Số $D_{interview}$
>
> | Tham số | Kiểu | Mô tả |
> |---------|------|-------|
> | `interview_date` | `Date` | Ngày phỏng vấn |
> | `interview_time` | `Time` | Giờ phỏng vấn |
> | `location_or_link` | `String` | Địa điểm hoặc link Zoom |
> | `status` | `Enum` | `SCHEDULED` \| `EVALUATED` |
> | `rating` | `Integer` | Điểm đánh giá: $rating \in [1, 5]$ sao |
> | `feedback` | `String` | Nhận xét chi tiết về ứng viên |
> | `evaluated_at` | `Timestamp` | Thời gian hoàn thành đánh giá |

> [!warning] Lưu Ý Quan Trọng
> - Chỉ có thể submit đánh giá **một lần** sau khi phỏng vấn.
> - Sau khi trạng thái chuyển thành `EVALUATED`, **không thể chỉnh sửa** rating hoặc feedback.
> - Interviewer chỉ thấy **phỏng vấn được giao cho mình** — không thể xem phỏng vấn của người khác.

> [!note] Ví Dụ Kịch Bản Sử Dụng
> **Scenario:** Interviewer hoàn thành buổi phỏng vấn và gửi đánh giá.
> 1. Truy cập `GET /interviews` → xem lịch phỏng vấn hôm nay
> 2. Chọn `GET /interviews/15` → xem thông tin ứng viên & job
> 3. Sau phỏng vấn: `POST /interviews/15/evaluate`
>    - `rating = 4`, `feedback = "Ứng viên tốt, cần cải thiện kỹ năng SQL"`
> 4. Trạng thái cập nhật: `SCHEDULED` → `EVALUATED` ✅