# Thuật toán Dijkstra (Đường đi ngắn nhất)

---

## Định nghĩa
Thuật toán Dijkstra tìm đường đi ngắn nhất từ một đỉnh nguồn đơn (single-source) tới tất cả các đỉnh khác trên đồ thị có hướng hoặc vô hướng với các cạnh có trọng số **không âm**.

---

## Tác dụng
- **Tìm đường đi tối ưu:** Là giải thuật cốt lõi trong các ứng dụng bản đồ dẫn đường (như tìm tuyến đường đi qua các ngã rẽ có độ dài/thời gian di chuyển ngắn nhất).

---

## FLOW
Ý tưởng chính (Giải thuật tham lam - Greedy):
Sử dụng một **Hàng đợi ưu tiên (Priority Queue)** để luôn chọn đỉnh có khoảng cách tạm thời nhỏ nhất để tối ưu hóa.
1. Khởi tạo mảng khoảng cách `dist` từ nguồn tới mọi đỉnh là vô cùng ($\infty$), riêng `dist[source] = 0`.
2. Đưa cặp `(0, source)` vào Priority Queue.
3. Trong khi Priority Queue không rỗng:
   - Lấy đỉnh `u` có khoảng cách nhỏ nhất ra ngoài.
   - Nếu khoảng cách này lớn hơn `dist[u]`, bỏ qua (đã được tối ưu bởi đường đi khác ngắn hơn).
   - Với mỗi đỉnh kề `v` của `u` có trọng số cạnh là `w`:
     - Nếu `dist[u] + w < dist[v]`: cập nhật `dist[v] = dist[u] + w` và đưa `(dist[v], v)` vào Priority Queue (Relaxation).

---

## Code triển khai (Java)
```java
import java.util.*;

public class Dijkstra {
    static class Edge {
        int target, weight;
        Edge(int target, int weight) {
            this.target = target;
            this.weight = weight;
        }
    }

    static class Node implements Comparable<Node> {
        int id, distance;
        Node(int id, int distance) {
            this.id = id;
            this.distance = distance;
        }
        @Override
        public int compareTo(Node other) {
            return Integer.compare(this.distance, other.distance);
        }
    }

    public static int[] shortestPath(List<List<Edge>> adj, int source) {
        int V = adj.size();
        int[] dist = new int[V];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[source] = 0;

        PriorityQueue<Node> pq = new PriorityQueue<>();
        pq.add(new Node(source, 0));

        while (!pq.isEmpty()) {
            Node curr = pq.poll();
            int u = curr.id;

            if (curr.distance > dist[u]) continue;

            for (Edge edge : adj.get(u)) {
                int v = edge.target;
                int w = edge.weight;

                if (dist[u] + w < dist[v]) {
                    dist[v] = dist[u] + w;
                    pq.add(new Node(v, dist[v]));
                }
            }
        }
        return dist;
    }
}
```

---

## Lưu ý
> [!caution] Giới hạn cạnh trọng số âm
> Thuật toán Dijkstra **không hoạt động chính xác** trên đồ thị có các cạnh mang trọng số âm. Nếu đồ thị có cạnh âm, bắt buộc phải sử dụng thuật toán Bellman-Ford để tìm đường đi ngắn nhất.
