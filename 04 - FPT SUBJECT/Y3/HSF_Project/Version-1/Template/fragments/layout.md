# 🎨 Template: fragments/layout.html

> [!abstract] Tổng quan
> **Đường dẫn:** `src/main/resources/templates/fragments/layout.html`
> **Vai trò:** File fragment chứa các template piece tái sử dụng: `head`, `header`, `footer`. Mọi trang đều import từ đây.

---

## 🧩 Các Fragment

### Fragment 1: `head(title)`
```html
<head th:fragment="head(title)">
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1"/>
    <title th:text="${title}">TalentHub</title>
    <link rel="stylesheet" th:href="@{/css/style.css}"/>
</head>
```
- **Tham số `title`:** Tên trang truyền từ mỗi page (e.g. `'Sign In - TalentHub'`)
- Include CSS toàn cục `style.css`
- Sử dụng: `<head th:replace="~{fragments/layout :: head('Page Title - TalentHub')}">`

### Fragment 2: `header`
```html
<header th:fragment="header" class="site-header">
    <div class="container header-inner">
        <a th:href="@{/profile}" class="logo">TalentHub</a>
        <nav class="main-nav" th:if="${isAuthenticated}">
            <a th:href="@{/profile}">Profile</a>
            <a th:href="@{/hr/dashboard}" th:if="${canAccessHr}">HR Dashboard</a>
            <a th:href="@{/admin/dashboard}" th:if="${isAdmin}">Admin Dashboard</a>
            <a th:href="@{/admin/users}" th:if="${isAdmin}">Users</a>
        </nav>
    </div>
</header>
```
- Nav chỉ hiển khi `${isAuthenticated}` = true
- Menu items hiển theo role (từ `GlobalModelAdvice`)

### Fragment 3: `footer`
```html
<footer th:fragment="footer" class="site-footer">
    <div class="container"><p>&copy; 2026 TalentHub</p></div>
</footer>
```
Footer đơn giản với copyright.

---

## 🔗 Model Variables sử dụng

| Variable | Nguồn |
|----------|---------|
| `isAuthenticated` | `GlobalModelAdvice` |
| `canAccessHr` | `GlobalModelAdvice` |
| `isAdmin` | `GlobalModelAdvice` |
