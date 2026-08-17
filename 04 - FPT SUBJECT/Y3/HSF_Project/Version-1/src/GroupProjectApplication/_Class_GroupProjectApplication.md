# 🚀 Class: GroupProjectApplication

> [!abstract] Phân loại
> **Loại:** `Main Application Class` — Điểm khởi đầu của ứng dụng Spring Boot.
> **Package:** `com.example.groupproject`
> **Annotation:** `@SpringBootApplication`

---

## 📊 Method: `main(String[] args)`

```java
public static void main(String[] args) {
    SpringApplication.run(GroupProjectApplication.class, args);
}
```

Điểm khởi đầu của JVM. Gọi `SpringApplication.run()` để:
1. Khởi động Spring Application Context
2. Quét và đăng ký tất cả `@Bean`, `@Component`, `@Service`, `@Repository`, `@Controller`
3. Khởi động Tomcat embedded server
4. Chạy `DataInitializer.run()` để seed dữ liệu ban đầu

> [!note] `@SpringBootApplication` là tổ hợp của
> - `@Configuration` — class cấu hình Spring
> - `@EnableAutoConfiguration` — tự động cấu hình dựa theo dependencies
> - `@ComponentScan` — quét beans trong package `com.example.groupproject`
