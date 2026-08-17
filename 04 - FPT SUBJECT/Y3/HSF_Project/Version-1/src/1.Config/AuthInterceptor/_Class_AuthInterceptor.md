# 🛡️ Class: AuthInterceptor

> [!abstract] Phân loại
> **Loại:** `Config Component` — Spring MVC HandlerInterceptor thay thế Spring Security cho việc kiểm soát truy cập URL.
> **Package:** `com.example.groupproject.config`
> **Annotation:** `@Component`
> **Implements:** `HandlerInterceptor`

---

## 💉 Dependencies
- `AuthService authService` — lấy current user từ session

---

## 📊 Method: `preHandle`

```java
@Override
public boolean preHandle(HttpServletRequest request,
                          HttpServletResponse response,
                          Object handler) throws Exception
```

**Logic phân quyền URL:**

| Path | Điều kiện | Hành động |
|------|-----------|----------|
| `/login`, `/css/**`, `/js/**`, `/error` | Public | Cho qua |
| bất kỳ | User chưa login | Redirect `/login` |
| `/admin/**` | Không phải ADMIN | 403 Forbidden |
| `/hr/**`, `/jobs/**` | Không phải ADMIN/HR_MANAGER | 403 Forbidden |
| Khác | Đã login | Cho qua |

**Return:** `boolean` — `true` (cho qua) hoặc `false` (đã xử lý redirect/error)
