# Spring Boot Setup and Configuration

> [!abstract] Định nghĩa
> Note này tóm tắt cách thiết lập và cấu hình dự án Spring Boot bằng công cụ dựng (Build Tools - Maven/Gradle) và các định dạng cấu hình ứng dụng (`application.properties` / `application.yml`).

---

## 1. Công cụ dựng dự án: Maven vs Gradle

Spring Boot hỗ trợ hai công cụ quản lý thư viện và xây dựng dự án phổ biến nhất là **Maven** (sử dụng file cấu hình `pom.xml` dạng XML) và **Gradle** (sử dụng file cấu hình `build.gradle` dựa trên ngôn ngữ Groovy hoặc Kotlin DSL).

### Quản lý Dependency trong `pom.xml` (Maven)

Mỗi thư viện (dependency) được định nghĩa bởi bộ ba thông tin: `groupId`, `artifactId`, và `version`.

```xml
<dependencies>
    <!-- Web Starter hỗ trợ dựng MVC và REST APIs -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

> [!info] Spring Boot Parent Pom
> Thông thường, các dự án Spring Boot thừa kế cấu hình từ `spring-boot-starter-parent`. Lợi ích lớn nhất là bạn **không cần chỉ định phiên bản (`version`)** cho các starter chính thức của Spring Boot, giúp tránh xung đột phiên bản thư viện.

---

## 2. Định dạng cấu hình: Properties vs YAML

Spring Boot cho phép khai báo thông tin cấu hình (như cổng kết nối, cơ sở dữ liệu, logging) bằng một trong hai định dạng:

### Định dạng Properties (`application.properties`)
- Cấu trúc phẳng, sử dụng cặp khóa-giá trị phân tách bởi dấu bằng `=`. Dễ đọc cho các cấu hình nhỏ nhưng bị lặp lại các tiền tố (prefix).

```properties
server.port=8080
spring.datasource.url=jdbc:mysql://localhost:3306/db_name
spring.datasource.username=root
spring.datasource.password=123456
```

### Định dạng YAML (`application.yml`)
- Cấu trúc hình cây thụt lề cấp bậc rõ ràng, không bị lặp lại tiền tố, rất phù hợp cho các cấu hình phức tạp.

```yaml
server:
  port: 8080

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/db_name
    username: root
    password: 123456
```

> [!warning] Quy tắc định dạng YAML
> - Thụt lề trong YAML bắt buộc sử dụng **khoảng trắng (spaces)**, tuyệt đối không dùng phím Tab (gây lỗi phân tích cú pháp khởi chạy).
> - Sau dấu hai chấm `:` bắt buộc phải có **một khoảng trắng** trước khi điền giá trị.
> ```yaml
> # ✅ Nên làm (Do)
> server:
>   port: 8080
> 
> # ❌ Không nên làm (Don't)
> server:
>   port:8080 # Thiếu khoảng trắng sau dấu hai chấm!
> ```

---

## 3. Đọc cấu hình vào ứng dụng bằng `@Value`

Để đọc các cấu hình đã khai báo trong file `.properties` hoặc `.yml` vào trong Java Beans, ta sử dụng annotation `@Value` kết hợp cú pháp SpEL (Spring Expression Language).

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class DatabaseConfig {

    // ✅ Nên làm (Do): Định nghĩa giá trị mặc định sau dấu hai chấm đề phòng cấu hình bị thiếu.
    @Value("${server.port:8080}")
    private int serverPort;

    public void printPort() {
        System.out.println("Server is running on port: " + serverPort);
    }
}
```
