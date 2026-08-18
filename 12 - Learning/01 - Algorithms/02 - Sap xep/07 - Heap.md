# Heap Sort (Sắp xếp vun đống)

---

## Định nghĩa
Heap Sort là một thuật toán sắp xếp dựa trên so sánh, sử dụng cấu trúc dữ liệu Nhị phân Heap (thường là Max-Heap) để liên tục chọn phần tử lớn nhất và hoán đổi nó về cuối mảng.

---

## Tác dụng
- **Tối ưu hóa không gian lưu trữ:** Đạt độ phức tạp $O(N \log N)$ giống Merge Sort nhưng thực hiện sắp xếp tại chỗ (in-place) với độ phức tạp không gian chỉ là $O(1)$.

---

## FLOW
Ý tưởng chính:
1. **Xây dựng Heap (Build Heap):** Chuyển đổi mảng dữ liệu đầu vào thành một Max-Heap (mỗi nút cha luôn lớn hơn hoặc bằng các nút con của nó).
2. **Sắp xếp:**
   - Hoán đổi phần tử gốc (phần tử lớn nhất tại chỉ số `0`) với phần tử cuối cùng của Heap.
   - Giảm kích thước của Heap đi 1.
   - Gọi hàm `heapify()` trên nút gốc mới để tái cấu trúc lại Max-Heap.
   - Lặp lại cho đến khi kích thước Heap bằng 1.

---

## Code triển khai (Java)
```java
public class HeapSort {
    public static void sort(int[] arr) {
        int n = arr.length;

        // 1. Xây dựng Max-Heap từ mảng gốc
        for (int i = n / 2 - 1; i >= 0; i--) {
            heapify(arr, n, i);
        }

        // 2. Trích xuất từng phần tử lớn nhất từ Heap đưa về cuối mảng
        for (int i = n - 1; i > 0; i--) {
            // Hoán đổi gốc (lớn nhất) với phần tử cuối
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;

            // Xây dựng lại Max-Heap trên phần chưa sắp xếp
            heapify(arr, i, 0);
        }
    }

    private static void heapify(int[] arr, int n, int i) {
        int largest = i; // Khởi tạo nút cha là lớn nhất
        int left = 2 * i + 1;
        int right = 2 * i + 2;

        // Nếu nút con bên trái lớn hơn nút cha
        if (left < n && arr[left] > arr[largest]) {
            largest = left;
        }

        // Nếu nút con bên phải lớn hơn nút cha hiện tại
        if (right < n && arr[right] > arr[largest]) {
            largest = right;
        }

        // Nếu nút lớn nhất không phải là nút cha
        if (largest != i) {
            int swap = arr[i];
            arr[i] = arr[largest];
            arr[largest] = swap;

            // Tiếp tục vun đống đệ quy cho cây con bị ảnh hưởng
            heapify(arr, n, largest);
        }
    }
}
```

---

## Lưu ý
> [!warning] Không ổn định (Unstable)
> Do việc hoán đổi các phần tử từ đầu đến cuối Heap và đệ quy vun đống diễn ra liên tục trên các nút cách xa nhau, Heap Sort là thuật toán sắp xếp **không ổn định (unstable)**.
