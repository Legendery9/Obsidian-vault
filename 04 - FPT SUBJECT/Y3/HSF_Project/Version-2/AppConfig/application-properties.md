# application.properties

> [!abstract]
> File cấu hình trung tâm của Spring Boot. Tất cả các tham số runtime của ứng dụng **TalentHub** đều được khai báo tại đây, thay thế cho XML configuration truyền thống.

---

## 🗄️ Database — MySQL

```properties
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/talenthub?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC&characterEncoding=UTF-8
spring.datasource.username=root
spring.datasource.password=abc123
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

> [!info]
> **Các tham số URL quan trọng:**
> - `useSSL=false` — Tắt SSL (phù hợp môi trường local dev)
> - `allowPublicKeyRetrieval=true` — Cho phép lấy public key từ MySQL server (bắt buộc với MySQL 8+)
> - `serverTimezone=UTC` — Đảm bảo thống nhất múi giờ khi lưu trữ `DATETIME`
> - `characterEncoding=UTF-8` — Hỗ trợ tiếng Việt trong database

> [!warning]
> Phiên bản PostgreSQL đã được **comment out** (dấu `#`). Nếu chuyển sang PostgreSQL, cần bỏ comment các dòng `postgresql` và đổi `dialect` tương ứng.

---

## ⚙️ JPA / Hibernate

```properties
spring.jpa.hibernate.ddl-auto=update
spring.jpa.open-in-view=false
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
spring.jpa.properties.hibernate.format_sql=true
```

> [!info]
> **Giải thích từng tham số:**
> - `ddl-auto=update` — Hibernate tự động **cập nhật schema** khi khởi động (thêm cột/bảng mới) nhưng **không xóa** dữ liệu cũ. Phù hợp dev, **không dùng cho production**.
> - `open-in-view=false` — Tắt OSIV pattern → tránh giữ DB connection lâu, cải thiện performance.
> - `show-sql=true` — In ra câu SQL được Hibernate sinh ra (dùng debug).
> - `format_sql=true` — Format SQL để dễ đọc hơn trong console.

> [!warning]
> `ddl-auto=update` **KHÔNG nên dùng trên môi trường production**. Trên production cần đổi thành `validate` hoặc dùng migration tool như **Flyway/Liquibase**.

---

## 📝 Logging

```properties
logging.level.org.hibernate.SQL=DEBUG
logging.level.org.hibernate.type.descriptor.sql.BasicBinder=TRACE
```

> [!info]
> - `hibernate.SQL=DEBUG` — Log toàn bộ câu SQL.
> - `BasicBinder=TRACE` — Log các **tham số bind** (giá trị thực tế được truyền vào `?` placeholder).

---

## 📧 Email — SMTP Gmail

```properties
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=phamthaihai2272004@gmail.com
spring.mail.password=vwykzpujfbvwdsyn
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
```

> [!info]
> - **Port 587** + **STARTTLS** — Chuẩn giao thức bảo mật cho SMTP hiện đại (khác với SSL port 465).
> - `smtp.auth=true` — Yêu cầu xác thực username/password trước khi gửi mail.
> - `password` ở đây là **App Password** của Google (không phải mật khẩu Google account thực).

> [!warning]
> **Không commit** `spring.mail.password` lên Git public repository. Nên dùng biến môi trường hoặc Spring Vault trong dự án thực tế.

---

## 🖥️ Server

```properties
server.port=8080
server.error.whitelabel.enabled=false
```

> [!info]
> - `port=8080` — Ứng dụng chạy tại `http://localhost:8080`.
> - `whitelabel.enabled=false` — Tắt trang lỗi mặc định của Spring Boot, cho phép dùng custom error page riêng.

---

## 📁 File Upload

```properties
spring.servlet.multipart.max-file-size=5MB
spring.servlet.multipart.max-request-size=5MB
```

> [!info]
> Giới hạn kích thước file upload (CV, ảnh đại diện…). Cả hai giá trị cần đặt bằng nhau để tránh lỗi request bị reject trước khi xử lý từng file.

---

## 🎨 Thymeleaf

```properties
spring.thymeleaf.cache=false
```

> [!info]
> Tắt cache template Thymeleaf → Thay đổi HTML/template sẽ được phản ánh ngay **không cần restart** ứng dụng. Chỉ dùng ở môi trường development.
