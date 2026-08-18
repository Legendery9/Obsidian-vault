# Spring Data JPA and Hibernate

> [!abstract] Định nghĩa
> **JPA (Java Persistence API)** là một đặc tả kỹ thuật tiêu chuẩn (specification) mô tả cách quản lý dữ liệu quan hệ trong các ứng dụng Java. 
> **Hibernate** là một thư viện cụ thể triển khai (implementation) đặc tả JPA đó.
> **Spring Data JPA** là một phần của Spring Framework giúp đơn giản hóa việc triển khai tầng dữ liệu (Repository Layer) bằng cách tự động sinh mã SQL dựa trên các thực thể (Entities) và tên phương thức.

---

## 1. So sánh JDBC vs JPA

| Tiêu chí | JDBC | Spring Data JPA |
| --- | --- | --- |
| **Cách tiếp cận** | Viết câu lệnh SQL thuần thủ công. | Làm việc hướng đối tượng thông qua thực thể (Entity). |
| **Ánh xạ kết quả (Mapping)** | Phải tự đọc `ResultSet` và map thủ công vào Object. | Khung ORM tự động ánh xạ cơ sở dữ liệu vào Class Java. |
| **Mã lặp lại (Boilerplate)** | Rất nhiều (mở connection, đóng statement, xử lý lỗi). | Hầu như không có, Spring Boot tự động quản lý kết nối. |

---

## 2. Ánh xạ thực thể (ORM Mappings)

### Khai báo Entity cơ bản
Sử dụng các annotation từ gói `jakarta.persistence` để ánh xạ Class Java thành bảng cơ sở dữ liệu:

```java
import jakarta.persistence.*;
import java.time.LocalDateTime;

@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "username", nullable = false, unique = true)
    private String username;

    // ... getter, setter, constructor rỗng bắt buộc
}
```

> [!warning] Quy tắc thực thể JPA
> Tất cả các class được đánh dấu `@Entity` bắt buộc phải khai báo một **constructor không tham số (no-argument constructor)** ở phạm vi public hoặc protected. Nếu không, Hibernate sẽ không thể khởi tạo đối tượng khi lấy dữ liệu từ DB và ném lỗi `No default constructor for entity`.

---

### Mối quan hệ giữa các thực thể (Relationships)

#### @ManyToOne và @OneToMany
Thiết lập mối quan hệ 1-N (ví dụ: Một danh mục `Category` có nhiều thiết bị `Device`).

```java
// Lớp Device (Phía Nhiều - Quản lý khóa ngoại)
@Entity
@Table(name = "devices")
public class Device {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @ManyToOne
    @JoinColumn(name = "category_id", nullable = false) // Tên cột khóa ngoại trong bảng devices
    private Category category;
}
```

```java
// Lớp Category (Phía Một - Quan hệ đảo)
@Entity
@Table(name = "categories")
public class Category {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    // mappedBy trỏ tới tên biến "category" bên trong class Device
    @OneToMany(mappedBy = "category", cascade = CascadeType.ALL)
    private List<Device> devices;
}
```

---

## 3. Lớp Repository và Derived Query Methods

Khai báo Repository bằng cách kế thừa `JpaRepository<T, ID>`:

```java
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;
import java.util.Optional;

@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    // Spring tự sinh SQL dựa theo tên method!
    Optional<User> findByUsername(String username);
    
    boolean existsByUsername(String username);
    
    long countByActiveTrue();
}
```

### Các cú pháp đặt tên truy vấn Derived Queries phổ biến:

---

### Nhóm điều kiện cơ bản

| Method/Keyword | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `findBy`, `readBy`, `queryBy`, `getBy` | Hướng truy vấn (Query Subject/Prefix). | Khởi tạo mệnh đề SELECT ... WHERE cho phương thức tìm kiếm. | Đặt ở đầu tên phương thức Repository. Ví dụ: `findByEmail(String email)`. <br> **SQL:** `WHERE email = ?` <br> **JPQL:** `select u from User u where u.email = ?1` | Tên thuộc tính theo sau tiền tố này phải được viết hoa chữ cái đầu (VD: `email` -> `Email`). |
| `And` | Phép toán logic AND kết hợp. | Nối hai hoặc nhiều điều kiện lọc, yêu cầu tất cả các điều kiện đều đúng. | Kết hợp các trường trong tên phương thức. Ví dụ: `findByLastnameAndFirstname(String ln, String fn)`. <br> **SQL:** `WHERE lastname = ? AND firstname = ?` | Số lượng tham số truyền vào phương thức phải tương ứng và đúng thứ tự với các trường khai báo. |
| `Or` | Phép toán logic OR kết hợp. | Nối hai hoặc nhiều điều kiện lọc, chỉ cần một trong các điều kiện đúng. | Kết hợp các trường trong tên phương thức. Ví dụ: `findByEmailOrUsername(String email, String username)`. <br> **SQL:** `WHERE email = ? OR username = ?` | Thứ tự các tham số phương thức cực kỳ quan trọng và phải khớp chính xác với tên điều kiện. |
| `Distinct` | Loại bỏ trùng lặp (DISTINCT modifier). | Loại bỏ các kết quả có bản ghi trùng nhau trước khi trả về. | Đặt ngay sau tiền tố truy vấn. Ví dụ: `findDistinctPeopleByLastname(String ln)`. <br> **SQL:** `SELECT DISTINCT ... WHERE lastname = ?` | Thường dùng khi thực hiện các phép truy vấn JOIN có liên kết 1-N tránh nhân bản dòng kết quả. |
| `OrderBy` | Mệnh đề sắp xếp (Sorting modifier). | Sắp xếp các kết quả tìm kiếm theo một hoặc nhiều thuộc tính tăng/giảm dần. | Đặt ở cuối tên phương thức, theo sau là tên thuộc tính và chiều sắp xếp (`Asc`/`Desc`). Ví dụ: `findByActiveTrueOrderByAgeDesc()`. <br> **SQL:** `WHERE active = true ORDER BY age DESC` | Nếu không ghi rõ `Asc` hoặc `Desc` thì Spring Data JPA mặc định sắp xếp tăng dần (`Asc`). |
| `First` / `Top` | Giới hạn số lượng kết quả (Limiting modifier). | Chỉ lấy ra N bản ghi đầu tiên thỏa mãn điều kiện truy vấn. | Đặt ở giữa tiền tố truy vấn và từ khóa `By`. Ví dụ: `findFirst3ByOrderByAgeDesc()` hoặc `findTop5ByLastname(String ln)`. <br> **SQL:** `LIMIT 3` hoặc `LIMIT 5` | Nếu chỉ viết `findFirstBy` hoặc `findTopBy` (không có số), Spring Data JPA sẽ lấy ra duy nhất 1 bản ghi đầu tiên (trả về kiểu `Optional` hoặc `Entity`). |

---

### Toán tử so sánh

| Method/Keyword | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `GreaterThan` | Toán tử so sánh lớn hơn (`>`). | Lọc các bản ghi có giá trị thuộc tính lớn hơn tham số truyền vào. | Đi kèm thuộc tính số hoặc ngày tháng. Ví dụ: `findByAgeGreaterThan(int age)`. <br> **SQL:** `WHERE age > ?` <br> **JPQL:** `select u from User u where u.age > ?1` | Không bao gồm giá trị bằng. Nếu muốn so sánh cả bằng, dùng `GreaterThanEqual`. |
| `GreaterThanEqual` | Toán tử so sánh lớn hơn hoặc bằng (`>=`). | Lọc các bản ghi có giá trị thuộc tính lớn hơn hoặc bằng tham số truyền vào. | Đi kèm thuộc tính số hoặc ngày tháng. Ví dụ: `findByAgeGreaterThanEqual(int age)`. <br> **SQL:** `WHERE age >= ?` <br> **JPQL:** `select u from User u where u.age >= ?1` | Tránh nhầm lẫn thứ tự viết keyword: `GreaterThanEqual` chứ không phải `EqualGreaterThan`. |
| `LessThan` | Toán tử so sánh nhỏ hơn (`<`). | Lọc các bản ghi có giá trị thuộc tính nhỏ hơn tham số truyền vào. | Đi kèm thuộc tính số hoặc ngày tháng. Ví dụ: `findByAgeLessThan(int age)`. <br> **SQL:** `WHERE age < ?` <br> **JPQL:** `select u from User u where u.age < ?1` | Đối với kiểu ngày tháng, có thể dùng từ khóa tương đương là `Before`. |
| `LessThanEqual` | Toán tử so sánh nhỏ hơn hoặc bằng (`<=`). | Lọc các bản ghi có giá trị thuộc tính nhỏ hơn hoặc bằng tham số truyền vào. | Đi kèm thuộc tính số hoặc ngày tháng. Ví dụ: `findByAgeLessThanEqual(int age)`. <br> **SQL:** `WHERE age <= ?` <br> **JPQL:** `select u from User u where u.age <= ?1` | Đối với kiểu ngày tháng, có thể dùng từ khóa tương đương là `After` cho chiều ngược lại. |
| `Between` | Toán tử so sánh nằm trong khoảng `[min, max]`. | Lọc các bản ghi có giá trị thuộc tính nằm giữa hai mốc (bao gồm cả biên). | Yêu cầu truyền đúng 2 tham số. Ví dụ: `findByAgeBetween(int min, int max)`. <br> **SQL:** `WHERE age BETWEEN ? AND ?` <br> **JPQL:** `select u from User u where u.age between ?1 and ?2` | Biên so sánh có tính cả điểm đầu và điểm cuối (inclusive). Tham số nhỏ hơn nên truyền trước. |
| `Before` | Toán tử so sánh thời gian trước mốc (`<`). | Lọc các bản ghi có giá trị thời gian nằm trước thời điểm chỉ định. | Dành riêng cho thuộc tính kiểu Date/Time (LocalDateTime, Instant...). Ví dụ: `findByCreatedAtBefore(LocalDateTime time)`. <br> **SQL:** `WHERE created_at < ?` | Bản chất kỹ thuật giống hệt `LessThan` nhưng mang ngữ nghĩa rõ ràng cho thời gian. |
| `After` | Toán tử so sánh thời gian sau mốc (`>`). | Lọc các bản ghi có giá trị thời gian nằm sau thời điểm chỉ định. | Dành riêng cho thuộc tính kiểu Date/Time (LocalDateTime, Instant...). Ví dụ: `findByCreatedAtAfter(LocalDateTime time)`. <br> **SQL:** `WHERE created_at > ?` | Bản chất kỹ thuật giống hệt `GreaterThan` nhưng mang ngữ nghĩa rõ ràng cho thời gian. |

---

### Kiểm tra NULL

| Method/Keyword | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `IsNull` / `Null` | Phép kiểm tra giá trị rỗng (`IS NULL`). | Lọc các bản ghi có trường dữ liệu chưa được điền giá trị (NULL). | Thường dùng cho các trường trạng thái, cờ xóa mềm. Ví dụ: `findByDeletedAtIsNull()`. <br> **SQL:** `WHERE deleted_at IS NULL` <br> **JPQL:** `select u from User u where u.deletedAt is null` | Phương thức này không nhận tham số đầu vào cho trường kiểm tra NULL. |
| `IsNotNull` / `NotNull` | Phép kiểm tra giá trị khác rỗng (`IS NOT NULL`). | Lọc các bản ghi đã được điền giá trị (khác NULL). | Ví dụ: `findByEmailIsNotNull()`. <br> **SQL:** `WHERE email IS NOT NULL` <br> **JPQL:** `select u from User u where u.email is not null` | Không nhận tham số đầu vào. Tránh nhầm lẫn viết `NotEmpty` (dành cho Collection). |

---

### Thao tác với chuỗi (String matching)

| Method/Keyword | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `Like` | Khớp mẫu chuỗi (`LIKE` operator). | Tìm kiếm chuỗi ký tự theo pattern tùy chỉnh chứa ký tự đại diện `%` hoặc `_`. | Tham số truyền vào phải tự chứa ký tự đại diện (VD: `"%John%"`). Ví dụ: `findByNameLike(String pattern)`. <br> **SQL:** `WHERE name LIKE ?` | Phải truyền thủ công ký tự `%` ở đầu/cuối của tham số khi gọi hàm. Nếu không sẽ tương đương so sánh bằng. |
| `NotLike` | Không khớp mẫu chuỗi (`NOT LIKE`). | Lọc bỏ các bản ghi khớp với mẫu chuỗi được chỉ định. | Ví dụ: `findByNameNotLike(String pattern)`. <br> **SQL:** `WHERE name NOT LIKE ?` | Giống như `Like`, tham số truyền vào cũng cần chứa ký tự đại diện `%` nếu muốn tìm kiếm tương đối. |
| `StartingWith` | Bắt đầu bằng chuỗi (Prefix match). | Tìm kiếm các chuỗi bắt đầu bằng tham số truyền vào. | Ví dụ: `findByNameStartingWith(String prefix)`. <br> **SQL:** `WHERE name LIKE 'prefix%'` <br> **JPQL:** `select u from User u where u.name like concat(?1, '%')` | Spring Data JPA tự động nối thêm `%` vào cuối tham số, lập trình viên chỉ cần truyền chuỗi thô. |
| `EndingWith` | Kết thúc bằng chuỗi (Suffix match). | Tìm kiếm các chuỗi kết thúc bằng tham số truyền vào. | Ví dụ: `findByNameEndingWith(String suffix)`. <br> **SQL:** `WHERE name LIKE '%suffix'` <br> **JPQL:** `select u from User u where u.name like concat('%', ?1)` | Spring Data JPA tự động nối `%` vào đầu tham số truyền vào. |
| `Containing` | Chứa chuỗi (Infix match). | Tìm kiếm các chuỗi có chứa tham số truyền vào ở bất kỳ vị trí nào. | Thích hợp làm chức năng tìm kiếm nhanh theo từ khóa. Ví dụ: `findByNameContaining(String keyword)`. <br> **SQL:** `WHERE name LIKE '%keyword%'` <br> **JPQL:** `select u from User u where u.name like concat('%', ?1, '%')` | Spring Data JPA tự động bao bọc tham số bằng 2 ký tự `%` ở cả đầu và cuối. |
| `IgnoreCase` | So khớp không phân biệt hoa thường. | Chuyển đổi cả hai vế so sánh về dạng chữ thường trước khi so sánh. | Đặt ở cuối tên thuộc tính. Ví dụ: `findByNameIgnoreCase(String name)`. <br> **SQL:** `WHERE LOWER(name) = LOWER(?)` <br> **JPQL:** `select u from User u where lower(u.name) = lower(?1)` | Có thể kết hợp với các toán tử chuỗi khác như `ContainingIgnoreCase`, `StartingWithIgnoreCase` để tăng tính linh hoạt. |

---

## 4. Phân trang (Pagination) và Giám sát dữ liệu (Auditing)

### Phân trang bằng `Pageable`
Tránh tải quá nhiều bản ghi lên bộ nhớ bằng cách chia trang ở phía database:

```java
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;
import org.springframework.data.domain.PageRequest;
import org.springframework.data.domain.Sort;

// Tạo yêu cầu lấy trang thứ 0, kích thước 5 bản ghi, sắp xếp theo ID giảm dần
Pageable pageable = PageRequest.of(0, 5, Sort.by("id").descending());
Page<User> userPage = userRepository.findAll(pageable);

List<User> users = userPage.getContent(); // Lấy dữ liệu thực tế của trang hiện tại
```

### Giám sát dữ liệu tự động (Auditing)
Lưu dấu vết thời gian tạo và chỉnh sửa bản ghi bằng cách kích hoạt `@EnableJpaAuditing` ở file main và khai báo thuộc tính:

```java
@CreatedDate
@Column(updatable = false)
private LocalDateTime createdAt;

@LastModifiedDate
private LocalDateTime updatedAt;
```
