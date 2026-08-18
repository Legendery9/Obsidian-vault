# Function và Stored Procedure (Chương trình con)

---

## Định nghĩa
Function (Hàm) và Stored Procedure (Thủ tục lưu trữ) là các khối lệnh SQL được biên dịch trước và lưu trữ tập trung trên cơ sở dữ liệu, cho phép tái sử dụng logic xử lý nhiều lần.

---

## Tác dụng
- **Tái sử dụng mã nguồn:** Tránh viết đi viết lại cùng một logic xử lý SQL ở nhiều nơi trong ứng dụng.
- **Giảm băng thông mạng:** Ứng dụng chỉ cần gửi lệnh gọi tên hàm/thủ tục thay vì gửi cả đoạn script SQL dài qua mạng.
- **Tăng tính bảo mật:** Phân quyền cho người dùng chỉ được gọi thủ tục mà không cần cấp quyền truy cập trực tiếp vào các bảng dữ liệu bên dưới.

---

## Bảng tham chiếu

### So sánh Function và Stored Procedure

| Tiêu chí so sánh | Function (Hàm) | Stored Procedure (Thủ tục) |
| :--- | :--- | :--- |
| **Giá trị trả về** | **Bắt buộc** trả về duy nhất một giá trị (`RETURNS type` và `RETURN val`). | Không bắt buộc trả về giá trị trực tiếp (Dùng tham số `OUT`/`INOUT` hoặc trả về tập kết quả). |
| **Tham số truyền vào**| Chỉ nhận tham số đầu vào (mặc định là `IN`). | Hỗ trợ 3 loại tham số:<br>- `IN`: Tham số truyền vào<br>- `OUT`: Tham số đầu ra<br>- `INOUT`: Cả hai |
| **Cách gọi sử dụng** | Gọi trực tiếp trong câu lệnh SQL (Ví dụ: `SELECT my_func(col) FROM tbl`). | Phải sử dụng từ khóa `CALL` (Ví dụ: `CALL my_proc(param)`). |
| **Lệnh DML bên trong** | Hạn chế thao tác thay đổi dữ liệu bảng (như `INSERT`, `UPDATE`, `DELETE`) để tránh hiệu ứng phụ (side effects). | Thoải mái thực thi các lệnh DML và quản lý giao dịch (`COMMIT`, `ROLLBACK`). |

---

## Ví dụ

### 1. Tạo và sử dụng Stored Procedure (Có tham số IN và OUT)
Thủ tục lấy tổng số học sinh của một lớp học:
```sql
DELIMITER $$

CREATE PROCEDURE GetStudentCountByClass(
    IN input_class_id INT,
    OUT total_students INT
)
BEGIN
    SELECT COUNT(*) 
    INTO total_students
    FROM students
    WHERE class_id = input_class_id;
END$$

DELIMITER ;

-- Cách gọi sử dụng Stored Procedure trong SQL:
CALL GetStudentCountByClass(1, @count);
SELECT @count AS Class_1_Total;
```

### 2. Tạo và sử dụng Function (Hàm trả về giá trị)
Hàm phân loại học lực dựa trên điểm số:
```sql
DELIMITER $$

CREATE FUNCTION EvaluateGrade(score DECIMAL(3,1))
RETURNS VARCHAR(20)
DETERMINISTIC
BEGIN
    DECLARE result VARCHAR(20);
    
    IF score >= 8.0 THEN
        SET result = 'Giỏi';
    ELSEIF score >= 6.5 THEN
        SET result = 'Khá';
    ELSEIF score >= 5.0 THEN
        SET result = 'Trung bình';
    ELSE
        SET result = 'Yếu';
    END IF;
    
    RETURN result;
END$$

DELIMITER ;

-- Cách sử dụng Function trực tiếp trong câu SELECT:
SELECT full_name, EvaluateGrade(9.2) AS grade FROM students;
```

---

## Lưu ý
> [!important] Từ khóa DETERMINISTIC
> Khi định nghĩa Function trong MySQL, bạn cần khai báo tính chất của hàm:
> - `DETERMINISTIC`: Hàm luôn trả về cùng một kết quả với cùng một tham số truyền vào.
> - `NOT DETERMINISTIC` (Mặc định): Kết quả trả về có thể thay đổi ở mỗi lần gọi cho dù tham số truyền vào giống nhau (ví dụ: hàm có chứa lệnh lấy thời gian thực hoặc gọi hàm ngẫu nhiên).
