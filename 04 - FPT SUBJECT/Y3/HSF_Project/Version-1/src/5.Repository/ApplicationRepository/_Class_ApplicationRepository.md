# 🗄️ Interface: ApplicationRepository

> [!abstract] Phân loại
> **Loại:** `Repository Interface` — JPA Repository cho entity `Application`.
> **Package:** `com.example.groupproject.repository`
> **Extends:** `JpaRepository<Application, Integer>`

---

## 📊 Methods

### `countByStatus(ApplicationStatus status)`
**Tác dụng:** Đếm application theo status (global, dùng cho admin).
```java
long countByStatus(ApplicationStatus status)
```

### `countByStatusScoped(ApplicationStatus status, Integer createdById)`
**Tác dụng:** Đếm application theo status, có scope theo người tạo job. Dùng cho HR dashboard.
```java
@Query("""
    SELECT COUNT(a) FROM Application a
    WHERE a.status = :status
      AND (:createdById IS NULL OR a.job.createdBy.id = :createdById)
""")
long countByStatusScoped(@Param("status") ApplicationStatus status,
                         @Param("createdById") Integer createdById)
```
