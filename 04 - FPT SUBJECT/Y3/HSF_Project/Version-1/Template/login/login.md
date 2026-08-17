# 🎨 Template: login.html

> [!abstract] Tổng quan
> **Đường dẫn:** `src/main/resources/templates/login.html`
> **Controller:** `LoginController.login()` (GET /login)
> **Vai trò:** Trang đăng nhập duy nhất của ứng dụng. Public route — không cần xác thực.

---

## 🧩 Phân đoạn chính

### 1. Head Fragment
```html
<head th:replace="~{fragments/layout :: head('Sign In - TalentHub')}"></head>
```
Sử dụng Thymeleaf fragment từ `layout.html` để include CSS và meta tags. Title: *"Sign In - TalentHub"*.

### 2. Alert Messages
```html
<div th:if="${param.error}" class="alert alert-error">Invalid username or password.</div>
<div th:if="${param.logout}" class="alert alert-success">You have been signed out.</div>
```
- `${param.error}` → hiển thị khi URL có `?error` (login thất bại)
- `${param.logout}` → hiển thị khi URL có `?logout` (vừa đăng xuất)

### 3. Login Form
```html
<form th:action="@{/login}" method="post">
    <input type="text" id="username" name="username" required autofocus/>
    <input type="password" id="password" name="password" required/>
    <button type="submit" class="btn btn-primary">Sign In</button>
</form>
```
- `th:action="@{/login}"` → gửi POST đến `/login` (xử lý bởi `LoginController.loginSubmit()`)
- `required` → HTML5 client-side validation
- `autofocus` → tự focus vào trường username khi load trang

---

## 🔗 Model Variables sử dụng

| Variable | Nguồn | Mô tả |
|----------|--------|-------|
| `param.error` | URL query param | Param `?error` trong URL |
| `param.logout` | URL query param | Param `?logout` trong URL |
