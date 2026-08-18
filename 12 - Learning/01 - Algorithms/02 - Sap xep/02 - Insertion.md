# Insertion Sort (Sắp xếp chèn)

---

## Định nghĩa
Sắp xếp chèn (Insertion Sort) là một thuật toán sắp xếp đơn giản, hoạt động bằng cách duyệt qua từng phần tử và chèn nó vào đúng vị trí của nó trong phần mảng đã được sắp xếp trước đó.

---

## Tác dụng
- **Tối ưu với mảng gần như đã sắp xếp:** Đạt độ phức tạp cực kỳ tối ưu ($O(N)$) khi mảng đầu vào chỉ có một vài phần tử bị sai vị trí.
- **Sắp xếp trực tuyến (Online sorting):** Có thể sắp xếp một danh sách ngay khi nhận thêm phần tử mới mà không cần nhận toàn bộ dữ liệu từ đầu.

---

## FLOW
Ý tưởng chính:
1. Coi phần tử đầu tiên là mảng đã sắp xếp.
2. Duyệt từ phần tử thứ 2 đến cuối mảng:
   - Lưu giá trị phần tử hiện tại vào biến `key`.
   - Di chuyển các phần tử lớn hơn `key` của mảng đã sắp xếp lên một vị trí để tạo khoảng trống.
   - Chèn `key` vào khoảng trống đó.

---

## Code triển khai (Java)
```java
public class InsertionSort {
    public static void sort(int[] arr) {
        int n = arr.length;
        for (int i = 1; i < n; ++i) {
            int key = arr[i];
            int j = i - 1;

            // Di chuyển các phần tử lớn hơn key về sau
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j = j - 1;
            }
            arr[j + 1] = key;
        }
    }
}
```

---

## Lưu ý
> [!tip] Mảng kích thước nhỏ
> Trong thực tế, mặc dù các thuật toán phân rã như Quick Sort hay Merge Sort có hiệu năng tốt ở quy mô lớn, nhưng với các mảng nhỏ (thường ít hơn 10 - 20 phần tử), Insertion Sort chạy nhanh hơn do tốn ít chi phí quản lý bộ nhớ hơn.
