# ⚙️ Class: AuthService

> [!abstract] Phân loại
> **Loại:** `Service Class` — Xử lý xác thực (Authentication) và phân quyền (Authorization) dựa trên session.
> **Package:** `com.example.groupproject.service`
> **Annotation:** `@Service`

---

## 💉 Dependencies (Inject)

- `UserRepository userRepository` — truy vấn database để load User entity theo username hoặc ID

---

## 📌 Hằng số

```java
public static final String SESSION_USER_ID = "loggedInUserId";
```

Khóa lưu user ID vào HttpSession.

---

## 📊 Methods

### `getCurrentUser(HttpSession session)`

> [!note] Lấy user đang đăng nhập từ session

```java
@Transactional(readOnly = true)
public User getCurrentUser(HttpSession session)
```

- Lấy `loggedInUserId` từ session → query DB bằng `userRepository.findById()`
- **Return:** `User` hoặc `null` (nếu chưa đăng nhập)

---

### `login(String username, String password, HttpSession session)`

> [!note] Xác thực đăng nhập

```java
@Transactional
public boolean login(String username, String password, HttpSession session)
```

**Logic:**
1. Tìm user theo username (`findByUsername`)
2. Kiểm tra `status == ACTIVE`
3. So sánh password plain-text
4. Nếu đúng: lưu `userId` vào session

> [!warning] Bảo mật
> Password đang so sánh plain-text, không hash. Cần cải thiện bằng BCrypt trong production.

- **Return:** `boolean` — `true` nếu đăng nhập thành công

---

### `logout(HttpSession session)`

```java
public void logout(HttpSession session)
```

Gọi `session.invalidate()` để hủy toàn bộ session. **Return:** `void`

---

### `isAuthenticated(HttpSession session)`

```java
public boolean isAuthenticated(HttpSession session)
```

Kiểm tra session có user hợp lệ không. **Return:** `boolean`

---

### `hasRole(User user, UserRole role)` & `hasAnyRole(User user, UserRole... roles)`

```java
public boolean hasRole(User user, UserRole role)
public boolean hasAnyRole(User user, UserRole... roles)
```

Kiểm tra user có role cụ thể không. **Return:** `boolean`

---

### `requireAuthenticated(User user)` / `requireRole(...)` / `requireAnyRole(...)`

```java
public void requireAuthenticated(User user)  // throws IllegalStateException nếu null
public void requireRole(User user, UserRole role)  // throws nếu sai role
public void requireAnyRole(User user, UserRole... roles)  // throws nếu không có role nào
```

Các guard method: ném `IllegalStateException` nếu điều kiện không thỏa mãn. Dùng trong Controllers để bảo vệ endpoint.
