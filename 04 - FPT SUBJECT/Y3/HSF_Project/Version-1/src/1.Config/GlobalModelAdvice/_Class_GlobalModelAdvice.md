# ⚙️ Class: GlobalModelAdvice

> [!abstract] Phân loại
> **Loại:** `Config Class` — `@ControllerAdvice` tự động inject các biến global vào Model của mọi Controller.
> **Package:** `com.example.groupproject.config`
> **Annotation:** `@ControllerAdvice`

---

## 💉 Dependencies
- `AuthService authService` — lấy thông tin user hiện tại

---

## 📊 `@ModelAttribute` Methods

| Method | Attribute Key | Kiểu | Mô tả |
|--------|--------------|-------|-------|
| `currentUser(session)` | `currentUser` | `User` | User đang đăng nhập |
| `isAuthenticated(session)` | `isAuthenticated` | `boolean` | Có đăng nhập không |
| `isAdmin(session)` | `isAdmin` | `boolean` | Là ADMIN không |
| `canAccessHr(session)` | `canAccessHr` | `boolean` | Là ADMIN hoặc HR_MANAGER không |

> [!note] Ứng dụng trong Thymeleaf
> Các biến này dùng được trực tiếp trong template: `th:if="${isAdmin}"`, `th:if="${canAccessHr}"` trong `layout.html`.
