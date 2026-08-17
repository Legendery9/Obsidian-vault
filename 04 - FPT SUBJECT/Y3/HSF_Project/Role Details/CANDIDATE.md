# 4️⃣ CANDIDATE — Ứng Viên

> [!abstract] Tổng Quan Vai Trò
> **Tên vai trò:** $Role_{CANDIDATE}$
> **Phạm vi:** Cá nhân
>
> Ứng viên là người dùng cuối, tự đăng ký tài khoản, có thể duyệt danh sách công việc, nộp đơn ứng tuyển và theo dõi tiến trình ứng tuyển của riêng mình.

---

## 🧩 Đặc Điểm

- 📄 **Ứng tuyển** công việc công khai
- 🌐 Xem **danh sách job** công khai
- 📤 **Nộp CV** và đơn ứng tuyển
- 📊 **Theo dõi trạng thái** ứng tuyển của bản thân

---

## 🛣️ Truy Cập (Routes)

> [!info] Danh Sách Route $P_{CANDIDATE}$
>
> | Method | Endpoint | Chức năng |
> |--------|----------|-----------|
> | `GET`  | `/jobs` | Danh sách job công khai (có filter) |
> | `GET`  | `/jobs/{id}` | Chi tiết job + form apply |
> | `POST` | `/jobs/{id}/apply` | Nộp đơn ứng tuyển |
> | `GET`  | `/candidate/applications` | Danh sách ứng tuyển của mình |
> | `POST` | `/candidate/applications/{id}/withdraw` | Rút đơn ứng tuyển |
> | `GET`  | `/profile` | Xem profile cá nhân |
> | `GET`  | `/change-password` | Đổi mật khẩu |

---

## ✅ Quyền Chi Tiết

- ✅ Xem danh sách công việc đang tuyển (`PUBLIC`)
- ✅ Lọc job theo `department` / `location`
- ✅ Nộp **CV** + **cover letter** cho job
- ✅ Xem **lịch sử ứng tuyển** cá nhân
- ✅ Lọc ứng tuyển theo trạng thái: `APPLIED`, `SCREENING`, `INTERVIEW`, `OFFER`, `HIRED`, `REJECTED`, `WITHDRAWN`
- ✅ **Rút đơn** ứng tuyển (nếu chưa qua stage nào)
- ✅ Xem **trạng thái ứng tuyển** real-time
- ❌ **Không** xem ứng tuyển của candidate khác
- ❌ **Không** quản lý job posting
- ❌ **Không** xem bất kỳ user khác (ngoài chính mình)
- ❌ **Không** xem lịch phỏng vấn (HR sẽ notify qua email)

---

## 🔄 Quy Trình Ứng Tuyển

> [!note] Luồng Trạng Thái Ứng Tuyển
> Trạng thái ứng tuyển của $CANDIDATE$ thay đổi theo quy trình tuyển dụng:

$$
APPLIED \xrightarrow{\text{HR review CV}} SCREENING \xrightarrow{\text{phỏng vấn}} INTERVIEW \xrightarrow{\text{được offer}} OFFER \xrightarrow{\text{nhận việc}} HIRED
$$

> Hoặc kết thúc sớm:
$$
\text{Bất kỳ stage} \rightarrow REJECTED \quad \text{hoặc} \quad WITHDRAWN
$$

---

## 📋 Form Ứng Tuyển

> [!info] Các Tham Số Form $F_{apply}$
>
> | Tham số | Kiểu | Mô tả |
> |---------|------|-------|
> | `job_id` | `Long` | ID công việc ứng tuyển |
> | `candidate_id` | `Long` | ID ứng viên *(lấy từ session)* |
> | `cv_filename` | `String` | Tên file CV |
> | `cv_storage_path` | `String` | Đường dẫn lưu CV trên server |
> | `cover_letter` | `String` | Thư xin việc *(tuỳ chọn)* |
> | `status` | `Enum` | Mặc định: `APPLIED` |

> [!warning] Lưu Ý Quan Trọng
> - Candidate chỉ được **rút đơn** khi trạng thái vẫn là `APPLIED` hoặc `SCREENING`.
> - Sau khi đã vào giai đoạn `INTERVIEW`, việc rút đơn cần có **xác nhận từ HR**.
> - Thông tin phỏng vấn **không hiển thị** trên giao diện candidate — chỉ gửi qua **email**.