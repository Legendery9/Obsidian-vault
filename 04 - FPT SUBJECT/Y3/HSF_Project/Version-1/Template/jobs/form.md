# 🎨 Template: jobs/form.html

> [!abstract] Tổng quan
> **Đường dẫn:** `src/main/resources/templates/jobs/form.html`
> **Controller:** `JobController.createJob()` (GET /jobs/new)
> **Vai trò:** Form tạo Job Posting mới. Hiện tại là **placeholder** — form đầy đủ sẽ có trong sprint tiếp theo.

---

## 🧩 Nội dung hiện tại

```html
<div class="card">
    <p>The job creation form will be available here.</p>
    <a th:href="@{/hr/dashboard}" class="btn btn-secondary">Back to HR Dashboard</a>
</div>
```

> [!note] Sprint roadmap
> "SCR-11" — Form tạo job đầy đủ sẽ cho phép nhập: title, department, location, description, requirements, salary range, deadline, và submit để tạo `JobPosting` entity mới.
