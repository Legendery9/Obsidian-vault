# 🎨 Template: change-password.html

> [!abstract] Tổng quan
> **Đường dẫn:** `src/main/resources/templates/change-password.html`
> **Controller:** `ProfileController.changePassword()` (GET /change-password)
> **Vai trò:** Trang đổi mật khẩu. Hiện tại là **placeholder** — form đổi mật khẩu sẽ có trong sprint tiếp theo.

---

## 🧩 Nội dung hiện tại

```html
<div class="card">
    <p>This screen will allow you to change your password. Please check back later.</p>
    <a th:href="@{/profile}" class="btn btn-secondary">Back to Profile</a>
</div>
```

> [!note] Sprint roadmap
> "SCR-04" — Form sẽ bao gồm: nhập mật khẩu cũ, mật khẩu mới, xác nhận mật khẩu mới. Liên kết với `PasswordResetToken` entity đã có sẵn.
