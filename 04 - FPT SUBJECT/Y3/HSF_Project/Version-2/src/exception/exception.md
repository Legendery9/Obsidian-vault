# Package: exception

> [!abstract]
> Package `exception` chứa các **Custom Exception class** để biểu diễn các lỗi business logic cụ thể. Thay vì throw `Exception` generic, dự án định nghĩa các exception có tên rõ ràng để Controller có thể bắt và xử lý từng trường hợp một cách tường minh.

---

## 📄 Danh sách Exceptions

### `AccountLockedException.java`
> [!info]
> **Khi nào throw:** User đăng nhập sai quá **5 lần liên tiếp** → tài khoản bị khóa tự động (`status = LOCKED`).
>
> **Nơi throw:** `AuthService.login()` — khi `failedLoginCount >= 5`
>
> **Nơi catch:** `LoginController.loginUser()`:
> ```java
> } catch (AccountLockedException e) {
>     return "redirect:/login?error=locked";
> }
> ```
> → Redirect về trang login với banner thông báo tài khoản bị khóa.

---

### `AdminLockedException.java`
> [!info]
> **Khi nào throw:** Tài khoản **ADMIN** bị admin khác deactivate/lock (edge case đặc biệt, xử lý riêng để phân biệt với user thông thường bị khóa).
>
> **Nơi throw:** `AuthService.login()` — khi role là `ADMIN` và status không phải `ACTIVE`
>
> **Nơi catch:** `LoginController.loginUser()`:
> ```java
> } catch (AdminLockedException e) {
>     return "auth/admin-locked-page";
> }
> ```
> → Render trang HTML riêng biệt thay vì redirect (UX khác với user thông thường).

---

## 🔄 Flow xử lý Exception trong Login

```
POST /login
    ↓
AuthService.login(dto, session)
    ├── Sai password (< 5 lần) → throw IllegalArgumentException
    │       ↓ catch → redirect:/login?error=generic
    │
    ├── Sai password (≥ 5 lần) → status=LOCKED → throw AccountLockedException
    │       ↓ catch → redirect:/login?error=locked
    │
    ├── Admin bị khóa → throw AdminLockedException
    │       ↓ catch → render auth/admin-locked-page
    │
    └── Status INACTIVE → throw IllegalStateException
            ↓ catch → redirect:/login?error=status
```

> [!warning]
> Hai exception này kế thừa `RuntimeException` (unchecked) — không cần khai báo `throws` ở method signature.
