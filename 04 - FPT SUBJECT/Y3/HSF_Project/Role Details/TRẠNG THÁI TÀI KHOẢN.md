# 📋 TRẠNG THÁI TÀI KHOẢN — UserStatus

> [!abstract] Tổng Quan
> Hệ thống HSF sử dụng enum $UserStatus$ để kiểm soát trạng thái hoạt động của tài khoản người dùng.
> Mỗi trạng thái quyết định khả năng đăng nhập và sử dụng hệ thống của người dùng.

---

## 🔢 Các Trạng Thái

> [!info] Enum $UserStatus$
>
> | Trạng thái | Ý nghĩa |
> |-----------|---------|
> | `ACTIVE` | Tài khoản **hoạt động bình thường** — có thể đăng nhập |
> | `LOCKED` | Tài khoản bị **khóa vĩnh viễn** bởi quản trị viên |
> | `INACTIVE` | Tài khoản **chưa xác minh email** / chưa được kích hoạt |

```java
public enum UserStatus {
    ACTIVE,     // Tài khoản hoạt động bình thường
    LOCKED,     // Khóa vĩnh viễn (quản trị viên)
    INACTIVE    // Chưa xác minh email / kích hoạt
}
```

---

## 🔄 Chuyển Trạng Thái

### Luồng $CANDIDATE$ (Tự đăng ký)

$$
Register \xrightarrow{\text{chờ xác minh}} INACTIVE \xrightarrow{\text{nhấn link verify}} ACTIVE \xrightarrow{\text{Admin deactivate}} LOCKED
$$

### Luồng $HR\_MANAGER$ / $INTERVIEWER$ (Tạo bởi Admin)

$$
\text{Admin tạo tài khoản} \xrightarrow{\text{trực tiếp}} ACTIVE \xrightarrow{\text{Admin deactivate}} LOCKED
$$

> [!warning] Lưu Ý Về Trạng Thái
> - `LOCKED` là trạng thái **vĩnh viễn** — chỉ $ADMIN$ mới có thể unlock.
> - `INACTIVE` chỉ áp dụng cho $CANDIDATE$ tự đăng ký — **không tự động** chuyển sang `ACTIVE`.
> - $HR\_MANAGER$ và $INTERVIEWER$ do Admin tạo sẽ có trạng thái `ACTIVE` **ngay lập tức**.

---

## 🔐 Kiểm Tra Khi Đăng Nhập

> [!warning] Logic Xác Thực Bắt Buộc
> Mọi yêu cầu đăng nhập **phải** kiểm tra $UserStatus$ trước khi cấp quyền truy cập. Bỏ sót bước này có thể cho phép tài khoản bị khóa đăng nhập trái phép.

```java
if (user.getStatus() == UserStatus.LOCKED) {
    throw new AdminLockedException("Tài khoản đã bị quản trị viên khóa");
}

if (user.getStatus() == UserStatus.INACTIVE) {
    throw new IllegalStateException("Tài khoản chưa được kích hoạt");
}
```

> [!note] Ví Dụ Kịch Bản
> **Scenario:** Candidate đăng ký nhưng quên xác minh email.
> - Trạng thái: `INACTIVE`
> - Khi đăng nhập → hệ thống ném `IllegalStateException`
> - Giải pháp: Gửi lại email xác minh → Candidate nhấn link → Trạng thái → `ACTIVE` ✅