# ⚙️ Class: UserManagementService

> [!abstract] Phân loại
> **Loại:** `Service Class` — Quản lý vòng đời tài khoản người dùng (Admin use cases).
> **Package:** `com.example.groupproject.service`
> **Annotation:** `@Service`

---

## 💉 Dependencies (Inject)

- `UserRepository userRepository` — CRUD operations trên bảng `users`
- `ActivityLogRepository activityLogRepository` — ghi log sau mỗi thao tác quản trị

---

## 📌 Hằng số

```java
private static final Set<UserRole> CREATABLE_ROLES = Set.of(UserRole.HR_MANAGER, UserRole.INTERVIEWER);
```

Chỉ Admin được tạo 2 role này (không được tạo ADMIN hoặc CANDIDATE).

---

## 📊 Methods

### `searchUsers(String search, UserRole role, UserStatus status)`

```java
@Transactional(readOnly = true)
public List<User> searchUsers(String search, UserRole role, UserStatus status)
```

Tìm kiếm user với filter linh hoạt: tên/email, role, status. Dùng cho trang admin/users.
- **Return:** `List<User>`

---

### `createUser(CreateUserForm form, User actor)`

```java
@Transactional
public User createUser(CreateUserForm form, User actor)
```

Tạo tài khoản mới (chỉ HR_MANAGER hoặc INTERVIEWER). Kiểm tra duplicate username/email. Ghi activity log `ACCOUNT_CREATED`.
- **Return:** `User` (entity vừa tạo)

---

### `unlockUser(Integer userId, User actor)`

```java
@Transactional
public void unlockUser(Integer userId, User actor)
```

Mở khóa tài khoản bị LOCKED: reset `status=ACTIVE`, `failedLoginCount=0`, `lockedAt=null`. Ghi log `ACCOUNT_UNLOCKED`.
- **Return:** `void`

---

### `deactivateUser(Integer userId, User actor)`

```java
@Transactional
public void deactivateUser(Integer userId, User actor)
```

Vô hiệu hóa tài khoản (ACTIVE/LOCKED → INACTIVE). Không cho xóa admin cuối cùng. Ghi log `ACCOUNT_DEACTIVATED`.
- **Return:** `void`

---

### `canDeactivate(User user)` & `canUnlock(User user)`

```java
public boolean canDeactivate(User user)
public boolean canUnlock(User user)
```

Kiểm tra xem có thể thực hiện thao tác không (dùng để hiển/ẩn nút trong UI).
- **Return:** `boolean`
