# Sắp xếp Topo (Topological Sort)

---

## Định nghĩa
Sắp xếp Topo (Topological Sort) của một đồ thị có hướng không chu trình (DAG - Directed Acyclic Graph) là một sự sắp xếp tuyến tính thứ tự của các đỉnh sao cho với mọi cạnh có hướng đi từ đỉnh $u$ đến đỉnh $v$, $u$ luôn xuất hiện trước $v$ trong cách sắp xếp.

---

## Tác dụng
- **Lập lịch công việc:** Giải quyết các bài toán về trình tự công việc cần thực hiện trước/sau (ví dụ: đăng ký các môn học tiên quyết tại trường đại học, quy trình đóng gói phần mềm trong CI/CD).

---

## FLOW
Có hai thuật toán sắp xếp Topo phổ biến nhất:

### 1. Giải thuật Kahn (Dựa trên bán bậc vào - Indegree / BFS)
1. Tính bán bậc vào (số lượng cạnh đi vào) của tất cả các đỉnh.
2. Đưa các đỉnh có bán bậc vào bằng `0` vào Queue.
3. Trong khi Queue không rỗng:
   - Lấy đỉnh `u` ra khỏi Queue và lưu vào danh sách kết quả.
   - Với mỗi đỉnh kề `v` của `u`, giảm bán bậc vào của `v` đi 1.
   - Nếu bán bậc vào của `v` giảm về `0`, đưa `v` vào Queue.
4. Nếu danh sách kết quả không đủ $V$ đỉnh, đồ thị có chứa chu trình (không thể sắp xếp Topo).

### 2. Sử dụng DFS (Kèm Stack)
1. Thực hiện DFS trên các đỉnh chưa được duyệt.
2. Khi một đỉnh đã duyệt xong tất cả các đỉnh con của nó (hoàn thành xong nhánh đệ quy), đẩy đỉnh đó vào một **Stack**.
3. Kết quả sắp xếp Topo thu được bằng cách lấy lần lượt các phần tử ra khỏi Stack.

---

## Code triển khai (Java - Giải thuật Kahn)
```java
import java.util.*;

public class TopologicalSort {
    public static List<Integer> sort(List<List<Integer>> adj) {
        int V = adj.size();
        int[] inDegree = new int[V];

        // 1. Tính bán bậc vào của mỗi đỉnh
        for (int u = 0; u < V; u++) {
            for (int v : adj.get(u)) {
                inDegree[v]++;
            }
        }

        // 2. Đưa các đỉnh có bán bậc vào bằng 0 vào Queue
        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < V; i++) {
            if (inDegree[i] == 0) {
                queue.add(i);
            }
        }

        List<Integer> topoOrder = new ArrayList<>();

        // 3. Xử lý hàng đợi
        while (!queue.isEmpty()) {
            int u = queue.poll();
            topoOrder.add(u);

            for (int v : adj.get(u)) {
                inDegree[v]--;
                if (inDegree[v] == 0) {
                    queue.add(v);
                }
            }
        }

        // Kiểm tra xem có chu trình hay không
        if (topoOrder.size() != V) {
            System.out.println("Đồ thị chứa chu trình!");
            return Collections.emptyList();
        }

        return topoOrder;
    }
}
```

---

## Lưu ý
> [!warning] Yêu cầu bắt buộc là DAG
> Sắp xếp Topo **chỉ áp dụng được** trên đồ thị có hướng không có chu trình (DAG). Nếu đồ thị có chu trình, thứ tự phụ thuộc vòng tròn sẽ khiến không có đỉnh nào đạt bán bậc vào bằng 0 ở giữa quy trình, làm giải thuật bị ngắt quãng.
