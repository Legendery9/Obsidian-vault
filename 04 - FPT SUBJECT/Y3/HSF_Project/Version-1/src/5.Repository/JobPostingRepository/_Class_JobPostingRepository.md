# 🗄️ Interface: JobPostingRepository

> [!abstract] Phân loại
> **Loại:** `Repository Interface` — JPA Repository cho entity `JobPosting`.
> **Package:** `com.example.groupproject.repository`
> **Extends:** `JpaRepository<JobPosting, Integer>`

---

## 📊 Methods

### `countByStatus(JobStatus status)`
**Tác dụng:** Đếm tất cả job theo status. Dùng cho Admin dashboard (global scope).
```java
long countByStatus(JobStatus status)
```

### `countByStatusAndCreatedById(JobStatus status, Integer createdById)`
**Tác dụng:** Đếm job theo status và người tạo. Dùng cho HR dashboard (scope theo HR_MANAGER).
```java
long countByStatusAndCreatedById(JobStatus status, Integer createdById)
```

### `findActiveJobs(JobStatus status, Integer createdById)`
**Tác dụng:** Lấy danh sách job ACTIVE, sort theo deadline (null xuống cuối).
```java
@Query("""
    SELECT j FROM JobPosting j
    WHERE j.status = :status
      AND (:createdById IS NULL OR j.createdBy.id = :createdById)
    ORDER BY CASE WHEN j.applicationDeadline IS NULL THEN 1 ELSE 0 END,
             j.applicationDeadline ASC, j.title ASC
""")
List<JobPosting> findActiveJobs(@Param("status") JobStatus status,
                                @Param("createdById") Integer createdById)
```
