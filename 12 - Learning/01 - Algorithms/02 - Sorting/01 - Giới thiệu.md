# Giới thiệu nhóm Thuật toán Sắp xếp (Sorting)

---

## Định nghĩa
Nhóm thuật toán sắp xếp tập hợp các phương pháp sắp đặt các phần tử trong một danh sách (mảng) theo một thứ tự nhất định (tăng dần hoặc giảm dần).

---

## Tác dụng
- **Tăng tốc độ tìm kiếm:** Dữ liệu đã sắp xếp là điều kiện bắt buộc để chạy các thuật toán tìm kiếm tối ưu như Binary Search.
- **Tiền xử lý dữ liệu:** Giúp gom nhóm các phần tử trùng lặp, xác định phần tử lớn nhất/nhỏ nhất một cách nhanh chóng.

---

## Bảng tham chiếu

### Độ phức tạp của các thuật toán sắp xếp (Sorting Complexity)

| Thuật toán | Độ phức tạp tốt nhất (Best) | Độ phức tạp trung bình (Average) | Độ phức tạp tệ nhất (Worst) | Bộ nhớ phụ (Space) | Tính ổn định (Stable) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **[[02 - Insertion\|Insertion Sort]]** | $O(N)$ | $O(N^2)$ | $O(N^2)$ | $O(1)$ | **Yes** |
| **[[03 - Selection\|Selection Sort]]** | $O(N^2)$ | $O(N^2)$ | $O(N^2)$ | $O(1)$ | No |
| **[[04 - Bubble\|Bubble Sort]]** | $O(N)$ | $O(N^2)$ | $O(N^2)$ | $O(1)$ | **Yes** |
| **[[05 - Shell\|Shell Sort]]** | $O(N \log N)$ | $O(N^{1.5})$ | $O(N^2)$ | $O(1)$ | No |
| **[[06 - Merge\|Merge Sort]]** | $O(N \log N)$ | $O(N \log N)$ | $O(N \log N)$ | $O(N)$ | **Yes** |
| **[[07 - Heap\|Heap Sort]]** | $O(N \log N)$ | $O(N \log N)$ | $O(N \log N)$ | $O(1)$ | No |
| **[[08 - Quick\|Quick Sort]]** | $O(N \log N)$ | $O(N \log N)$ | $O(N^2)$ | $O(\log N)$ | No |
| **[[09 - Quick 3-way\|Quick Sort 3-way]]** | $O(N)$ | $O(N \log N)$ | $O(N^2)$ | $O(\log N)$ | No |

---

## Lưu ý
> [!info] Khái niệm Stable (Tính ổn định)
> Một thuật toán sắp xếp được gọi là **stable** nếu nó bảo toàn thứ tự ban đầu của các phần tử có giá trị bằng nhau. Điều này rất quan trọng khi sắp xếp các đối tượng phức tạp có nhiều thuộc tính (ví dụ: sắp xếp danh sách sinh viên theo tên, sau đó sắp xếp theo lớp).