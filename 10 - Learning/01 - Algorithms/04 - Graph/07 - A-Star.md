# Thuật toán A* (Tìm kiếm Heuristic)

---

## Định nghĩa
A* (A-Star) là một thuật toán tìm kiếm đường đi trên đồ thị, mở rộng từ Dijkstra bằng cách sử dụng các hàm đánh giá Heuristic để định hướng tìm kiếm thông minh về phía đỉnh đích, làm giảm thiểu số lượng đỉnh cần duyệt.

---

## Tác dụng
- **Tìm kiếm tối ưu trong game và robot:** Là tiêu chuẩn vàng để lập trình AI tìm đường đi (Pathfinding) trong các trò chơi chiến thuật hoặc di chuyển của robot tự hành trong bản đồ lưới 2D/3D.

---

## FLOW
Ý tưởng chính:
Tại mỗi bước duyệt, thuật toán chọn đỉnh $n$ tiếp theo có giá trị hàm chi phí $f(n)$ thấp nhất:
$$
f(n) = g(n) + h(n)
$$
Trong đó:
- $g(n)$: Chi phí thực tế từ đỉnh nguồn xuất phát tới đỉnh hiện tại $n$.
- $h(n)$: Chi phí ước lượng Heuristic từ đỉnh hiện tại $n$ tới đỉnh đích (ví dụ: khoảng cách đường chim bay Euclidean hoặc khoảng cách Manhattan trên bản đồ lưới).

---

## Code triển khai (Java - Minh họa thuật toán trên lưới 2D)
```java
import java.util.*;

public class AStar {
    static class Cell {
        int x, y;
        double g, h, f;
        Cell parent;
        Cell(int x, int y) {
            this.x = x;
            this.y = y;
            this.g = Double.MAX_VALUE;
            this.f = Double.MAX_VALUE;
        }
    }

    // Hàm Heuristic tính khoảng cách Manhattan (phù hợp di chuyển 4 hướng trên lưới)
    private static double calculateHeuristic(int x, int y, Cell target) {
        return Math.abs(x - target.x) + Math.abs(y - target.y);
    }

    public static List<Cell> findPath(int[][] grid, Cell start, Cell target) {
        int rows = grid.length;
        int cols = grid[0].length;
        
        PriorityQueue<Cell> openList = new PriorityQueue<>(Comparator.comparingDouble(c -> c.f));
        boolean[][] closedList = new boolean[rows][cols];

        start.g = 0;
        start.h = calculateHeuristic(start.x, start.y, target);
        start.f = start.g + start.h;
        openList.add(start);

        int[][] dirs = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}}; // 4 hướng di chuyển

        while (!openList.isEmpty()) {
            Cell curr = openList.poll();
            closedList[curr.x][curr.y] = true;

            if (curr.x == target.x && curr.y == target.y) {
                // Đã tìm thấy đích, tái tạo đường đi
                List<Cell> path = new ArrayList<>();
                Cell temp = curr;
                while (temp != null) {
                    path.add(temp);
                    temp = temp.parent;
                }
                Collections.reverse(path);
                return path;
            }

            for (int[] dir : dirs) {
                int nx = curr.x + dir[0];
                int ny = curr.y + dir[1];

                if (nx >= 0 && nx < rows && ny >= 0 && ny < cols && grid[nx][ny] == 0 && !closedList[nx][ny]) {
                    double gNew = curr.g + 1.0;
                    double hNew = calculateHeuristic(nx, ny, target);
                    double fNew = gNew + hNew;

                    Cell neighbor = new Cell(nx, ny);
                    neighbor.g = gNew;
                    neighbor.h = hNew;
                    neighbor.f = fNew;
                    neighbor.parent = curr;

                    openList.add(neighbor);
                }
            }
        }
        return Collections.emptyList(); // Không tìm thấy đường đi
    }
}
```

---

## Lưu ý
> [!important] Tính chấp nhận được của Heuristic (Admissibility)
> Để thuật toán A* đảm bảo tìm được đường đi ngắn nhất chính xác, hàm Heuristic $h(n)$ phải là một **hàm chấp nhận được** (admissible), nghĩa là nó không bao giờ được ước lượng chi phí lớn hơn chi phí thực tế tối thiểu từ đỉnh hiện tại tới đích (ví dụ: khoảng cách đường chim bay luôn ngắn hơn hoặc bằng đường đi thực tế).
