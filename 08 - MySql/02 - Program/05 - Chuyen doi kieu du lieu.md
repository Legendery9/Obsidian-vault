# Chuyển đổi Kiểu dữ liệu (CAST / CONVERT)

---

## Định nghĩa
Chuyển đổi kiểu dữ liệu là quá trình biến đổi giá trị từ kiểu dữ liệu này sang kiểu dữ liệu khác (ví dụ: chuyển từ chuỗi ký tự sang số nguyên hoặc ngày tháng) trong MySQL, bao gồm chuyển đổi tường minh (Explicit) và ngầm định (Implicit).

---

## Tác dụng
- **Chuẩn hóa dữ liệu trong truy vấn:** Giúp so sánh chính xác giữa hai cột có kiểu dữ liệu khác nhau.
- **Trình bày báo cáo:** Định dạng ngày giờ hoặc số thực theo cấu trúc mong muốn hiển thị.
- **Giải quyết lỗi so sánh:** Tránh lỗi xung đột collation hoặc kiểu dữ liệu khi thực hiện phép nối (`JOIN`) hoặc so khớp.

---

## Bảng tham chiếu

### 1. Hàm chuyển đổi kiểu dữ liệu tường minh

| Hàm chuyển đổi | Cú pháp sử dụng | Các kiểu dữ liệu đích hỗ trợ (Target Types) |
| :--- | :--- | :--- |
| **`CAST()`** | `CAST(expression AS target_type)` | - `BINARY` (Chuỗi nhị phân)<br>- `CHAR` (Chuỗi ký tự)<br>- `DATE` (Ngày)<br>- `DATETIME` (Ngày giờ)<br>- `TIME` (Giờ)<br>- `DECIMAL` (Số thập phân)<br>- `SIGNED` (Số nguyên có dấu)<br>- `UNSIGNED` (Số nguyên không dấu)<br>- `JSON` (Dữ liệu JSON) |
| **`CONVERT()`** | `CONVERT(expression, target_type)` | Hỗ trợ các kiểu đích tương tự như `CAST()`. |
| **`CONVERT() WITH CHARSET`**| `CONVERT(expression USING charset_name)` | Dùng để chuyển đổi bảng mã ký tự (Character set) của chuỗi (ví dụ: chuyển sang `utf8mb4`). |

---

## Ví dụ

### 1. Sử dụng hàm `CAST()` để chuyển đổi kiểu dữ liệu
```sql
-- Chuyển chuỗi thành số nguyên không dấu để thực hiện phép toán
SELECT CAST('123' AS UNSIGNED) + 10 AS result_sum; -- Kết quả: 133

-- Chuyển chuỗi thành định dạng DATE
SELECT CAST('2026-08-19' AS DATE) AS formatted_date;

-- Chuyển số thực thành chuỗi ký tự
SELECT CAST(99.5 AS CHAR) AS string_score;
```

### 2. Sử dụng hàm `CONVERT()`
```sql
-- Chuyển đổi chuỗi sang định dạng DATETIME
SELECT CONVERT('2026-08-19 23:30:00', DATETIME) AS date_time_val;

-- Chuyển đổi mã hóa ký tự của chuỗi sang UTF-8
SELECT CONVERT('Xin chào' USING utf8mb4) AS utf_string;
```

### 3. Ép kiểu ngầm định (Implicit Conversion - do MySQL tự xử lý)
```sql
-- MySQL tự động ép chuỗi '10' thành số 10 để cộng
SELECT 50 + '10' AS auto_convert; -- Kết quả: 60

-- Cẩn thận: MySQL ép chuỗi không chứa số thành 0
SELECT 50 + 'abc' AS bad_convert; -- Kết quả: 50
```

---

## Lưu ý
> [!warning] Rủi ro ép kiểu ngầm định
> Không nên lạm dụng việc ép kiểu ngầm định của MySQL vì nó có thể dẫn đến kết quả sai lệch ngoài ý muốn (như việc `'abc'` bị ép thành `0` khi tính toán). Luôn sử dụng `CAST` hoặc `CONVERT` khi cần so sánh hay tính toán liên kiểu dữ liệu để đảm bảo tính nhất quán của code.
