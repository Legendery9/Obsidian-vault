# Truy vấn Database trong Java với @Query

---

## Định nghĩa
`@Query` là một annotation trong Spring Data JPA dùng để định nghĩa các câu lệnh truy vấn dữ liệu tùy chỉnh (JPQL/HQL hoặc SQL thuần) trực tiếp trên các phương thức của interface Repository trong ứng dụng Java.

---

## Tác dụng
- **Viết truy vấn phức tạp:** Giải quyết các bài toán truy vấn lồng nhau, join nhiều bảng phức tạp mà cơ chế sinh query tự động của Spring Data JPA (Query Method) không hỗ trợ hoặc viết quá dài.
- **Tối ưu hiệu năng:** Cho phép viết SQL thuần (Native Query) để tận dụng tối đa các tính năng đặc thù của MySQL (như Index, Stored Procedure, Json Query).

---

## Bảng tham chiếu

### So sánh JPQL (Mặc định) và Native Query (SQL thuần)

| Tiêu chí | JPQL (Java Persistence Query Language) | Native Query (SQL thuần) |
| :--- | :--- | :--- |
| **Đối tượng hướng tới** | Hướng đối tượng (truy vấn trên **Entity Class** và các thuộc tính của Java Class). | Hướng cơ sở dữ liệu (truy vấn trực tiếp trên **Table** và các **Cột** trong DB). |
| **Tính độc lập DB** | **Cao:** Tự động dịch sang SQL tương ứng của hệ quản trị DB đang dùng (MySQL, PostgreSQL, Oracle...). | **Thấp:** Phụ thuộc hoàn toàn vào cú pháp của DB cụ thể (ví dụ: dùng hàm MySQL thì sang Oracle có thể lỗi). |
| **Khai báo trong Code** | `@Query("SELECT u FROM User u WHERE u.email = :email")` | `@Query(value = "SELECT * FROM users WHERE email = :email", nativeQuery = true)` |
| **Hỗ trợ hàm đặc thù** | Hạn chế, chỉ hỗ trợ các hàm chung của chuẩn JPA. | Đầy đủ, hỗ trợ mọi hàm, trigger, json và cú pháp riêng của DB. |

---

## Ví dụ

### 1. Truy vấn bằng JPQL (Truy vấn trên Class `Student` Entity)
```java
package com.example.repository;

import com.example.entity.Student;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.query.Param;
import java.util.List;

public interface StudentRepository extends JpaRepository<Student, Long> {

    // JPQL sử dụng tên Class Entity (Student) và tên biến thuộc tính (fullName)
    @Query("SELECT s FROM Student s WHERE s.fullName LIKE %:name% AND s.age >= :minAge")
    List<Student> findStudentsByNameAndAge(
        @Param("name") String name, 
        @Param("minAge") int minAge
    );
}
```

### 2. Truy vấn bằng Native Query (Truy vấn trên Bảng `students` vật lý của MySQL)
```java
package com.example.repository;

import com.example.entity.Student;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.query.Param;
import java.util.List;

public interface StudentRepository extends JpaRepository<Student, Long> {

    // Native Query viết SQL thuần với tên bảng 'students' và các cột vật lý
    @Query(
        value = "SELECT * FROM students WHERE class_id = :classId ORDER BY created_at DESC", 
        nativeQuery = true
    )
    List<Student> findByClassIdNative(@Param("classId") Long classId);
}
```

---

## Lưu ý
> [!warning] Rủi ro bảo mật SQL Injection
> Tránh nối chuỗi trực tiếp trong câu lệnh `@Query` (Ví dụ: `value = "SELECT * FROM students WHERE name = " + input`). Luôn sử dụng kỹ thuật liên kết tham số (Named Parameters) bằng cú pháp `:parameterName` kết hợp `@Param` hoặc định vị tham số `?1`, `?2` để JPA tự động bảo vệ ứng dụng khỏi lỗ hổng SQL Injection.
