# ⚙️ Class: WebMvcConfig

> [!abstract] Phân loại
> **Loại:** `Config Class` — Đăng ký `AuthInterceptor` vào Spring MVC interceptor chain.
> **Package:** `com.example.groupproject.config`
> **Annotation:** `@Configuration`
> **Implements:** `WebMvcConfigurer`

---

## 💉 Dependencies
- `AuthInterceptor authInterceptor` — interceptor cần đăng ký

---

## 📊 Method: `addInterceptors`

```java
@Override
public void addInterceptors(InterceptorRegistry registry) {
    registry.addInterceptor(authInterceptor)
            .addPathPatterns("/**")
            .excludePathPatterns("/css/**", "/js/**", "/error");
}
```

Đăng ký `AuthInterceptor` cho tất cả path (`/**`) trừ static resources và error page.
