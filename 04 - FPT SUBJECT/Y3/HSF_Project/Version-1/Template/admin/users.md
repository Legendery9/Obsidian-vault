# 🎨 Template: admin/users.html

> [!abstract] Tổng quan
> **Đường dẫn:** `src/main/resources/templates/admin/users.html`
> **Controller:** `UserManagementController` (GET+POST /admin/users)
> **Vai trò:** Trang quản lý tài khoản hệ thống. Chỉ ADMIN truy cập.

---

## 🧩 Phân đoạn chính

### 1. Flash Messages
```html
<div th:if="${successMessage}" class="alert alert-success" th:text="${successMessage}"></div>
<div th:if="${errorMessage}" class="alert alert-error" th:text="${errorMessage}"></div>
```

### 2. Search & Filter Form
```html
<form th:action="@{/admin/users}" method="get" class="filter-bar">
    <input type="text" name="search" th:value="${search}" placeholder="Search..."/>
    <select name="role"><!-- các option từ ${roles} --></select>
    <select name="status"><!-- các option từ ${statuses} --></select>
    <button type="submit">Filter</button>
</form>
```
Filter GET form với 3 tiêu chí: text search, role, status. `th:value` giữ lại giá trị filter.

### 3. Create User Form
```html
<form th:action="@{/admin/users}" th:object="${createUserForm}" method="post">
    <input type="text" id="fullName" th:field="*{fullName}"/>
    <span class="field-error" th:if="${#fields.hasErrors('fullName')}" th:errors="*{fullName}"></span>
    <!-- username, email, password, role tương tự -->
    <button type="submit">Create Account</button>
</form>
```
- `th:object` binding với `CreateUserForm`
- `th:field="*{fieldName}"` tự set id/name/value
- `#fields.hasErrors()` + `th:errors` hiển thị lỗi validation từng trường

### 4. User List Table
```html
<tr th:each="u : ${users}">
    <!-- hiển thị fullName, username, email, role badge, status badge, createdAt -->
    <td class="actions-cell">
        <form th:if="${canUnlock[u.id]}" th:action="@{/admin/users/{id}/unlock(id=${u.id})}" method="post">
            <button class="btn btn-warning btn-sm">Unlock</button>
        </form>
        <form th:if="${canDeactivate[u.id]}" th:action="@{/admin/users/{id}/deactivate(id=${u.id})}" method="post">
            <button class="btn btn-danger btn-sm">Deactivate</button>
        </form>
    </td>
</tr>
```
- `canUnlock`, `canDeactivate` là `Map<Integer, Boolean>` — kiểm tra từng user có được unlock/deactivate không
- Path variable `{id}` trong action URL

---

## 🔗 Model Variables

| Variable | Kiểu | Nguồn |
|----------|-------|--------|
| `users` | `List<User>` | `UserManagementController` |
| `createUserForm` | `CreateUserForm` | `UserManagementController` |
| `canUnlock`, `canDeactivate` | `Map<Integer, Boolean>` | `UserManagementController` |
| `roles`, `statuses`, `creatableRoles` | Enum arrays | `UserManagementController` |
| `search`, `selectedRole`, `selectedStatus` | Filter values | `UserManagementController` |
