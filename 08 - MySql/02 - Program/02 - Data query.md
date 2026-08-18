# Truy vấn Dữ liệu (DQL)

---

## Định nghĩa
Truy vấn dữ liệu là nhóm lệnh Ngôn ngữ Truy vấn Dữ liệu (DQL - Data Query Language) xoay quanh lệnh `SELECT`, được sử dụng để đọc và kết xuất thông tin từ cơ sở dữ liệu.

---

## Tác dụng
- **Lọc và tìm kiếm thông tin:** Trích xuất đúng phần dữ liệu cần thiết theo điều kiện mong muốn.
- **Tổng hợp và phân tích dữ liệu:** Sử dụng các hàm tổng hợp (`SUM`, `AVG`, `COUNT`...) kết hợp gom nhóm để đưa ra các báo cáo thống kê.
- **Liên kết nhiều bảng:** Kết nối dữ liệu từ nhiều bảng quan hệ khác nhau thông qua phép nối (`JOIN`).

---

## Bảng tham chiếu

### 1. Thứ tự viết và thứ tự thực thi của câu lệnh SQL

| Thứ tự viết trong Code | Mệnh đề (Clause) | Thứ tự thực thi của MySQL | Mô tả hoạt động |
| :---: | :--- | :---: | :--- |
| **1** | `SELECT` | **5** | Chọn các cột cần hiển thị và tính toán biểu thức |
| **2** | `FROM` | **1** | Xác định bảng nguồn hoặc thực hiện `JOIN` |
| **3** | `WHERE` | **2** | Lọc dữ liệu thô ở cấp độ hàng trước khi gom nhóm |
| **4** | `GROUP BY` | **3** | Gom các hàng có cùng giá trị cột thành các nhóm |
| **5** | `HAVING` | **4** | Lọc dữ liệu sau khi gom nhóm (dùng kèm hàm tổng hợp) |
| **6** | `ORDER BY` | **6** | Sắp xếp dữ liệu đầu ra (ASC/DESC) |
| **7** | `LIMIT` | **7** | Giới hạn số lượng bản ghi trả về |

### 2. Các loại phép JOIN

| Loại phép JOIN | Mô tả kết quả |
| :--- | :--- |
| `INNER JOIN` | Chỉ lấy các bản ghi có giá trị khớp nhau ở cả hai bảng |
| `LEFT JOIN` | Lấy toàn bộ bản ghi bảng bên trái và phần khớp ở bảng bên phải (nếu không khớp điền `NULL`) |
| `RIGHT JOIN` | Lấy toàn bộ bản ghi bảng bên phải và phần khớp ở bảng bên trái |
| `FULL JOIN` | Lấy tất cả bản ghi khi có sự khớp ở một trong hai bảng (MySQL không hỗ trợ trực tiếp, phải dùng `UNION` giữa `LEFT JOIN` và `RIGHT JOIN`) |

---

## Ví dụ

### Câu lệnh truy vấn tổng hợp phức tạp
```sql
SELECT 
    c.class_name, 
    COUNT(s.student_id) AS total_students,
    AVG(s.age) AS average_age
FROM classes c
LEFT JOIN students s ON c.class_id = s.class_id
WHERE s.age >= 10
GROUP BY c.class_id, c.class_name
HAVING total_students > 2
ORDER BY average_age DESC
LIMIT 5;
```

---

## Lưu ý
> [!important] Phân biệt WHERE và HAVING
> - Mệnh đề `WHERE` lọc dữ liệu **trước** khi tính toán gom nhóm và **không được chứa** các hàm tổng hợp (như `AVG`, `SUM`, `COUNT`).
> - Mệnh đề `HAVING` lọc dữ liệu **sau** khi gom nhóm (`GROUP BY`) và **chuyên dùng** để lọc kết quả của các hàm tổng hợp.
