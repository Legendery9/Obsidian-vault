# 🎮 Method: loginSubmit (POST /login)

> [!abstract] Phân loại
> **Class:** `LoginController` | **Loại:** `Controller Method` — Spring MVC POST handler
> **Package:** `com.example.groupproject.controller`

## 🗺️ Ánh xạ
- **HTTP Method:** `POST`
- **URL:** `/login`
- **Form action:** `th:action="@{/login}" method="post"` trong `login.html`

## 🎯 Tác dụng
Xử lý form đăng nhập: nhận username + password từ request, gọi `AuthService.login()` để xác thực. Nếu thành công → redirect profile. Nếu thất bại → redirect về login với param `?error`.

## 💉 Dependencies
- `AuthService authService` — thực hiện xác thực user, lưu session

## 📥 Parameters & 📤 Return

```java
public String loginSubmit(@RequestParam String username,
                          @RequestParam String password,
                          HttpSession session)
// Return: "redirect:/profile" | "redirect:/login?error"
```

| Tham số | Kiểu | Mô tả |
|---------|------|-------|
| `username` | `String` | Username từ form HTML (`name="username"`) |
| `password` | `String` | Password từ form HTML (`name="password"`) |
| `session` | `HttpSession` | Session dùng để lưu user ID sau login thành công |

**Return:** `String` redirect — về `/profile` nếu login OK, về `/login?error` nếu thất bại
