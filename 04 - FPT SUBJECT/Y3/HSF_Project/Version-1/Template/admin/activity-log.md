# 🎨 Template: admin/activity-log.html

> [!abstract] Tổng quan
> **Đường dẫn:** `src/main/resources/templates/admin/activity-log.html`
> **Controller:** `AdminDashboardController.activityLog()` (GET /admin/activity-log)
> **Vai trò:** Trang Activity Log đầy đủ. Hiện tại là **placeholder** — chức năng searchable log sẽ có trong sprint tiếp theo.

---

## 🧩 Nội dung hiện tại

```html
<div class="card">
    <p>The searchable activity log will be available here.</p>
    <a th:href="@{/admin/dashboard}" class="btn btn-secondary">Back to Admin Dashboard</a>
</div>
```

> [!note] Sprint roadmap
> Trang này đang hiển thị placeholder text "SCR-09". Full activity log (tìm kiếm, phân trang, filter theo event type) sẽ được implement trong sprint tiếp theo.
