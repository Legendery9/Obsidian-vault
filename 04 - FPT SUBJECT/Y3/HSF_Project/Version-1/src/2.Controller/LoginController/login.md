# 🎮 Method: login (GET /login)

> [!abstract] Phân loại
> **Class:** `LoginController` | **Loại:** `Controller Method` — Spring MVC GET handler
> **Package:** `com.example.groupproject.controller`

## 🗺️ Ánh xạ
- **HTTP Method:** `GET`
- **URL:** `/login`
- **Trả về view:** `login` (render template `templates/login.html`)

## 🎯 Tác dụng
Hiển thị trang đăng nhập. Nếu user đã đăng nhập (có session hợp lệ), redirect ngay đến `/profile` (không hiển thị form login lại).

## 💉 Dependencies
- `AuthService authService` — kiểm tra trạng thái đăng nhập qua session

## 📥 Parameters & 📤 Return

```java
public String login(HttpSession session)
// Return: "login" | "redirect:/profile"
```

| Tham số | Kiểu | Mô tả |
|---------|------|-------|
| `session` | `HttpSession` | Session hiện tại của request |

**Return:** `String` — tên view `"login"` hoặc redirect string `"redirect:/profile"`
