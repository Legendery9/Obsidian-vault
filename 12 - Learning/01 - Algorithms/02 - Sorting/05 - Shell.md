# Shell Sort (Sắp xếp Shell)

---

## Định nghĩa
Shell Sort là một cải tiến của thuật toán Sắp xếp chèn (Insertion Sort). Nó phân chia mảng thành các mảng con bằng cách sử dụng một khoảng cách nhảy (gap), sắp xếp các mảng con đó bằng Insertion Sort, sau đó giảm dần khoảng cách nhảy cho đến khi gap bằng 1.

---

## Tác dụng
- **Tối ưu hóa phép di chuyển:** Insertion Sort di chuyển phần tử từng bước một ($O(1)$ khoảng cách). Shell Sort cho phép phần tử nhảy xa vượt bậc về phía vị trí đúng của nó, giúp giảm thiểu số lượng phép gán.

---

## FLOW
Ý tưởng chính:
1. Chọn khoảng cách nhảy ban đầu `gap` (thường là `n/2`).
2. Sắp xếp chèn các phần tử nằm cách nhau một khoảng là `gap`.
3. Giảm khoảng cách nhảy `gap = gap/2` và lặp lại bước 2.
4. Thuật toán kết thúc khi `gap = 0` (lúc này mảng đã được sắp xếp).

---

## Code triển khai (Java)
```java
public class ShellSort {
    public static void sort(int[] arr) {
        int n = arr.length;
        // Khởi tạo gap và giảm dần sau mỗi vòng
        for (int gap = n / 2; gap > 0; gap /= 2) {
            // Sắp xếp chèn cho các mảng con cách nhau một khoảng gap
            for (int i = gap; i < n; i++) {
                int temp = arr[i];
                int j;
                for (j = i; j >= gap && arr[j - gap] > temp; j -= gap) {
                    arr[j] = arr[j - gap];
                }
                arr[j] = temp;
            }
        }
    }
}
```

---

## Lưu ý
> [!important] Lựa chọn dãy Gap (Gap sequence)
> Hiệu năng của Shell Sort phụ thuộc rất lớn vào cách chọn dãy gap. Cách chọn mặc định `n/2, n/4...` có độ phức tạp tệ nhất là $O(N^2)$. Tuy nhiên, nếu sử dụng dãy gap khác như của Knuth (`(3^k - 1)/2`) hoặc Sedgewick, độ phức tạp trung bình có thể tối ưu hơn rất nhiều.
