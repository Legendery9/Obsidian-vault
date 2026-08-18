# Interpolation Search (Tìm kiếm nội suy)

---

## Định nghĩa
Tìm kiếm nội suy (Interpolation Search) là một cải tiến của Tìm kiếm nhị phân dành cho mảng đã được sắp xếp và có giá trị **phân bố tương đối đồng đều**, trong đó vị trí kiểm tra tiếp theo được nội suy dựa trên giá trị của phần tử cần tìm.

---

## Tác dụng
- **Tốc độ cực nhanh cho dữ liệu đồng đều:** Với dữ liệu phân bố đều, số lượng phép so sánh trung bình giảm xuống chỉ còn $O(\log(\log N))$, nhanh hơn nhiều so với $O(\log N)$ của Binary Search.

---

## FLOW
Ý tưởng chính:
Thay vì luôn chọn vị trí giữa $mid = (low + high)/2$, thuật toán ước lượng vị trí kiểm tra $pos$ theo công thức tương tự như cách con người tra từ điển (ví dụ: tìm từ bắt đầu bằng chữ "A" sẽ lật ở đầu sách, bắt đầu bằng "Y" lật ở cuối sách):
$$
pos = low + \left( \frac{x - arr[low]}{arr[high] - arr[low]} \right) \times (high - low)
$$

---

## Code triển khai (Java)
```java
public class InterpolationSearch {
    public static int search(int[] arr, int x) {
        int low = 0;
        int high = arr.length - 1;

        while (low <= high && x >= arr[low] && x <= arr[high]) {
            // Điều kiện dừng để tránh chia cho 0
            if (low == high) {
                if (arr[low] == x) return low;
                return -1;
            }

            // Công thức tính vị trí nội suy
            int pos = low + (int) (((double)(high - low) / (arr[high] - arr[low])) * (x - arr[low]));

            // Kiểm tra phần tử tại vị trí pos
            if (arr[pos] == x) {
                return pos;
            }

            // Nếu x lớn hơn, bỏ qua nửa trái
            if (arr[pos] < x) {
                low = pos + 1;
            } 
            // Nếu x nhỏ hơn, bỏ qua nửa phải
            else {
                high = pos - 1;
            }
        }
        return -1;
    }
}
```

---

## Lưu ý
> [!warning] Trường hợp tệ nhất đạt $O(N)$
> Nếu dữ liệu phân bố lệch không đều (ví dụ: cấp số nhân như `1, 2, 4, 8, 16, 1024, 1000000...`), công thức nội suy ước lượng vị trí sai lệch lớn, khiến thuật toán suy thoái thành tìm kiếm tuần tự với độ phức tạp tệ nhất đạt $O(N)$.
