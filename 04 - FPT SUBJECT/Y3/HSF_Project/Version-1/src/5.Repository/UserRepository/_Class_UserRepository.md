# 🗄️ Interface: UserRepository

> [!abstract] Phân loại
> **Loại:** `Repository Interface` — JPA Repository cho entity `User`.
> **Package:** `com.example.groupproject.repository`
> **Extends:** `JpaRepository<User, Integer>` (có sẵn CRUD: save, findById, findAll, delete...)

---

## 💉 Không cần inject — Spring tự tạo bean

---

## 📊 Methods

### `findByUsername(String username)`
**Tác dụng:** Tìm user theo username (duy nhất). Dùng bởi `AuthService` khi đăng nhập.
```java
User findByUsername(String username)  // Return: User | null
```

### `findByEmail(String email)`
**Tác dụng:** Kiểm tra trùng email khi tạo tài khoản.
```java
User findByEmail(String email)  // Return: User | null
```

### `countByRole(UserRole role)`, `countByStatus(UserStatus status)`, `countByRoleAndStatus(...)`
**Tác dụng:** Đếm users theo tiêu chí — dùng cho admin dashboard stats.
```java
long countByRole(UserRole role)
long countByStatus(UserStatus status)
long countByRoleAndStatus(UserRole role, UserStatus status)
```

### `searchUsers(String search, UserRole role, UserStatus status)`
**Tác dụng:** Tìm kiếm user với 3 filter tùy chọn (null = bỏ qua filter đó).
```java
@Query("""
    SELECT u FROM User u
    WHERE (:search IS NULL OR :search = ''
           OR LOWER(u.fullName) LIKE LOWER(CONCAT('%', :search, '%'))
           OR LOWER(u.email) LIKE LOWER(CONCAT('%', :search, '%')))
      AND (:role IS NULL OR u.role = :role)
      AND (:status IS NULL OR u.status = :status)
    ORDER BY u.createdAt DESC
""")
List<User> searchUsers(@Param("search") String search,
                       @Param("role") UserRole role,
                       @Param("status") UserStatus status)
```
