# Package: config

> [!abstract]
> Package `config` chứa các class cấu hình toàn cục cho ứng dụng Spring Boot. Thay thế Spring Security bằng cơ chế authentication thủ công qua `HttpSession`, và thiết lập các component cross-cutting (xuyên suốt toàn bộ request).

---

## 📄 Các Class Trong Package

### 1. `AuthInterceptor.java` — Bộ gác cổng HTTP

> [!info]
> **Vai trò:** Kiểm tra authentication và phân quyền (authorization) cho **mọi HTTP request** trước khi request đến Controller.
>
> **Cơ chế hoạt động (`preHandle`):**
> - Lấy `User` từ session qua `AuthService.getCurrentUser()`
> - Nếu `user == null` → redirect về `/login`
> - Kiểm tra role tương ứng với path:
>   - `/admin/**` → yêu cầu `ADMIN`
>   - `/candidate/**` → yêu cầu `CANDIDATE`
>   - `/hr/**`, `/jobs/**` → yêu cầu `ADMIN` hoặc `HR_MANAGER`
>   - `/applications/**` → yêu cầu `ADMIN`, `HR_MANAGER`, hoặc `INTERVIEWER`
>
> **Public paths** (không cần auth): `/login`, `/register`, `/verify`, `/`, `/jobs`, `/forgot-password`, `/reset-password`, `/logout`, `/css/**`, `/js/**`, `/error`

---

### 2. `WebMvcConfig.java` — Đăng ký Interceptor

> [!info]
> **Vai trò:** Implement `WebMvcConfigurer` để đăng ký `AuthInterceptor` vào Spring MVC pipeline.
>
> - Áp dụng interceptor cho pattern `/**` (tất cả paths)
> - **Exclude** các public paths khỏi interceptor (trùng với `isPublicPath()` trong `AuthInterceptor`)
> - Bao gồm: `/`, `/login`, `/register`, `/verify`, `/forgot-password`, `/reset-password`, `/jobs`, `/jobs/**`, `/css/**`, `/js/**`, `/images/**`, `/error`

---

### 3. `GlobalModelAdvice.java` — Inject dữ liệu vào mọi View

> [!info]
> **Vai trò:** Annotated `@ControllerAdvice` — tự động inject các model attribute vào **tất cả** Thymeleaf template mà không cần khai báo lại trong từng Controller.
>
> | Model Attribute | Kiểu | Mô tả |
> |---|---|---|
> | `currentUser` | `User` | Object User đang đăng nhập |
> | `isAuthenticated` | `boolean` | `true` nếu user đã login |
> | `isAdmin` | `boolean` | `true` nếu role là `ADMIN` |
> | `canAccessHr` | `boolean` | `true` nếu role là `ADMIN` hoặc `HR_MANAGER` |
>
> Template Thymeleaf dùng như: `th:if="${isAdmin}"`, `th:text="${currentUser.fullName}"`
```java
@ControllerAdvice
public class GlobalControllerAdvice {

    @ModelAttribute
    public void addUser(Model model, HttpSession session) {
        User user = (User) session.getAttribute("loggedUser");
        model.addAttribute("loggedUser", user);
    }
}
```

---

### 4. `DataInitializer.java` — Seed dữ liệu khởi tạo

> [!info]
> **Vai trò:** Implement `ApplicationRunner` — chạy **1 lần duy nhất** khi ứng dụng khởi động để seed dữ liệu ban đầu.
>
> **Logic:**
> - Kiểm tra xem đã có `ADMIN` account chưa (`userRepository.countByRole(ADMIN)`)
> - Nếu chưa → tạo admin mặc định:
>   - **username:** `admin`
>   - **password:** `Admin@123` (BCrypt encoded)
>   - **email:** `admin@talenthub.local`
>   - **role:** `ADMIN`, **status:** `ACTIVE`
> - Annotated `@Profile("!test")` → **không chạy** trong môi trường test

---

### 5. `PasswordConfig.java` — Bean mã hóa mật khẩu

> [!info]
> **Vai trò:** Đăng ký `BCryptPasswordEncoder` làm Spring Bean (singleton) để inject vào các Service cần hash/verify password.
>
> ```java
> @Bean
> public BCryptPasswordEncoder passwordEncoder() {
>     return new BCryptPasswordEncoder();
> }
> ```
> Được inject vào: `AuthService`, `UserManagementService`.

---

## 🔗 Quan hệ giữa các class

```
WebMvcConfig
    └── đăng ký → AuthInterceptor
                      └── gọi → AuthService.getCurrentUser()

GlobalModelAdvice
    └── inject vào tất cả View ← AuthService.getCurrentUser()

DataInitializer
    └── chạy khi startup → UserRepository.save()

PasswordConfig
    └── cung cấp BCryptPasswordEncoder → AuthService / UserManagementService
```
