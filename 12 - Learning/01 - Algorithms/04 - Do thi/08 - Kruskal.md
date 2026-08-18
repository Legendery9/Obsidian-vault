# Thuật toán Kruskal (Cây khung nhỏ nhất)

---

## Định nghĩa
Thuật toán Kruskal tìm cây khung nhỏ nhất (Minimum Spanning Tree - MST) của đồ thị vô hướng có trọng số liên thông bằng cách duyệt qua danh sách các cạnh đã sắp xếp từ nhỏ đến lớn và thêm cạnh vào cây khung nếu nó không tạo thành chu trình.

---

## Tác dụng
- **Tối ưu hóa chi phí mạng lưới:** Thiết lập đường cáp quang kết nối các thành phố, đường ống dẫn nước giữa các khu vực sao cho tổng độ dài đường ống xây dựng là ngắn nhất và tất cả các điểm đều được liên thông.

---

## FLOW
Ý tưởng chính (Giải thuật tham lam kết hợp DSU):
Sử dụng cấu trúc dữ liệu **Union-Find (Disjoint Set Union - DSU)** để kiểm tra nhanh chu trình.
1. Khởi tạo cây khung rỗng và khởi tạo cấu trúc DSU cho $V$ đỉnh riêng biệt.
2. Sắp xếp tất cả các cạnh của đồ thị theo thứ tự trọng số tăng dần.
3. Duyệt qua từng cạnh $(u, v)$ có trọng số $w$ trong danh sách đã sort:
   - Tìm tập hợp cha của $u$ và $v$ thông qua DSU.
   - Nếu cha của $u$ khác cha của $v$ (tức là không tạo thành chu trình):
     - Thêm cạnh $(u, v)$ vào cây khung.
     - Hợp nhất (Union) hai tập hợp của $u$ và $v$ lại.
   - Nếu cây khung đã đủ $V-1$ cạnh, dừng thuật toán sớm.

---

## Code triển khai (Java)
```java
import java.util.*;

public class Kruskal {
    static class Edge implements Comparable<Edge> {
        int src, dest, weight;
        Edge(int src, int dest, int weight) {
            this.src = src;
            this.dest = dest;
            this.weight = weight;
        }
        @Override
        public int compareTo(Edge other) {
            return Integer.compare(this.weight, other.weight);
        }
    }

    // Cấu trúc DSU đơn giản hỗ trợ Kruskal
    static class DSU {
        int[] parent;
        DSU(int n) {
            parent = new int[n];
            for (int i = 0; i < n; i++) parent[i] = i;
        }
        int find(int i) {
            if (parent[i] == i) return i;
            return parent[i] = find(parent[i]); // Path compression
        }
        boolean union(int i, int j) {
            int rootI = find(i);
            int rootJ = find(j);
            if (rootI != rootJ) {
                parent[rootI] = rootJ;
                return true;
            }
            return false;
        }
    }

    public static List<Edge> getMST(List<Edge> edges, int V) {
        Collections.sort(edges); // Sắp xếp các cạnh tăng dần
        DSU dsu = new DSU(V);
        List<Edge> mst = new ArrayList<>();

        for (Edge edge : edges) {
            if (dsu.union(edge.src, edge.dest)) {
                mst.add(edge);
                if (mst.size() == V - 1) break;
            }
        }
        return mst;
    }
}
```

---

## Lưu ý
> [!important] Hiệu năng thuật toán
> Độ phức tạp thời gian của Kruskal phụ thuộc chính vào phép sắp xếp các cạnh: $O(E \log E)$ hoặc $O(E \log V)$. Do đó, Kruskal cực kỳ hiệu quả trên các đồ thị thưa (số cạnh $E$ nhỏ tương đương số đỉnh $V$). Đối với đồ thị dày (nhiều cạnh), thuật toán Prim sẽ cho hiệu năng tốt hơn.
