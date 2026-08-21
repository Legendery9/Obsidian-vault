[Microsoft Learn - Repository Pattern](https://learn.microsoft.com/en-us/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application) | [Baeldung - DAO vs Repository](https://www.baeldung.com/java-spring-semantical-difference-between-repository-and-dao)

# Repository Pattern

---

## Định nghĩa

**Repository Pattern** là một mẫu thiết kế (Design Pattern) đóng vai trò là một lớp trung gian nằm giữa tầng xử lý nghiệp vụ (Business Logic Layer) và tầng truy cập dữ liệu (Data Access / Infrastructure Layer). Nó cung cấp một giao diện giống như một bộ sưu tập các đối tượng nghiệp vụ trong bộ nhớ (In-memory collection), giúp ẩn đi các chi tiết kỹ thuật phức tạp của việc truy vấn cơ sở dữ liệu.

---

## Đặc đặc điểm chính

- **Trừu tượng hóa truy cập dữ liệu:** Lớp Service hoàn toàn không biết cơ sở dữ liệu bên dưới là gì (SQL, NoSQL, File hệ thống) hay dùng thư viện nào (Hibernate, JDBC, Entity Framework). Nó chỉ tương tác qua Interface.
- **Tập trung hóa logic truy vấn:** Mọi câu lệnh SQL, HQL hoặc truy vấn Linq đều được gom nhóm tại một nơi duy nhất (Repository Implementation).
- **Mô phỏng bộ sưu tập:** Repository cung cấp các phương thức CRUD cơ bản như `add()`, `remove()`, `get()`, `find()` tương tự như đang thao tác với một List hoặc Set.

---

## FLOW trực quan

Sơ đồ Mermaid dưới đây mô tả luồng tương tác khi Service yêu cầu lấy dữ liệu thông qua Interface Repository:

```mermaid
sequenceDiagram
    autonumber
    participant Service as Business Service
    participant RepoInterface as Repository Interface
    participant RepoImpl as Repository Implementation
    database DB as SQL Database

    Service->>RepoInterface: Gọi findById(id)
    Note over RepoInterface: Trừu tượng hóa
    RepoInterface->>RepoImpl: Chuyển tiếp lời gọi
    RepoImpl->>DB: Thực thi truy vấn (SELECT * FROM...)
    DB-->>RepoImpl: Trả về tập kết quả ResultSet
    RepoImpl->>RepoImpl: Ánh xạ kết quả thành Entity Object (ORM)
    RepoImpl-->>Service: Trả về Domain Object (ví dụ: Student)
```

---

## Ưu điểm / Nhược điểm

> [!info] **Bảng so sánh chi tiết**
>
> | Tiêu chí | Ưu điểm | Nhược điểm |
> | :--- | :--- | :--- |
> | **Tính dễ kiểm thử (Testability)** | Dễ dàng Mock Repository Interface để viết Unit Test cho tầng Service mà không cần kết nối tới Database thật. | Tăng số lượng file code (phải tạo cả Interface và Implementation class). |
> | **Độc lập công nghệ** | Dễ dàng thay đổi thư viện truy xuất cơ sở dữ liệu (ví dụ từ JDBC sang JPA) hoặc chuyển đổi database mà không phải sửa code tầng Service. | Gây hiểu lầm: Dễ viết các câu truy vấn không tối ưu (N+1 query problem) do ẩn đi cách thức thực thi SQL bên dưới. |
> | **Tái sử dụng** | Tránh lặp lại các câu truy vấn phức tạp ở nhiều nơi trong hệ thống. | Tạo ra một lớp trung gian không cần thiết đối với các ứng dụng CRUD siêu đơn giản. |

---

## Khi nào nên dùng

- Ứng dụng có Business Logic phức tạp và thường xuyên thay đổi.
- Dự án áp dụng phương pháp Domain-Driven Design (DDD), trong đó Domain Model là trung tâm và cần được cô lập hoàn toàn khỏi Database.
- Khi muốn viết Unit Test chất lượng cao cho tầng Service.
- Dự án có khả năng thay đổi công nghệ lưu trữ dữ liệu trong tương lai.

---

## Ví dụ minh hoá

Trong Java Spring Boot, ta sử dụng **Spring Data JPA** để tự động sinh ra các cài đặt của Repository Pattern:

- **Định nghĩa Repository Interface:**
  ```java
  public interface StudentRepository extends JpaRepository<Student, Long> {
      // Spring Data JPA sẽ tự động tạo câu truy vấn SQL tìm theo email
      Optional<Student> findByEmail(String email);
  }
  ```
- **Sử dụng trong Service:**
  ```java
  @Service
  public class StudentService {
      @Autowired
      private StudentRepository studentRepository;

      public Student getStudentByEmail(String email) {
          return studentRepository.findByEmail(email)
                  .orElseThrow(() -> new EntityNotFoundException("Student not found"));
      }
  }
  ```
> [!note] 
> Chi tiết cách sử dụng Spring Data JPA, cấu hình Entity, Hibernate và các phương thức truy vấn nâng cao có sẵn tại file `[[01 - Spring Data JPA and Hibernate]]` trong vault.

---

## Lưu ý

- **Phân biệt DAO vs Repository:**
  - **DAO (Data Access Object)** là một lớp bao bọc xung quanh một bảng cơ sở dữ liệu cụ thể, cung cấp các thao tác CRUD cấp thấp trực tiếp trên bảng đó.
  - **Repository** hoạt động ở cấp độ cao hơn (Domain Level). Nó quản lý một **Aggregate Root** (một nhóm các thực thể liên quan chặt chẽ) và tập trung vào nghiệp vụ hơn là vào bảng dữ liệu vật lý. Một Repository có thể sử dụng nhiều DAO bên trong để hoàn thành nhiệm vụ.
- **Kết hợp Unit of Work:** Repository Pattern thường đi kèm với **Unit of Work Pattern** để quản lý các Transactions, đảm bảo nhiều thao tác ghi dữ liệu trên các Repository khác nhau được thực hiện thành công cùng nhau (Atomicity) hoặc Rollback hoàn toàn nếu xảy ra lỗi.
