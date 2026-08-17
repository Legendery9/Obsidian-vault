# 🎮 Method: logout (POST /logout)

> [!abstract] Phân loại
> **Class:** `LoginController` | **Loại:** `Controller Method` — Spring MVC POST handler
> **Package:** `com.example.groupproject.controller`

## 🗺️ Ánh xạ
- **HTTP Method:** `POST`
- **URL:** `/logout`
- **Form action:** button "Sign Out" trong `profile.html`

## 🎯 Tác dụng
Hủy session hiện tại của user (đăng xuất), sau đó redirect về trang login với param `?logout` để hiển thị thông báo đăng xuất thành công.

## 💉 Dependencies
- `AuthService authService` — gọi `session.invalidate()` để hủy session

## 📥 Parameters & 📤 Return

```java
public String logout(HttpSession session)
// Return: "redirect:/login?logout"
```

| Tham số | Kiểu | Mô tả |
|---------|------|-------|
| `session` | `HttpSession` | Session hiện tại cần hủy |

**Return:** `String` — `"redirect:/login?logout"` luôn luôn
