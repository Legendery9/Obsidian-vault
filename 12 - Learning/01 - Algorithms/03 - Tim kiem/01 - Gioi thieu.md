# Giới thiệu nhóm Thuật toán Tìm kiếm (Searching)

---

## Định nghĩa
Nhóm thuật toán tìm kiếm bao gồm các phương pháp dùng để kiểm tra sự tồn tại hoặc xác định vị trí của một phần tử mục tiêu (target) trong một cấu trúc dữ liệu (mảng, danh sách, bảng băm).

---

## Tác dụng
- **Khai thác dữ liệu:** Là khối tính toán cốt lõi của mọi hệ thống thông tin khi truy vấn dữ liệu từ khóa.
- **Tối ưu hóa hiệu năng hệ thống:** Việc chuyển từ tìm kiếm tuần tự ($O(N)$) sang các thuật toán tối ưu hơn ($O(\log N)$ hoặc $O(1)$) giúp tăng tốc độ phản hồi của phần mềm lên hàng nghìn lần.

---

## Bảng tham chiếu

### Độ phức tạp và điều kiện áp dụng của các thuật toán tìm kiếm

| Thuật toán | Độ phức tạp thời gian (Worst) | Điều kiện áp dụng | Cơ chế hoạt động cốt lõi |
| :--- | :---: | :--- | :--- |
| **[[02 - Linear\|Linear Search]]** | $O(N)$ | Mọi kiểu mảng (không cần sắp xếp) | Duyệt tuần tự từ đầu đến cuối mảng |
| **[[03 - Binary\|Binary Search]]** | $O(\log N)$ | Mảng **bắt buộc** phải được sắp xếp | Chia đôi phạm vi tìm kiếm liên tiếp |
| **[[04 - Jump\|Jump Search]]** | $O(\sqrt{N})$ | Mảng **bắt buộc** phải được sắp xếp | Nhảy qua từng khối kích thước $\sqrt{N}$ |
| **[[05 - Interpolation\|Interpolation Search]]**| $O(N)$ (Trung bình $O(\log(\log N))$) | Mảng đã sắp xếp, **dữ liệu phân bố đều** | Ước lượng vị trí dựa trên giá trị tìm kiếm |
| **[[06 - Exponential\|Exponential Search]]**| $O(\log N)$ | Mảng **bắt buộc** phải được sắp xếp | Tìm khoảng chứa mục tiêu bằng lũy thừa của 2, sau đó Binary Search |
| **[[07 - Fibonacci\|Fibonacci Search]]**| $O(\log N)$ | Mảng **bắt buộc** phải được sắp xếp | Chia phạm vi tìm kiếm dựa trên dãy số Fibonacci |
| **[[08 - Ternary\|Ternary Search]]** | $O(\log N)$ | Mảng **bắt buộc** phải được sắp xếp | Chia phạm vi làm 3 phần bằng 2 điểm chốt |
| **[[09 - Hash\|Hash Search]]** | $O(1)$ (tệ nhất $O(N)$) | Cần cấu trúc bảng băm (Hash Table) | Truy xuất trực tiếp thông qua hàm băm (Hash function) |

---

## Lưu ý
> [!important] Quy tắc chọn thuật toán tối ưu
> - Nếu mảng **chưa được sắp xếp và nhỏ**: Hãy dùng **Linear Search** để tránh tốn chi phí sắp xếp.
> - Nếu dữ liệu **đã sắp xếp và phân bố đều** (như danh bạ điện thoại từ A-Z, dãy số liên tục): **Interpolation Search** là lựa chọn tối ưu nhất.
> - Nếu tìm kiếm trên **mảng có kích thước cực lớn hoặc vô hạn**: **Exponential Search** rất phù hợp vì nó nhanh chóng khoanh vùng được biên giới hạn trên của mảng.