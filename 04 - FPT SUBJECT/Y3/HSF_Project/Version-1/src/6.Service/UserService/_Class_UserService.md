# ⚙️ Class: UserService

> [!abstract] Phân loại
> **Loại:** `Service Class` — Các thao tác cơ bản trên User entity.
> **Package:** `com.example.groupproject.service`
> **Annotation:** `@Service @Transactional(readOnly = true)`

---

## 💉 Dependencies (Inject)

- `UserRepository userRepository` — truy vấn user theo username hoặc ID

---

## 📊 Methods

### `getByUsername(String username)`

```java
public User getByUsername(String username)
```

Tìm User theo username. **Return:** `User` hoặc `null`

### `getById(Integer id)`

```java
public User getById(Integer id)
```

Tìm User theo ID. **Return:** `User` hoặc `null`

> [!note] Về vai trò
> `UserService` cung cấp các query cơ bản. Logic phức tạp hơn (tạo, unlock, deactivate) thuộc về `UserManagementService`. Xác thực session thuộc về `AuthService`.
