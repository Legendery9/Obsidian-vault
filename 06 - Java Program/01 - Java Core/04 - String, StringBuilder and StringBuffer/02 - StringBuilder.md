# Java StringBuilder and StringBuffer

> [!abstract] Định nghĩa
> **StringBuilder** và **StringBuffer** là các lớp đại diện cho chuỗi ký tự khả biến (mutable), cho phép thực hiện các thao tác thêm, sửa, xóa trực tiếp trên đối tượng ban đầu mà không sinh ra các đối tượng rác trên bộ nhớ Heap như [[01 - String]].

---

## 1. So sánh String vs StringBuilder vs StringBuffer

| Tiêu chí | String | StringBuilder | StringBuffer |
| --- | --- | --- | --- |
| **Tính khả biến** | Bất biến (Immutable) | Khả biến (Mutable) | Khả biến (Mutable) |
| **Đồng bộ (Thread-Safe)**| ✅ (Do bất biến) | ❌ (Không đồng bộ) | ✅ (Synchronized methods) |
| **Hiệu năng (Speed)** | Chậm khi sửa đổi | Cực nhanh | Chậm hơn StringBuilder |
| **Phạm vi khuyên dùng** | Hằng số, chuỗi ít đổi. | Đơn luồng cần xử lý chuỗi nhiều. | Đa luồng cần đồng bộ xử lý chuỗi. |

---

## 2. Các phương thức phổ biến của StringBuilder / StringBuffer

Các hàm này thực thi trực tiếp và thay đổi trạng thái đối tượng ban đầu:

- `append(String str)`: Nối thêm chuỗi vào cuối đối tượng hiện tại.
- `insert(int offset, String str)`: Chèn chuỗi tại vị trí index `offset` chỉ định.
- `delete(int start, int end)`: Xóa ký tự từ vị trí `start` đến trước `end`.
- `reverse()`: Đảo ngược thứ tự chuỗi ký tự.

---

## 3. Quy tắc tối ưu bộ nhớ khi nối chuỗi

> [!warning] Tránh nối chuỗi bằng toán tử + trong vòng lặp lớn
> Khi sử dụng toán tử `+` để nối chuỗi trong vòng lặp, Java sẽ âm thầm khởi tạo đối tượng `StringBuilder` mới ở mỗi vòng lặp để thực hiện phép cộng, gây lãng phí bộ nhớ nghiêm trọng.
> ```java
> // ❌ Không nên làm (Don't): Gây tràn bộ nhớ Heap
> String text = "";
> for (int i = 0; i < 1000; i++) {
>     text += i; // Tạo ra 1000 đối tượng rác trên Heap!
> }
> 
> // ✅ Nên làm (Do): Sử dụng duy nhất một StringBuilder
> StringBuilder sb = new StringBuilder();
> for (int i = 0; i < 1000; i++) {
>     sb.append(i);
> }
> String text = sb.toString(); // Chỉ tạo duy nhất một đối tượng String kết quả.
> ```
