# 🗄️ Interface: InterviewRepository

> [!abstract] Phân loại
> **Loại:** `Repository Interface` — JPA Repository cho entity `Interview`.
> **Package:** `com.example.groupproject.repository`
> **Extends:** `JpaRepository<Interview, Integer>`

---

## 📊 Methods

### `countUpcomingScoped(LocalDate from, LocalDate to, Integer createdById)`
**Tác dụng:** Đếm interview sắp diễn ra trong khoảng `[from, to]`, có scope theo người tạo job. Dùng cho dashboard stat "Upcoming Interviews (7 days)".

```java
@Query("""
    SELECT COUNT(i) FROM Interview i
    WHERE i.interviewDate BETWEEN :from AND :to
      AND (:createdById IS NULL OR i.application.job.createdBy.id = :createdById)
""")
long countUpcomingScoped(@Param("from") LocalDate from,
                         @Param("to") LocalDate to,
                         @Param("createdById") Integer createdById)
```

| Tham số | Kiểu | Mô tả |
|---------|------|-------|
| `from` | `LocalDate` | Ngày bắt đầu (today) |
| `to` | `LocalDate` | Ngày kết thúc (today + 7) |
| `createdById` | `Integer` | null = tất cả, không null = scope theo HR |
