# Giới thiệu nhóm Thuật toán Đồ thị (Graph)

---

## Định nghĩa
Đồ thị là một cấu trúc dữ liệu phi tuyến tính bao gồm một tập hợp các Đỉnh (Vertices/Nodes) kết nối với nhau bởi các Cạnh (Edges/Links). Nhóm thuật toán đồ thị tập hợp các phương pháp giải quyết các bài toán biểu diễn, tìm kiếm, tìm đường đi ngắn nhất, cây khung tối tiểu và liên thông trên đồ thị.

---

## Tác dụng
- **Mô hình hóa thế giới thực:** Biểu diễn mạng lưới giao thông, mạng xã hội, sơ đồ phân cấp tổ chức, hoặc sơ đồ phụ thuộc giữa các tác vụ.
- **Giải quyết các bài toán thực tế phức tạp:** Tìm đường đi ngắn nhất trên bản đồ (Google Maps), gợi ý kết bạn trên Facebook/LinkedIn, hoặc lập lịch dự án (PERT/CPM).

---

## Bảng tham chiếu

### Tóm tắt mục đích các thuật toán đồ thị cốt lõi

| Thuật toán | Mục đích giải quyết | Độ phức tạp thời gian | Phân nhóm |
| :--- | :--- | :---: | :--- |
| **[[02 - BFS\|BFS (Breadth-First Search)]]** | Duyệt đồ thị theo chiều rộng, tìm đường đi ngắn nhất trên đồ thị không trọng số | $O(V + E)$ | Duyệt đồ thị |
| **[[03 - DFS\|DFS (Depth-First Search)]]** | Duyệt đồ thị theo chiều sâu, tìm chu trình, liên thông | $O(V + E)$ | Duyệt đồ thị |
| **[[04 - Dijkstra\|Dijkstra]]** | Tìm đường đi ngắn nhất từ 1 đỉnh nguồn (không hỗ trợ cạnh âm) | $O((V + E) \log V)$ | Shortest Path |
| **[[05 - Bellman-Ford\|Bellman-Ford]]** | Tìm đường đi ngắn nhất hỗ trợ cạnh trọng số âm, phát hiện chu trình âm | $O(V \cdot E)$ | Shortest Path |
| **[[06 - Floyd-Warshall\|Floyd-Warshall]]** | Tìm đường đi ngắn nhất giữa **mọi cặp đỉnh** trên đồ thị | $O(V^3)$ | Shortest Path |
| **[[07 - A-Star\|A* (A-Star)]]** | Tìm đường đi ngắn nhất kết hợp Heuristic ước lượng khoảng cách | Phụ thuộc Heuristic | Shortest Path |
| **[[08 - Kruskal\|Kruskal]]** | Tìm cây khung nhỏ nhất (MST) bằng cách duyệt danh sách cạnh đã sort | $O(E \log E)$ | Minimum Spanning Tree |
| **[[09 - Prim\|Prim]]** | Tìm cây khung nhỏ nhất (MST) bằng cách phát triển đỉnh lân cận | $O((V + E) \log V)$ | Minimum Spanning Tree |
| **[[10 - Topological sort\|Topological Sort]]** | Sắp xếp topo thứ tự phụ thuộc của đồ thị có hướng không chu trình (DAG) | $O(V + E)$ | Lập lịch |
| **[[11 - Tarjan\|Tarjan]]** | Tìm các thành phần liên thông mạnh (SCC) bằng một lần duyệt DFS | $O(V + E)$ | Liên thông |
| **[[12 - Kosaraju\|Kosaraju]]** | Tìm các thành phần liên thông mạnh (SCC) bằng hai lần duyệt DFS | $O(V + E)$ | Liên thông |
| **[[13 - Union-Find DSU\|Union-Find DSU]]** | Quản lý các tập hợp rời nhau, kiểm tra chu trình đồ thị vô hướng | $O(E \cdot \alpha(V))$ | Cấu trúc bổ trợ |

---

## Lưu ý
> [!important] Biểu diễn đồ thị
> Đồ thị thường được biểu diễn bằng 2 cách chính trong bộ nhớ:
> 1. **Ma trận kề (Adjacency Matrix):** Mảng 2 chiều kích thước $V \times V$. Tốt cho đồ thị dày (nhiều cạnh), tra cứu cạnh cực nhanh ($O(1)$) nhưng tốn bộ nhớ ($O(V^2)$).
> 2. **Danh sách kề (Adjacency List):** Mảng gồm các danh sách liên kết. Tiết kiệm bộ nhớ ($O(V + E)$), phù hợp cho đồ thị thưa (ít cạnh) và là cách biểu diễn mặc định trong hầu hết các thuật toán.
