# 🎨 Template: profile.html

> [!abstract] Tổng quan
> **Đường dẫn:** `src/main/resources/templates/profile.html`
> **Controller:** `ProfileController.profile()` (GET /profile)
> **Vai trò:** Trang thông tin cá nhân. Đây là landing page sau đăng nhập và redirect từ URL gốc `/`.

---

## 🧩 Phân đoạn chính

### 1. Header & Footer Fragments
```html
<header th:replace="~{fragments/layout :: header}"></header>
<footer th:replace="~{fragments/layout :: footer}"></footer>
```
Sử dụng global header/footer từ `layout.html`.

### 2. Profile Information Card
```html
<dl class="profile-grid">
    <dt>Full Name</dt>   <dd th:text="${user.fullName}">John Doe</dd>
    <dt>Username</dt>   <dd th:text="${user.username}">johndoe</dd>
    <dt>Email</dt>      <dd th:text="${user.email}">john@example.com</dd>
    <dt>Role</dt>
    <dd>
        <span class="badge"
              th:classappend="'badge-' + ${#strings.toLowerCase(user.role.name())}"
              th:text="${#strings.replace(user.role.name(), '_', ' ')}">ADMIN</span>
    </dd>
</dl>
```
- Bind dữ liệu từ Model attribute `user` (User entity)
- `#strings.toLowerCase()` → tạo CSS class badge theo role (badge-admin, badge-hr_manager...)

### 3. Action Buttons (Hiển thị theo Role)
```html
<a th:href="@{/change-password}" class="btn btn-secondary">Change Password</a>
<a th:href="@{/hr/dashboard}" th:if="${canAccessHr}" class="btn btn-secondary">HR Dashboard</a>
<a th:href="@{/admin/dashboard}" th:if="${isAdmin}" class="btn btn-secondary">Admin Dashboard</a>
<form th:action="@{/logout}" method="post"><button type="submit" class="btn btn-danger">Sign Out</button></form>
```
- `th:if="${canAccessHr}"` → chỉ hiển với ADMIN/HR_MANAGER
- `th:if="${isAdmin}"` → chỉ hiển với ADMIN

---

## 🔗 Model Variables sử dụng

| Variable | Nguồn | Mô tả |
|----------|--------|-------|
| `user` | `ProfileController` | User entity của user đang đăng nhập |
| `isAdmin` | `GlobalModelAdvice` | Boolean: là ADMIN không |
| `canAccessHr` | `GlobalModelAdvice` | Boolean: có quyền HR không |
