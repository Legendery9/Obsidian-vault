# ⚙️ application.properties — Giải thích cấu hình

> [!abstract] Tổng quan
> File cấu hình chính của ứng dụng Spring Boot **TalentHub Recruitment Management System**.
> Được đặt tại `src/main/resources/application.properties`.

---

## 🏷️ Thông tin ứng dụng

| Key | Value | Ý nghĩa |
|-----|-------|---------|
| `spring.application.name` | `GroupProject` | Tên định danh của ứng dụng Spring Boot. Được dùng trong log, actuator, service discovery. |

---

## 🗄️ Cấu hình Database — MySQL

```properties
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/talenthub?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC&characterEncoding=UTF-8
spring.datasource.username=root
spring.datasource.password=abc123
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

| Key | Value | Ý nghĩa |
|-----|-------|---------|
| `spring.datasource.url` | `jdbc:mysql://127.0.0.1:3306/talenthub?...` | URL kết nối JDBC đến MySQL server trên localhost, schema `talenthub`. Các tham số: `useSSL=false` (tắt SSL), `allowPublicKeyRetrieval=true` (cho phép lấy public key khi xác thực), `serverTimezone=UTC` (timezone server), `characterEncoding=UTF-8` (encoding). |
| `spring.datasource.username` | `root` | Tên đăng nhập MySQL. |
| `spring.datasource.password` | `abc123` | Mật khẩu MySQL. |
| `spring.datasource.driver-class-name` | `com.mysql.cj.jdbc.Driver` | Driver JDBC cho MySQL Connector/J 8+. |

> [!warning] Bảo mật
> Mật khẩu `abc123` đang được lưu plain-text trong file cấu hình. Trong môi trường production, nên dùng biến môi trường hoặc Secret Manager thay thế.

---

## 🔧 Cấu hình JPA / Hibernate

```properties
spring.jpa.hibernate.ddl-auto=validate
spring.jpa.open-in-view=false
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
spring.jpa.properties.hibernate.format_sql=true
```

| Key | Value | Ý nghĩa |
|-----|-------|---------|
| `spring.jpa.hibernate.ddl-auto` | `validate` | Hibernate sẽ **kiểm tra** schema database có khớp với các Entity không, nhưng **không tạo/sửa** bảng. Nếu không khớp → ném exception khi start. |
| `spring.jpa.open-in-view` | `false` | Tắt Open Session in View pattern. Tránh lazy loading ngoài transaction, buộc load data đúng trong service layer. |
| `spring.jpa.show-sql` | `true` | In ra câu SQL được Hibernate thực thi vào console/log. Hữu ích khi debug. |
| `spring.jpa.properties.hibernate.dialect` | `MySQLDialect` | Dialect để Hibernate sinh SQL tương thích với MySQL. |
| `spring.jpa.properties.hibernate.format_sql` | `true` | Format SQL in ra cho dễ đọc (indent, xuống dòng). |

> [!note] Lưu ý `ddl-auto=validate`
> Schema thực tế phải được tạo thủ công từ file `talenthub_schema.sql` hoặc `talenthub_schema-mysql.sql` trước khi chạy app.

---

## 🌿 Cấu hình Thymeleaf

```properties
spring.thymeleaf.cache=false
```

| Key | Value | Ý nghĩa |
|-----|-------|---------|
| `spring.thymeleaf.cache` | `false` | Tắt cache template Thymeleaf. Mỗi request sẽ reload lại file HTML từ disk. Chỉ dùng trong môi trường **development** để xem thay đổi ngay lập tức mà không cần restart. |

---

## 🌐 Cấu hình Server

```properties
server.port=10111
server.error.whitelabel.enabled=false
```

| Key | Value | Ý nghĩa |
|-----|-------|---------|
| `server.port` | `10111` | Ứng dụng lắng nghe HTTP tại port `10111` (thay vì port mặc định `8080`). Truy cập tại `http://localhost:10111`. |
| `server.error.whitelabel.enabled` | `false` | Tắt trang lỗi mặc định của Spring Boot (Whitelabel Error Page). Ứng dụng sẽ tự xử lý error theo cách riêng. |
