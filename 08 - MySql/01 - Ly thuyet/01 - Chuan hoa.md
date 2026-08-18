# Chuẩn hóa Cơ sở dữ liệu (Normalization)

---

## Định nghĩa
Chuẩn hóa cơ sở dữ liệu là quá trình tổ chức cấu trúc bảng dữ liệu nhằm giảm thiểu sự trùng lặp (redundancy) và loại bỏ các dị thường (anomalies) khi thực hiện thêm, sửa, xóa dữ liệu.

---

## Tác dụng
- **Tiết kiệm dung lượng lưu trữ:** Tránh lưu lặp đi lặp lại cùng một thông tin ở nhiều nơi.
- **Bảo toàn toàn vẹn dữ liệu:** Tránh hiện tượng bất nhất (ví dụ: cập nhật địa chỉ khách hàng ở bảng này nhưng quên cập nhật ở bảng khác).
- **Hợp lý hóa truy vấn:** Tạo cấu trúc bảng rõ ràng, tối ưu hóa các phép nối (JOIN).

---

## Bảng tham chiếu

### Các dạng chuẩn cơ bản (1NF, 2NF, 3NF, BCNF)

| Dạng chuẩn                        | Điều kiện bắt buộc                                                                                                                 | Cách khắc phục vi phạm                                                                                         |
| :-------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------- |
| **1NF** (First Normal Form)       | - Mỗi ô chỉ chứa duy nhất một giá trị nguyên tố (atomic value).<br>- Không chứa mảng, danh sách hoặc nhóm lặp.                     | Tách các giá trị phân tách bằng dấu phẩy thành nhiều hàng riêng biệt hoặc bảng riêng.                          |
| **2NF** (Second Normal Form)      | - Phải đạt chuẩn 1NF.<br>- Mọi cột không phải khóa phải phụ thuộc hoàn toàn vào khóa chính (nếu khóa chính là khóa kép).           | Tách các thuộc tính chỉ phụ thuộc vào một phần của khóa chính ra một bảng mới.                                 |
| **3NF** (Third Normal Form)       | - Phải đạt chuẩn 2NF.<br>- Không có phụ thuộc bắc cầu giữa các thuộc tính không phải khóa (ví dụ: A → B, B → C thì không được có). | Tách thuộc tính phụ thuộc bắc cầu ra bảng riêng (đưa B và C ra bảng mới, giữ lại B làm khóa ngoại ở bảng gốc). |
| **BCNF** (Boyce-Codd Normal Form) | - Phải đạt chuẩn 3NF.<br>- Mọi phụ thuộc hàm $X \to Y$ thì $X$ phải là siêu khóa (superkey).                                       | Phân rã bảng để tất cả các mối quan hệ phụ thuộc đều bắt nguồn từ khóa chính.                                  |

---

## Ví dụ

### 1. Vi phạm và sửa đổi 1NF
- **Vi phạm 1NF:**
  | Tên Học Sinh | Môn Học |
  | ---- | ---- |
  | An | Toán, Lý, Hóa |
- **Đạt chuẩn 1NF (Mỗi ô 1 giá trị):**
  | Tên Học Sinh | Môn Học |
  | :--- | :--- |
  | An | Toán |
  | An | Lý |
  | An | Hóa |

### 2. Vi phạm và sửa đổi 2NF
Giả sử có khóa chính kép là `(Mã SV, Mã Môn)`.
- **Vi phạm 2NF:**
  | Mã SV (PK) | Mã Môn (PK) | Tên SV | Điểm |
  | :--- | :--- | :--- | :--- |
  | SV01 | MM01 | An | 9.0 |
  > [!warning] Giải thích vi phạm
  > Cột `Tên SV` chỉ phụ thuộc vào `Mã SV`, chứ không phụ thuộc vào `Mã Môn`. Đây là phụ thuộc từng phần.
- **Đạt chuẩn 2NF (Tách thành 2 bảng):**
  - **Bảng Sinh_Vien:** `(Mã SV [PK], Tên SV)`
  - **Bảng Ket_Qua:** `(Mã SV [FK], Mã Môn, Điểm)`

---

## Lưu ý
> [!note] Đánh đổi hiệu năng (De-normalization)
> Mặc dù chuẩn hóa giúp dữ liệu nhất quán, nhưng việc phân rã quá nhiều bảng sẽ buộc hệ thống phải thực hiện nhiều phép `JOIN` phức tạp, làm chậm tốc độ truy vấn đọc. Trong thực tế, đôi khi người ta chấp nhận vi phạm chuẩn hóa (gọi là khử chuẩn - denormalization) ở một mức độ hợp lý để tăng tốc hiệu năng đọc.
