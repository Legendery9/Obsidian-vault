# ⚙️ Class: DataInitializer

> [!abstract] Phân loại
> **Loại:** `Config Component` — Khởi tạo dữ liệu ban đầu khi ứng dụng start.
> **Package:** `com.example.groupproject.config`
> **Annotation:** `@Component @Profile("!test")`
> **Implements:** `ApplicationRunner`

---

## 💉 Dependencies
- `UserRepository userRepository` — kiểm tra và tạo admin mặc định

---

## 📊 Method: `run(ApplicationArguments args)`

```java
@Override
@Transactional
public void run(ApplicationArguments args)
```

**Logic:** Nếu chưa có ADMIN nào trong DB → tạo tài khoản admin mặc định:

```
Username: admin
Password: Admin@123
Email:    admin@talenthub.local
Role:     ADMIN
Status:   ACTIVE
```

> [!warning] Chỉ chạy khi `@Profile("!test")`
> Không chạy trong môi trường test. Mật khẩu admin mặc định lưu plain-text — nên thay đổi ngay khi deploy lên môi trường thực.
