# Thuật toán Prim (Cây khung nhỏ nhất)

---

## Định nghĩa
Thuật toán Prim tìm cây khung nhỏ nhất (Minimum Spanning Tree - MST) của đồ thị vô hướng trọng số liên thông bằng cách bắt đầu từ một đỉnh bất kỳ và liên tục chọn cạnh có trọng số nhỏ nhất kết nối một đỉnh trong cây khung với một đỉnh ngoài cây khung.

---

## Tác dụng
- **Tối ưu hóa chi phí mạng lưới:** Giống như Kruskal, dùng để thiết lập sơ đồ liên kết hạ tầng với tổng chi phí nhỏ nhất.
- **Tối ưu cho đồ thị dày:** Prim chạy nhanh hơn Kruskal trên đồ thị có nhiều cạnh ($E \approx V^2$) nhờ cơ chế tìm kiếm lân cận thay vì sort toàn bộ danh sách cạnh.

---

## FLOW
Ý tưởng chính (Greedy phát triển cây khung):
Sử dụng **Priority Queue** và mảng đánh dấu `inMST`.
1. Chọn một đỉnh bắt đầu (ví dụ đỉnh $0$). Khởi tạo khoảng cách tạm thời tới các đỉnh khác là $\infty$, riêng `dist[start] = 0`.
2. Đưa cặp `(0, start)` vào Priority Queue.
3. Trong khi Priority Queue không rỗng:
   - Lấy đỉnh `u` có khoảng cách nhỏ nhất kết nối tới MST hiện tại.
   - Nếu `u` đã nằm trong MST (`inMST[u] = true`), bỏ qua.
   - Đánh dấu `inMST[u] = true`.
   - Duyệt các đỉnh kề `v` của `u` có trọng số cạnh `w`:
     - Nếu `v` chưa nằm trong MST và `w < dist[v]`: cập nhật `dist[v] = w` và đưa `(dist[v], v)` vào Priority Queue.

---

## Code triển khai (Java)
```java
import java.util.*;

public class Prim {
    static class Edge {
        int target, weight;
        Edge(int target, int weight) {
            this.target = target;
            this.weight = weight;
        }
    }

    static class Node implements Comparable<Node> {
        int id, key;
        Node(int id, int key) {
            this.id = id;
            this.key = key;
        }
        @Override
        public int compareTo(Node other) {
            return Integer.compare(this.key, other.key);
        }
    }

    public static int getMSTWeight(List<List<Edge>> adj) {
        int V = adj.size();
        int[] key = new int[V];
        boolean[] inMST = new boolean[V];
        Arrays.fill(key, Integer.MAX_VALUE);
        key[0] = 0;

        PriorityQueue<Node> pq = new PriorityQueue<>();
        pq.add(new Node(0, 0));

        int totalWeight = 0;

        while (!pq.isEmpty()) {
            Node curr = pq.poll();
            int u = curr.id;

            if (inMST[u]) continue;

            inMST[u] = true;
            totalWeight += curr.key;

            for (Edge edge : adj.get(u)) {
                int v = edge.target;
                int w = edge.weight;

                if (!inMST[v] && w < key[v]) {
                    key[v] = w;
                    pq.add(new Node(v, key[v]));
                }
            }
        }
        return totalWeight;
    }
}
```

---

## Lưu ý
> [!important] So sánh Prim vs Kruskal
> - **Kruskal:** Quản lý tập hợp cạnh rời rạc, phù hợp cho **đồ thị thưa** (Sparse Graph) nhờ độ phức tạp $O(E \log V)$.
> - **Prim:** Phát triển từ một đỉnh gốc duy nhất, phù hợp hơn cho **đồ thị dày** (Dense Graph) bằng cách dùng Priority Queue để đạt độ phức tạp $O(E \log V)$ hoặc Fibonacci Heap đạt $O(E + V \log V)$.
