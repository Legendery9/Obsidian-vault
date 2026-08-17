# 4️⃣ ProfileController — `/profile`

> [!abstract]
> Controller đơn giản nhất trong hệ thống — hiển thị trang hồ sơ cá nhân. **Không có phân quyền theo role** — mọi user đã đăng nhập (bất kể role) đều có thể truy cập.

---

## 📌 Endpoints

### `GET /profile`

```
Request → ProfileController.profile()
    ↓
AuthService.getCurrentUser(session)
    ↓
user == null?
    └── true → return "redirect:/login"   ← Bảo vệ thủ công
    ↓
model.addAttribute("user", user)          ← Truyền User object vào view
    ↓
return "user/profile"                     ← Thymeleaf template
```

---

## ⚙️ Dependencies

| Dependency | Mục đích |
|---|---|
| `AuthService` | Lấy user từ session |

---

## 📝 Key Responsibilities

- **User profile display** — hiển thị thông tin cá nhân của user đang đăng nhập
- **Authentication check** — redirect về `/login` nếu chưa đăng nhập
- **No role restriction** — `ADMIN`, `HR_MANAGER`, `INTERVIEWER`, `CANDIDATE` đều dùng được

> [!info]
> Trang `/profile` là đích redirect của `HomeController` khi user đã đăng nhập vào `/` (trang chủ). Đây cũng là landing page mặc định cho các role không có dashboard riêng.

> [!note]
> **Lưu ý về Double Protection:**
> `AuthInterceptor` đã bảo vệ `/profile` (không nằm trong public paths), nhưng `ProfileController` vẫn kiểm tra thêm `user == null`. Đây là defensive programming — đảm bảo an toàn ngay cả khi có thay đổi ở interceptor trong tương lai.