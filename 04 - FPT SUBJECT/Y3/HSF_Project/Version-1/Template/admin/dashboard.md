# 🎨 Template: admin/dashboard.html

> [!abstract] Tổng quan
> **Đường dẫn:** `src/main/resources/templates/admin/dashboard.html`
> **Controller:** `AdminDashboardController.dashboard()` (GET /admin/dashboard)
> **Vai trò:** Trang tổng quan quản trị hệ thống. Chỉ ADMIN mới thấy.

---

## 🧩 Phân đoạn chính

### 1. Users by Role Section
```html
<div class="role-counts">
    <div class="role-count-item" th:each="entry : ${dashboard.userCountByRole}">
        <div class="count" th:text="${entry.value}">0</div>
        <div class="role-name" th:text="${#strings.replace(entry.key.name(), '_', ' ')}">ADMIN</div>
    </div>
</div>
```
Lặp qua `Map<UserRole, Long>` từ `AdminDashboardData`, hiển thị số user theo từng role.

### 2. Stats Grid
```html
<div class="stats-grid">
    <a th:href="@{/admin/users(status='LOCKED')}" class="stat-card clickable">
        <div class="value" th:text="${dashboard.lockedAccountCount}">0</div>
        <div class="label">Locked Accounts</div>
    </a>
    <!-- Active Jobs, Applied Candidates, Interviews in 7 Days -->
</div>
```
Các stat card có thể click được (Locked Accounts → filter sang trang users). Bind số liệu từ `dashboard.recruitmentSummary`.

### 3. Recent Activity List
```html
<ul class="activity-list" th:if="${!recentActivity.isEmpty()}">
    <li th:each="event : ${recentActivity}">
        <strong th:text="${event.actorDisplayName}">admin</strong> &mdash;
        <span th:text="${#strings.replace(event.eventType.name(), '_', ' ')}">SIGN IN</span>
        <div class="event-time" th:text="${#temporals.format(event.createdAt, 'dd MMM yyyy HH:mm')}">...</div>
    </li>
</ul>
```
Hiển thị 10 sự kiện gần nhất từ `ActivityLogDisplayView`. Dùng `#temporals.format()` để format `Instant` thành chuỗi ngày.

---

## 🔗 Model Variables

| Variable | Kiểu | Nguồn |
|----------|-------|--------|
| `dashboard` | `AdminDashboardData` | `AdminDashboardController` |
| `recentActivity` | `List<ActivityLogDisplayView>` | `AdminDashboardController` |
| `isAdmin`, `canAccessHr` | `boolean` | `GlobalModelAdvice` |
