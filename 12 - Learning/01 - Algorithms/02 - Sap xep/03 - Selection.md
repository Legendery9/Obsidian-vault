# Selection Sort (Sắp xếp chọn)

---

## Định nghĩa
Sắp xếp chọn (Selection Sort) là thuật toán sắp xếp hoạt động bằng cách liên tục tìm phần tử nhỏ nhất (hoặc lớn nhất) từ phần chưa sắp xếp của mảng và hoán đổi nó lên đầu phần chưa sắp xếp đó.

---

## Tác dụng
- **Giảm thiểu số phép hoán đổi (Swaps):** Trong trường hợp bộ nhớ flash hoặc ghi dữ liệu đắt đỏ, Selection Sort tối ưu vì số lần ghi (hoán đổi) chỉ là $O(N)$ trong mọi trường hợp.

---

## FLOW
Ý tưởng chính:
1. Duyệt mảng từ trái sang phải qua chỉ số $i$.
2. Với mỗi vị trí $i$, tìm phần tử nhỏ nhất trong đoạn còn lại của mảng từ $i+1$ đến cuối.
3. Hoán đổi phần tử nhỏ nhất đó với phần tử tại vị trí $i$.
4. Lặp lại cho đến hết mảng.

---

## Code triển khai (Java)
```java
public class SelectionSort {
    public static void sort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            // Tìm phần tử nhỏ nhất trong mảng chưa sắp xếp
            int minIdx = i;
            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[minIdx]) {
                    minIdx = j;
                }
            }
            // Hoán đổi phần tử nhỏ nhất với phần tử đầu tiên
            int temp = arr[minIdx];
            arr[minIdx] = arr[i];
            arr[i] = temp;
        }
    }
}
```

---

## Lưu ý
> [!warning] Hiệu năng không đổi
> Selection Sort luôn có độ phức tạp thời gian là $O(N^2)$ trong mọi trường hợp (tốt nhất, trung bình, tệ nhất) vì nó luôn phải quét toàn bộ phần chưa sắp xếp để tìm giá trị nhỏ nhất. Do đó, tránh dùng thuật toán này cho các mảng dữ liệu lớn.
