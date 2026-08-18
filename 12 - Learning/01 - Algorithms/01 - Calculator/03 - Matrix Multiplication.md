# Thuật toán Nhân Ma trận (Matrix Multiplication)

---

## Định nghĩa
Nhân ma trận là phép toán đại số tuyến tính kết hợp hai ma trận $A$ (kích thước $m \times n$) và $B$ (kích thước $n \times p$) để tạo ra ma trận kết quả $C$ (kích thước $m \times p$), trong đó mỗi phần tử $C_{ij}$ được tính bằng tích vô hướng của hàng $i$ của $A$ và cột $j$ của $B$.

---

## Tác dụng
- **Tính toán đồ họa:** Chuyển đổi tọa độ 2D/3D (xoay, co giãn hình ảnh).
- **Học máy & AI:** Là phép toán nền tảng của mạng nơ-ron nhân tạo (Neural Networks) khi tính toán lan truyền xuôi (Forward Propagation).

---

## Bảng tham chiếu

### So sánh các thuật toán nhân ma trận

| Phương pháp | Độ phức tạp thời gian (Big-O) | Mô tả thuật toán | Ưu điểm / Nhược điểm |
| :--- | :--- | :--- | :--- |
| **Naive Method (Ngây thơ)** | $O(N^3)$ | Sử dụng 3 vòng lặp `for` lồng nhau để tính toán từng phần tử. | **Ưu:** Dễ cài đặt, hiệu quả với ma trận nhỏ.<br>**Nhược:** Rất chậm khi kích thước ma trận lớn. |
| **Strassen Algorithm** | $O(N^{2.807})$ | Sử dụng kỹ thuật chia để trị (Divide and Conquer), chia nhỏ ma trận và giảm số phép nhân từ 8 xuống 7. | **Ưu:** Nhanh hơn trên lý thuyết với ma trận cực lớn.<br>**Nhược:** Phức tạp khi cài đặt, tốn bộ nhớ tạm. |

---

## Ví dụ

### Phép nhân ma trận $A \times B$ kích thước $2 \times 2$

Cho hai ma trận:
$$
A = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix},\quad B = \begin{bmatrix} 5 & 6 \\ 7 & 8 \end{bmatrix}
$$

Tính phần tử của ma trận kết quả $C = A \times B$:
- $C_{11} = 1 \times 5 + 2 \times 7 = 19$
- $C_{12} = 1 \times 6 + 2 \times 8 = 22$
- $C_{21} = 3 \times 5 + 4 \times 7 = 43$
- $C_{22} = 3 \times 6 + 4 \times 8 = 50$

Kết quả:
$$
C = \begin{bmatrix} 19 & 22 \\ 43 & 50 \end{bmatrix}
$$

---

## Code triển khai (Java - Naive Method)
```java
public class MatrixMultiplication {
    public static int[][] multiply(int[][] A, int[][] B) {
        int m = A.length;
        int n = A[0].length;
        int p = B[0].length;
        int[][] C = new int[m][p];

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < p; j++) {
                C[i][j] = 0;
                for (int k = 0; k < n; k++) {
                    C[i][j] += A[i][k] * B[k][j];
                }
            }
        }
        return C;
    }
}
```

---

## Lưu ý
> [!warning] Điều kiện nhân ma trận
> Phép nhân ma trận $A \times B$ **chỉ thực hiện được** khi và chỉ khi số cột của ma trận $A$ bằng số hàng của ma trận $B$. Phép nhân ma trận không có tính chất giao hoán ($A \times B \neq B \times A$).