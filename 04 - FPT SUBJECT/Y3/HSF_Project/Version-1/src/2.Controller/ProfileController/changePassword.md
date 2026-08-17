# 🎮 Method: changePassword (GET /change-password)

> [!abstract] Phân loại
> **Class:** `ProfileController` | **Loại:** `Controller Method` — Authenticated user GET handler
> **Package:** `com.example.groupproject.controller`

## 🗺️ Ánh xạ
- **HTTP Method:** `GET`
- **URL:** `/change-password`
- **Trả về view:** `change-password`
- **Quyền truy cập:** Bất kỳ user đã đăng nhập

## 🎯 Tác dụng
Hiển thị trang đổi mật khẩu. Hiện tại là placeholder — form đổi mật khẩu "coming in next sprint".

## 💉 Dependencies
- `AuthService authService` — kiểm tra user đã đăng nhập

## 📥 Parameters & 📤 Return

```java
public String changePassword(HttpSession session)
// Return: "change-password"
```

**Return:** `String` — `"change-password"`
