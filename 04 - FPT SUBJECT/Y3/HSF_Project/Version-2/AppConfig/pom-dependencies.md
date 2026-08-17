# pom.xml — Dependencies

> [!abstract]
> **TalentHub** được xây dựng trên **Spring Boot 3.5.0** với Java 17. File `pom.xml` khai báo toàn bộ dependencies (thư viện) mà Maven sẽ tải về và đưa vào classpath khi build.

---

## 📦 Project Metadata

| Thuộc tính | Giá trị |
|---|---|
| **groupId** | `com.example` |
| **artifactId** | `GroupProject` |
| **version** | `0.0.1-SNAPSHOT` |
| **Java version** | `17` |
| **Spring Boot parent** | `3.5.0` |

> [!info]
> Kế thừa từ `spring-boot-starter-parent` giúp tự động quản lý phiên bản của tất cả dependencies con — không cần khai báo version thủ công cho từng starter.

---

## 🔌 Dependencies Chính

### 🌐 Core Web + MVC
```xml
<artifactId>spring-boot-starter-web</artifactId>
```
- Bao gồm: **Spring MVC**, **Tomcat** (embedded), **Jackson** (JSON serialization).
- Cung cấp các annotation như `@Controller`, `@GetMapping`, `@PostMapping`, `@RequestParam`, `@PathVariable`.

---

### 🗄️ JPA / Hibernate
```xml
<artifactId>spring-boot-starter-data-jpa</artifactId>
```
- ORM framework để ánh xạ Java class ↔ database table.
- Dùng `@Entity`, `@Id`, `@ManyToOne`, `@OneToMany` để định nghĩa schema.
- Tự động sinh câu SQL thông qua **Hibernate** (implementation của JPA).

---

### 🎨 Thymeleaf (Template Engine)
```xml
<artifactId>spring-boot-starter-thymeleaf</artifactId>
```
- Server-side rendering engine: xử lý HTML template, inject data từ `Model` vào view.
- Cú pháp: `th:text`, `th:each`, `th:if`, `th:action`, `th:object`.
- Kết hợp với `GlobalModelAdvice` để tự động inject `currentUser`, `isAdmin`… vào mọi view.

---

### 🔐 Spring Security Crypto
```xml
<groupId>org.springframework.security</groupId>
<artifactId>spring-security-crypto</artifactId>
```
- **Chỉ** import phần **mã hóa mật khẩu** — **KHÔNG** dùng toàn bộ Spring Security framework.
- Cung cấp `BCryptPasswordEncoder` để hash/verify password an toàn.
- Tham chiếu: `PasswordConfig.java` — đăng ký `BCryptPasswordEncoder` làm Spring Bean.

> [!warning]
> Dự án **không dùng Spring Security cho authentication/authorization**. Thay vào đó, toàn bộ luồng auth được xây dựng thủ công qua `AuthInterceptor` + `HttpSession`.

---

### ✅ Bean Validation
```xml
<artifactId>spring-boot-starter-validation</artifactId>
```
- Kích hoạt các annotation validation như: `@NotBlank`, `@Email`, `@Size`, `@Min`, `@Max`.
- Dùng kết hợp với `@Valid` trên Controller để validate DTO/Form trước khi xử lý.
- Ví dụ: `LoginDTO`, `RegisterDTO`, `CreateUserForm`, `JobFormDTO`.

---

### 📧 Spring Mail
```xml
<artifactId>spring-boot-starter-mail</artifactId>
```
- Tích hợp **JavaMail API** để gửi email.
- Dùng trong: `EmailService.java` — gửi email xác thực tài khoản và OTP reset password.
- Cấu hình SMTP qua `application.properties`.

---

### ♻️ DevTools (Development Only)
```xml
<artifactId>spring-boot-devtools</artifactId>
<scope>runtime</scope>
<optional>true</optional>
```
- **Hot reload**: tự động restart ứng dụng khi code thay đổi.
- `optional=true` → **không bao gồm** trong production build.
- Tắt cache Thymeleaf tự động trong môi trường dev.

---

### 🐬 Database Drivers

| Driver | Artifact | Scope |
|---|---|---|
| **MySQL 8+** | `mysql-connector-j` | `runtime` |
| **PostgreSQL** | `postgresql` | `runtime` |

> [!info]
> Cả hai driver được khai báo nhưng chỉ **MySQL** đang được dùng (theo `application.properties`). Driver PostgreSQL được giữ lại để dễ dàng chuyển đổi database sau này.
> `scope=runtime` — chỉ cần khi chạy ứng dụng, không cần compile-time.

---

### 🧪 Test
```xml
<artifactId>spring-boot-starter-test</artifactId>
<scope>test</scope>
```
- Bao gồm: **JUnit 5**, **Mockito**, **Spring Test**.
- `scope=test` — chỉ có trong classpath khi chạy test, không đưa vào production JAR.

---

## 🔨 Build Plugin

```xml
<artifactId>spring-boot-maven-plugin</artifactId>
```
- Đóng gói ứng dụng thành **fat JAR** (bao gồm Tomcat embedded + toàn bộ dependencies).
- Chạy bằng lệnh: `java -jar GroupProject-0.0.1-SNAPSHOT.jar`.
