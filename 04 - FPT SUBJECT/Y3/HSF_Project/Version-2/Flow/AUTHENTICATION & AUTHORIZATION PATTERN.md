# 🔐 AUTHENTICATION & AUTHORIZATION PATTERN

> [!abstract]
> Dự án **không dùng Spring Security** cho auth. Thay vào đó, toàn bộ cơ chế authentication và authorization được xây dựng thủ công dựa trên **`HttpSession`** + **`AuthInterceptor`** + **`AuthService`**.

---

## 🔑 Authentication Flow (Đăng nhập)

```
POST /login (LoginController)
    ↓
AuthService.login(dto, session)
    ├── Tìm user theo username → UserRepository.findByUsername()
    ├── Kiểm tra status: INACTIVE → throw IllegalStateException
    ├── Kiểm tra status: LOCKED (admin) → throw AdminLockedException
    ├── BCryptPasswordEncoder.matches(raw, hash)
    │   ├── Sai → tăng failedLoginCount
    │   │         ├── < 5 lần → throw IllegalArgumentException
    │   │         └── ≥ 5 lần → status=LOCKED → throw AccountLockedException
    │   └── Đúng → reset failedLoginCount = 0
    ├── Kiểm tra emailVerified → throw nếu chưa xác thực
    ├── session.setAttribute("loggedInUserId", user.getId())
    └── return User
    ↓
LoginController: redirect theo role
    ├── ADMIN       → /admin/dashboard
    ├── HR_MANAGER  → /hr/dashboard
    ├── INTERVIEWER → /interviewer/applications
    └── CANDIDATE   → /candidate/applications
```

---

## 🛡️ Authorization Flow (Phân quyền mỗi request)

```
HTTP Request (bất kỳ URL nào)
    ↓
AuthInterceptor.preHandle()
    ├── isPublicPath(path)? → true: bỏ qua, tiếp tục
    ├── AuthService.getCurrentUser(session)
    │   └── userRepository.findById(session.getAttribute("loggedInUserId"))
    ├── user == null? → redirect /login
    ├── path /admin/**?    → role != ADMIN → 403 Forbidden
    ├── path /candidate/** → role != CANDIDATE → 403 Forbidden
    ├── path /hr/** hoặc /jobs/**? → role không phải ADMIN/HR_MANAGER → 403
    └── path /applications/**? → role không phải ADMIN/HR_MANAGER/INTERVIEWER → 403
    ↓
Request tiếp tục đến Controller
```

---

## 🔒 Role-based Access Map

| Path prefix | Roles được phép |
|---|---|
| `/admin/**` | `ADMIN` |
| `/candidate/**` | `CANDIDATE` |
| `/hr/**` | `ADMIN`, `HR_MANAGER` |
| `/jobs/**` (management) | `ADMIN`, `HR_MANAGER` |
| `/jobs` (public list) | Public (không cần login) |
| `/applications/**` | `ADMIN`, `HR_MANAGER`, `INTERVIEWER` |
| `/interview/**` | `ADMIN`, `HR_MANAGER` |
| `/profile`, `/change-password` | Mọi role đã đăng nhập |

---

## 📡 GlobalModelAdvice — Inject Auth State vào View

> [!info]
> `@ControllerAdvice` tự động inject vào **mọi** Thymeleaf template:
> - `${currentUser}` — Object User đang đăng nhập (null nếu chưa login)
> - `${isAuthenticated}` — `true/false`
> - `${isAdmin}` — `true` nếu role = `ADMIN`
> - `${canAccessHr}` — `true` nếu role = `ADMIN` hoặc `HR_MANAGER`

---

## 🚪 Đăng xuất

```
POST /logout (LoginController)
    ↓
AuthService.doLogout(session)
    └── session.invalidate()
    ↓
redirect:/login
```

> [!warning]
> **Lưu ý quan trọng:**
> - User được lưu trong session bằng **userId** (không phải toàn bộ User object) để tránh stale data.
> - Mỗi request cần user data, `AuthService.getCurrentUser()` **luôn query lại DB** — đảm bảo dữ liệu luôn fresh.
> - Việc không dùng Spring Security có nghĩa là **không có CSRF protection tự động** — cần chú ý nếu mở rộng dự án.