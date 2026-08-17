# 🎮 Method: home (GET /)

> [!abstract] Phân loại
> **Class:** `LoginController` | **Loại:** `Controller Method` — Root URL redirect
> **Package:** `com.example.groupproject.controller`

## 🗺️ Ánh xạ
- **HTTP Method:** `GET`
- **URL:** `/` (root)

## 🎯 Tác dụng
Redirect URL gốc `/` đến `/profile`. Đây là entry point của ứng dụng — mọi request đến root đều được chuyển đến trang Profile (AuthInterceptor sẽ kiểm tra authentication tiếp theo).

## 📥 Parameters & 📤 Return

```java
public String home()
// Return: "redirect:/profile"
```

**Return:** `String` — `"redirect:/profile"` luôn luôn