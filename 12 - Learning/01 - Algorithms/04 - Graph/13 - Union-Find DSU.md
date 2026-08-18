# Union-Find / DSU (Cấu trúc dữ liệu các tập hợp rời nhau)

---

## Định nghĩa
Union-Find hay DSU (Disjoint Set Union) là một cấu trúc dữ liệu quản lý một tập hợp các phần tử được chia thành các tập con không giao nhau (rời nhau), hỗ trợ hai thao tác chính: Tìm kiếm đại diện tập hợp (`find`) và Hợp nhất hai tập hợp (`union`).

---

## Tác dụng
- **Kiểm tra liên thông đồ thị:** Kiểm tra xem hai đỉnh có thuộc cùng một thành phần liên thông hay không cực nhanh.
- **Phát hiện chu trình:** Dùng để phát hiện chu trình trong đồ thị vô hướng (là khối bổ trợ bắt buộc của thuật toán tìm cây khung nhỏ nhất Kruskal).

---

## FLOW
Ý tưởng tối ưu hóa (Nguyên lý 20/80):
Một DSU cơ bản có thể suy biến thành chuỗi dạng đường thẳng khiến độ phức tạp đạt $O(N)$. Để đạt độ phức tạp gần như hằng số ($O(\alpha(N))$ - hàm ngược Ackermann), ta áp dụng 2 kỹ thuật tối ưu:
1. **Nén đường đi (Path Compression):** Trong quá trình tìm gốc (`find`), cập nhật trực tiếp cha của tất cả các nút trên đường đi trỏ thẳng về nút gốc.
2. **Gộp theo hạng/kích thước (Union by Rank/Size):** Khi gộp hai tập hợp, luôn treo cây có chiều cao nhỏ hơn vào gốc của cây có chiều cao lớn hơn để giữ cho cây luôn cân bằng.

---

## Code triển khai (Java)
```java
public class DSU {
    private final int[] parent;
    private final int[] rank;

    public DSU(int size) {
        parent = new int[size];
        rank = new int[size];
        for (int i = 0; i < size; i++) {
            parent[i] = i; // Ban đầu, mỗi phần tử là cha của chính nó
            rank[i] = 0;
        }
    }

    // Thao tác Find có áp dụng Nén đường đi (Path Compression)
    public int find(int i) {
        if (parent[i] == i) {
            return i;
        }
        // Đệ quy gán trực tiếp cha của i bằng nút gốc tìm được
        return parent[i] = find(parent[i]); 
    }

    // Thao tác Union có áp dụng Gộp theo hạng (Union by Rank)
    public boolean union(int i, int j) {
        int rootI = find(i);
        int rootJ = find(j);

        // Nếu đã cùng thuộc một tập hợp
        if (rootI == rootJ) {
            return false; // Không cần gộp
        }

        // Gộp cây thấp hơn vào cây cao hơn
        if (rank[rootI] < rank[rootJ]) {
            parent[rootI] = rootJ;
        } else if (rank[rootI] > rank[rootJ]) {
            parent[rootJ] = rootI;
        } else {
            parent[rootI] = rootJ;
            rank[rootJ]++; // Tăng hạng nếu hai cây bằng chiều cao
        }
        return true;
    }
}
```

---

## Lưu ý
> [!important] Độ phức tạp thời gian cực nhỏ
> Nhờ áp dụng đồng thời cả hai kỹ thuật **Path Compression** và **Union by Rank**, độ phức tạp thời gian trung bình cho mỗi thao tác `find` hoặc `union` chỉ còn là $O(\alpha(N))$ (hầu như bằng $O(1)$ trong mọi giới hạn tính toán thực tế).
