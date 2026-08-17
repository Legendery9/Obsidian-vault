# 📦 pom.xml — Dependencies & Build

> [!abstract] Tổng quan
> File quản lý dependencies và build của dự án Maven.
> **Artifact:** `GroupProject` | **Group:** `com.example` | **Version:** `0.0.1-SNAPSHOT`
> **Spring Boot Parent:** `3.5.0` | **Java Version:** `21`

---

## 🏗️ Parent & Project Info

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>3.5.0</version>
</parent>
<properties>
    <java.version>21</java.version>
</properties>
```

> [!info] Spring Boot Parent
> Kế thừa từ `spring-boot-starter-parent` giúp tự động quản lý version của tất cả dependencies con, không cần khai báo version riêng lẻ. Java 21 là LTS version hiện đại nhất.

---

## 📚 Dependencies

> [!info] Nhóm 1 — Core Web & MVC
> ### `spring-boot-starter-web`
> - **GroupId:** `org.springframework.boot`
> - **Tác dụng:** Cung cấp Spring MVC (DispatcherServlet, Controllers, REST), Tomcat embedded server, Jackson (JSON serialization). Là nền tảng để xây dựng web application.

---

> [!info] Nhóm 2 — Database & ORM
> ### `spring-boot-starter-data-jpa`
> - **GroupId:** `org.springframework.boot`
> - **Tác dụng:** Tích hợp Spring Data JPA + Hibernate ORM. Cho phép dùng `@Entity`, `@Repository`, `JpaRepository` để thao tác database mà không cần viết SQL thủ công.
>
> ### `mysql-connector-j`
> - **GroupId:** `com.mysql` | **Scope:** `runtime`
> - **Tác dụng:** JDBC Driver cho MySQL. Cần thiết để ứng dụng kết nối được với MySQL server. Scope `runtime` nghĩa là chỉ cần khi chạy, không cần compile.
>
> ### `postgresql`
> - **GroupId:** `org.postgresql` | **Scope:** `runtime`
> - **Tác dụng:** JDBC Driver cho PostgreSQL. Được thêm vào dự phòng, dự án hiện đang dùng MySQL nhưng có thể chuyển sang PostgreSQL.

---

> [!info] Nhóm 3 — Template Engine
> ### `spring-boot-starter-thymeleaf`
> - **GroupId:** `org.springframework.boot`
> - **Tác dụng:** Tích hợp Thymeleaf — template engine phía server cho Java. Cho phép viết HTML với các thuộc tính `th:*` để binding data từ Model, xử lý điều kiện, vòng lặp, fragment layout.

---

> [!info] Nhóm 4 — Validation
> ### `spring-boot-starter-validation`
> - **GroupId:** `org.springframework.boot`
> - **Tác dụng:** Tích hợp Jakarta Bean Validation (Hibernate Validator). Cho phép dùng các annotation `@NotBlank`, `@Email`, `@Size`, `@Pattern` trên DTO/Form class để validate input tự động.

---

> [!info] Nhóm 5 — Development Tools
> ### `spring-boot-devtools`
> - **GroupId:** `org.springframework.boot` | **Scope:** `runtime` | **Optional:** `true`
> - **Tác dụng:** Công cụ hỗ trợ development: **hot reload** (tự động restart khi thay đổi class), **LiveReload** (refresh browser tự động), tắt cache Thymeleaf. Scope `optional` nghĩa là không được đóng gói vào production JAR.

---

> [!info] Nhóm 6 — Testing
> ### `spring-boot-starter-test`
> - **GroupId:** `org.springframework.boot` | **Scope:** `test`
> - **Tác dụng:** Bộ testing framework đầy đủ: JUnit 5, Mockito, Spring Test (MockMvc, @SpringBootTest), AssertJ. Chỉ dùng trong môi trường test, không đóng gói vào production.

---

## 🔨 Build Plugins

```xml
<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
</plugin>
```

| Plugin | Tác dụng |
|--------|----------|
| `spring-boot-maven-plugin` | Đóng gói ứng dụng thành **executable JAR** (fat JAR) với tất cả dependencies. Cho phép chạy `mvn spring-boot:run` để khởi động dev server. |
