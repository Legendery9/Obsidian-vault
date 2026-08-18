# Kiểu Dữ liệu trong MySQL

---

## Định nghĩa
Kiểu dữ liệu trong MySQL xác định loại dữ liệu (như số, chuỗi, ngày tháng, nhị phân, JSON) mà một cột trong bảng có thể lưu trữ, đồng thời quyết định dung lượng bộ nhớ được cấp phát cho cột đó.

---

## Tác dụng
- **Tối ưu hóa bộ nhớ lưu trữ:** Chọn đúng kiểu dữ liệu giúp tiết kiệm dung lượng đĩa cứng và tăng tốc độ đọc/ghi.
- **Bảo vệ tính toàn vẹn dữ liệu:** Ngăn chặn việc nhập sai định dạng dữ liệu (ví dụ: nhập chữ vào cột chứa ngày tháng).
- **Hỗ trợ tính toán:** Đảm bảo các hàm toán học hoặc xử lý chuỗi hoạt động chính xác.

---

## Bảng tham chiếu

### Phân loại các kiểu dữ liệu phổ biến trong MySQL

| Phân nhóm | Kiểu dữ liệu | Phạm vi / Dung lượng | Ứng dụng thực tế |
| :--- | :--- | :--- | :--- |
| **Số nguyên** | `TINYINT` | 1 byte (-128 đến 127) | Lưu trữ trạng thái (Ví dụ: `status` 0/1/2), tuổi tác |
| | `INT` / `INTEGER` | 4 bytes (khoảng -2 tỷ đến 2 tỷ) | ID tự tăng thông thường, số đếm |
| | `BIGINT` | 8 bytes (cực kỳ lớn) | ID của hệ thống dữ liệu lớn (Big Data) |
| **Số thực** | `FLOAT` | 4 bytes | Tọa độ GPS, số thực không yêu cầu chính xác tuyệt đối |
| | `DOUBLE` | 8 bytes | Tính toán khoa học thông thường |
| | `DECIMAL(p, s)` | Thay đổi (Chính xác tuyệt đối) | **Lưu trữ tiền tệ**, điểm số cần chính xác cao |
| **Chuỗi ký tự** | `CHAR(N)` | Độ dài cố định (0 đến 255) | Lưu mã bưu điện, mã quốc gia, mã hash cố định |
| | `VARCHAR(N)` | Độ dài thay đổi (0 đến 65,535) | Lưu tên, địa chỉ, email, mô tả ngắn |
| | `TEXT` | Tối đa 65,535 ký tự | Lưu nội dung bài viết, tài liệu dài |
| **Ngày giờ** | `DATE` | Định dạng `YYYY-MM-DD` | Lưu ngày sinh, ngày kỷ niệm (không cần giờ) |
| | `DATETIME` | Định dạng `YYYY-MM-DD HH:MM:SS` | Lưu mốc thời gian độc lập với múi giờ |
| | `TIMESTAMP` | Định dạng tương tự `DATETIME` | Tự động chuyển đổi theo múi giờ (Timezone-aware) |
| **JSON** | `JSON` | Tối đa bằng kích thước gói tin | Lưu dữ liệu động, cấu hình bán cấu trúc (Semi-structured) |

---

## Ví dụ

### Cách khai báo và sử dụng các kiểu dữ liệu trong SQL
```sql
CREATE TABLE products (
    product_id BIGINT AUTO_INCREMENT PRIMARY KEY,
    product_name VARCHAR(150) NOT NULL,
    product_code CHAR(8) NOT NULL UNIQUE,     -- Ví dụ: PRD10023
    price DECIMAL(10, 2) NOT NULL,            -- Lưu tối đa 99.999.999,99
    description TEXT,
    attributes JSON,                          -- Lưu trữ thuộc tính động dạng JSON
    expiry_date DATE,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

---

## Lưu ý
> [!important] Quy tắc chọn kiểu dữ liệu tối ưu
> - **Tiền tệ:** Luôn sử dụng kiểu `DECIMAL` để lưu trữ tiền tệ. Tuyệt đối không dùng `FLOAT` hay `DOUBLE` vì chúng sẽ gây ra sai số làm tròn khi thực hiện các phép toán cộng trừ.
> - **CHAR vs VARCHAR:** Dùng `CHAR` cho các cột có độ dài chuỗi luôn cố định (ví dụ: mã quốc gia 2 ký tự như 'VN', 'US'). Dùng `VARCHAR` cho các chuỗi có độ dài thay đổi để tiết kiệm không gian bộ nhớ.
