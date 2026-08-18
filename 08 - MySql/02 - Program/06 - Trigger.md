# Trigger trong MySQL

---

## Định nghĩa
Trigger là một khối mã SQL được đặt tên và lưu trữ trong cơ sở dữ liệu, tự động kích hoạt (execute) để thực thi khi có một sự kiện thao tác dữ liệu (DML: `INSERT`, `UPDATE`, `DELETE`) xảy ra trên một bảng cụ thể.

---

## Tác dụng
- **Tự động hóa ghi log:** Lưu vết lịch sử thay đổi của dữ liệu (Auditing).
- **Ràng buộc nghiệp vụ phức tạp:** Kiểm tra và thực thi các luật nghiệp vụ mà ràng buộc thường (`CHECK`) không làm được (ví dụ: so sánh dữ liệu giữa nhiều bảng).
- **Đồng bộ hóa dữ liệu:** Tự động tính toán hoặc cập nhật số liệu ở bảng khác khi bảng hiện tại thay đổi.

---

## Bảng tham chiếu

### Phân loại các loại Trigger theo sự kiện

| Thời điểm kích hoạt | Sự kiện thao tác | Phạm vi áp dụng | Đối tượng truy cập dữ liệu |
| :--- | :--- | :--- | :--- |
| **`BEFORE`** | `INSERT` | Chạy trước khi dữ liệu được ghi vào đĩa. Thường dùng để chuẩn hóa dữ liệu hoặc kiểm tra hợp lệ. | Sử dụng biến: <br>- `NEW.column_name` (giá trị chuẩn bị ghi) |
| | `UPDATE` | Chạy trước khi cập nhật. | Sử dụng biến:<br>- `OLD.column_name` (giá trị cũ)<br>- `NEW.column_name` (giá trị mới sẽ cập nhật) |
| | `DELETE` | Chạy trước khi xóa dòng dữ liệu. | Sử dụng biến:<br>- `OLD.column_name` (giá trị sắp xóa) |
| **`AFTER`** | `INSERT` | Chạy sau khi dữ liệu đã được ghi vào bảng. Thường dùng để cập nhật bảng khác hoặc ghi log. | Sử dụng biến `NEW.column_name` (chỉ đọc) |
| | `UPDATE` | Chạy sau khi cập nhật dữ liệu thành công. | Sử dụng biến `OLD` và `NEW` (chỉ đọc) |
| | `DELETE` | Chạy sau khi dòng dữ liệu đã bị xóa khỏi bảng. | Sử dụng biến `OLD.column_name` (chỉ đọc) |

---

## Ví dụ

### Kịch bản: Tự động ghi log lịch sử và cập nhật số lượng khi có đơn hàng mới

#### 1. Chuẩn bị bảng dữ liệu
```sql
CREATE TABLE inventory (
    item_id INT PRIMARY KEY,
    item_name VARCHAR(100),
    stock_quantity INT
);

CREATE TABLE orders (
    order_id INT AUTO_INCREMENT PRIMARY KEY,
    item_id INT,
    order_quantity INT,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### 2. Tạo Trigger cập nhật số lượng kho sau khi chèn đơn hàng
```sql
DELIMITER $$

CREATE TRIGGER after_order_insert
AFTER INSERT ON orders
FOR EACH ROW
BEGIN
    -- Trừ số lượng hàng trong kho dựa trên đơn hàng mới
    UPDATE inventory 
    SET stock_quantity = stock_quantity - NEW.order_quantity
    WHERE item_id = NEW.item_id;
END$$

DELIMITER ;
```

---

## Lưu ý
> [!caution] Nhược điểm và hạn chế của Trigger
> - **Hiệu năng:** Trigger chạy ngầm trên mỗi dòng dữ liệu (`FOR EACH ROW`). Nếu thực hiện các truy vấn lồng nhau phức tạp bên trong Trigger, hiệu năng của câu lệnh `INSERT`/`UPDATE` gốc sẽ bị giảm nghiêm trọng.
> - **Khó debug:** Do Trigger tự động chạy ngầm, lập trình viên ứng dụng khó theo dõi luồng thực thi dữ liệu, dẫn đến khó tìm nguyên nhân khi xảy ra lỗi logic dữ liệu.
