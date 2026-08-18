# LIKE và Regular Expression (Tìm kiếm mẫu)

---

## Định nghĩa
LIKE và Regular Expression (REGEXP) là các toán tử so khớp mẫu trong SQL dùng để tìm kiếm các chuỗi ký tự thỏa mãn một khuôn mẫu định sẵn trong cơ sở dữ liệu.

---

## Tác dụng
- **Tìm kiếm tương đối (Fuzzy Search):** Hỗ trợ tìm kiếm dữ liệu khi người dùng chỉ nhớ một phần của từ khóa (ví dụ: tìm tên học sinh bắt đầu bằng chữ "A").
- **So khớp phức tạp (Regex):** Hỗ trợ các biểu thức chính quy để tìm kiếm dữ liệu có định dạng đặc thù như số điện thoại, email, định dạng mã số.

---

## Bảng tham chiếu

### 1. Toán tử LIKE và các ký tự đại diện (Wildcards)

| Ký tự đại diện | Ý nghĩa so khớp | Ví dụ mẫu |
| :---: | :--- | :--- |
| `%` | Đại diện cho **không, một hoặc nhiều** ký tự bất kỳ | `LIKE 'A%'` (Bắt đầu bằng chữ A)<br>`LIKE '%son'` (Kết thúc bằng "son") |
| `_` | Đại diện cho **đúng một** ký tự bất kỳ | `LIKE 'A_'` (Chuỗi gồm đúng 2 ký tự bắt đầu bằng A)<br>`LIKE '_b%'` (Ký tự thứ hai là b) |

### 2. Toán tử REGEXP (Biểu thức chính quy) trong MySQL

| Ký hiệu Regex | Ý nghĩa so khớp | Ví dụ |
| :---: | :--- | :--- |
| `^` | Bắt đầu chuỗi | `REGEXP '^Data'` (Bắt đầu bằng từ "Data") |
| `$` | Kết thúc chuỗi | `REGEXP 'db$'` (Kết thúc bằng từ "db") |
| `.` | Một ký tự bất kỳ (giống `_` của LIKE) | `REGEXP 'd.t'` (Khớp với "dat", "dot", "dit") |
| `*` | Lặp lại ký tự trước đó **0 hoặc nhiều lần** | `REGEXP 'ab*'` (Khớp với "a", "ab", "abbb"...) |
| `+` | Lặp lại ký tự trước đó **1 hoặc nhiều lần** | `REGEXP 'ab+'` (Khớp với "ab", "abbb", không khớp "a") |
| `[a-z]` | Khớp bất kỳ ký tự nào nằm trong khoảng từ a đến z | `REGEXP '^[a-m]'` (Bắt đầu bằng chữ cái từ a đến m) |
| `[A\|B]` | Khớp với ký tự A **hoặc** B (Hoạt động OR) | `REGEXP 'Toan|Ly'` (Chứa từ "Toan" hoặc "Ly") |

---

## Ví dụ

### 1. Ví dụ dùng toán tử LIKE
```sql
-- Tìm kiếm các học sinh có email sử dụng tên miền gmail.com
SELECT * FROM students 
WHERE email LIKE '%@gmail.com';

-- Tìm kiếm các mã lớp học gồm 5 ký tự và bắt đầu bằng 'LH'
SELECT * FROM classes 
WHERE class_name LIKE 'LH___';
```

### 2. Ví dụ dùng toán tử REGEXP
```sql
-- Tìm kiếm học sinh có họ tên bắt đầu bằng "Nguyen" hoặc "Tran"
SELECT * FROM students 
WHERE full_name REGEXP '^(Nguyen|Tran)';

-- Tìm kiếm học sinh có tên kết thúc bằng một chữ số từ 0 đến 9
SELECT * FROM students 
WHERE full_name REGEXP '[0-9]$';
```

---

## Lưu ý
> [!tip] Hiệu năng so khớp
> Sử dụng `REGEXP` và `LIKE` với ký tự đại diện ở đầu chuỗi (ví dụ: `%keyword`) sẽ **không tận dụng được Index** của cột đó, dẫn đến việc quét toàn bộ bảng (Table Scan) và làm giảm tốc độ truy vấn đối với các bảng lớn.
