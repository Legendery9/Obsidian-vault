# Tạo và Cấu hình Bảng (DDL)

---

## Định nghĩa
Tạo và cấu hình bảng là nhóm lệnh Định nghĩa Dữ liệu (DDL - Data Definition Language) dùng để khởi tạo, thay đổi hoặc xóa bỏ các cấu trúc dữ liệu (Database, Schema, Table, Index) trong hệ quản trị cơ sở dữ liệu.

---

## Tác dụng
- **Xây dựng cấu trúc lưu trữ:** Thiết lập các cột, kiểu dữ liệu tương ứng và các ràng buộc (Constraints).
- **Đảm bảo toàn vẹn dữ liệu:** Sử dụng các khóa chính (Primary Key), khóa ngoại (Foreign Key), ràng buộc duy nhất (Unique), ràng buộc kiểm tra (Check).

---

## Bảng tham chiếu

### Các câu lệnh DDL cốt lõi

| Cú pháp SQL | Tác dụng | Lưu ý |
| :--- | :--- | :--- |
| `CREATE DATABASE db_name;` | Tạo một database mới | Có thể dùng `CREATE SCHEMA` thay thế |
| `USE db_name;` | Chọn database làm việc mặc định | Phải chạy trước khi thao tác trên bảng |
| `CREATE TABLE tbl_name (...);` | Tạo một bảng mới với cấu trúc cột | Cần định nghĩa khóa chính (PK) |
| `ALTER TABLE tbl_name ADD ...;` | Thêm cột hoặc ràng buộc mới vào bảng | Không làm mất dữ liệu cũ |
| `ALTER TABLE tbl_name MODIFY ...;` | Thay đổi kiểu dữ liệu của một cột | Cẩn thận nếu độ dài mới nhỏ hơn dữ liệu hiện tại |
| `ALTER TABLE tbl_name DROP ...;` | Xóa một cột hoặc ràng buộc | Dữ liệu trên cột đó sẽ bị xóa vĩnh viễn |
| `DROP TABLE tbl_name;` | Xóa bỏ hoàn toàn bảng và toàn bộ dữ liệu | Không thể hoàn tác (Rollback) |
| `TRUNCATE TABLE tbl_name;` | Xóa sạch toàn bộ dữ liệu trong bảng | Nhanh hơn lệnh `DELETE` vì không ghi log từng dòng |

---

## Ví dụ

### Cú pháp tạo bảng hoàn chỉnh với các ràng buộc
```sql
-- 1. Tạo database và sử dụng
CREATE DATABASE IF NOT EXISTS school_db;
USE school_db;

-- 2. Tạo bảng lớp học (bảng cha)
CREATE TABLE IF NOT EXISTS classes (
    class_id INT AUTO_INCREMENT PRIMARY KEY,
    class_name VARCHAR(50) NOT NULL UNIQUE
);

-- 3. Tạo bảng học sinh (bảng con có khóa ngoại)
CREATE TABLE IF NOT EXISTS students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    full_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    age INT CHECK (age >= 6 AND age <= 18),
    class_id INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    
    -- Định nghĩa khóa ngoại liên kết tới bảng classes
    FOREIGN KEY (class_id) REFERENCES classes(class_id) 
        ON DELETE SET NULL 
        ON UPDATE CASCADE
);
```

---

## Lưu ý
> [!caution] Hành động xóa dữ liệu nguy hiểm
> Lệnh `DROP TABLE` và `TRUNCATE TABLE` là các thao tác DDL tự động commit ngay lập tức (Auto-commit) và **không thể phục hồi** bằng lệnh `ROLLBACK`. Hãy cực kỳ cẩn thận khi thực thi trên môi trường Production!
