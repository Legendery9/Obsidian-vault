# Quick Sort (Sắp xếp nhanh)

---

## Định nghĩa
Sắp xếp nhanh (Quick Sort) là thuật toán sắp xếp dựa trên kỹ thuật Chia để trị (Divide and Conquer), hoạt động bằng cách chọn một phần tử làm điểm chốt (pivot), phân chia mảng thành hai phần: một phần chứa các phần tử nhỏ hơn pivot và phần còn lại lớn hơn pivot, sau đó lặp lại đệ quy trên hai phần đó.

---

## Tác dụng
- **Tốc độ thực tế nhanh nhất:** Đối với dữ liệu ngẫu nhiên phân bố trong RAM, Quick Sort thường có tốc độ thực tế nhanh nhất trong số các thuật toán sắp xếp dựa trên so sánh nhờ tận dụng tốt bộ nhớ đệm (Cache locality).

---

## FLOW
Ý tưởng chính:
1. **Chọn Pivot:** Có nhiều cách chọn (phần tử đầu, cuối, giữa, hoặc ngẫu nhiên).
2. **Phân hoạch (Partition):** Duyệt qua mảng và chuyển các phần tử nhỏ hơn pivot sang trái, các phần tử lớn hơn sang phải. Đặt pivot vào đúng vị trí của nó.
3. **Đệ quy:** Tiếp tục gọi đệ quy sắp xếp hai phân mảng con bên trái và bên phải của pivot.

---

## Code triển khai (Java - Phân hoạch Lomuto)
```java
public class QuickSort {
    public static void sort(int[] arr, int low, int high) {
        if (low < high) {
            // pi là chỉ số phân hoạch, arr[pi] đã ở đúng vị trí
            int pi = partition(arr, low, high);

            // Sắp xếp đệ quy hai phần
            sort(arr, low, pi - 1);
            sort(arr, pi + 1, high);
        }
    }

    private static int partition(int[] arr, int low, int high) {
        // Chọn phần tử cuối cùng làm pivot
        int pivot = arr[high];
        int i = (low - 1); // Chỉ số của phần tử nhỏ hơn

        for (int j = low; j < high; j++) {
            // Nếu phần tử hiện tại nhỏ hơn hoặc bằng pivot
            if (arr[j] <= pivot) {
                i++;
                // Hoán đổi arr[i] và arr[j]
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        // Hoán đổi pivot về đúng vị trí giữa hai phân mảng
        int temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;

        return i + 1;
    }
}
```

---

## Lưu ý
> [!caution] Trường hợp tệ nhất $O(N^2)$ và cách khắc phục
> Trường hợp tệ nhất của Quick Sort xảy ra khi pivot được chọn luôn là phần tử nhỏ nhất hoặc lớn nhất (Ví dụ: mảng đã được sắp xếp sẵn và luôn chọn phần tử cuối làm pivot). 
> - **Khắc phục:** Chọn pivot ngẫu nhiên (Randomized Quick Sort) hoặc chọn phần tử trung vị của ba phần tử (Median-of-three) đầu, giữa và cuối mảng.
