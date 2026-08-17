# 🎮 Method: profile (GET /profile)

> [!abstract] Phân loại
> **Class:** `ProfileController` | **Loại:** `Controller Method` — Authenticated user GET handler
> **Package:** `com.example.groupproject.controller`

## 🗺️ Ánh xạ
- **HTTP Method:** `GET`
- **URL:** `/profile`
- **Trả về view:** `profile`
- **Quyền truy cập:** Bất kỳ user đã đăng nhập

## 🎯 Tác dụng
Hiển thị trang thông tin cá nhân của user đang đăng nhập: fullName, username, email, role.

## 💉 Dependencies
- `AuthService authService` — lấy user hiện tại và kiểm tra xác thực

## 📥 Parameters & 📤 Return

```java
public String profile(Model model, HttpSession session)
// Return: "profile"
```

**Model attributes được add:**
- `user` → `User` (entity của user đang đăng nhập)

**Return:** `String` — `"profile"`
