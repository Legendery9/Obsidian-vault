# Hash Search (Tìm kiếm bằng bảng băm)

---

## Định nghĩa
Tìm kiếm bằng bảng băm (Hash Search) là thuật toán tìm kiếm phần tử thông qua việc ánh xạ trực tiếp khóa (key) của dữ liệu sang một vị trí chỉ số lưu trữ (index) trong bộ nhớ bằng cách sử dụng một Hàm băm (Hash function).

---

## Tác dụng
- **Tốc độ tối ưu nhất:** Đạt độ phức tạp thời gian trung bình lý tưởng là $O(1)$ (hằng số), tức là tìm kiếm ngay lập tức mà không phụ thuộc vào kích thước của tập dữ liệu.
- **Ứng dụng rộng rãi:** Là cơ chế lưu trữ và tra cứu của các cấu trúc dữ liệu cốt lõi như `HashMap`, `HashSet` trong Java, `Dict` trong Python, `Object`/`Map` trong JavaScript.

---

## FLOW
Ý tưởng chính:
1. **Ghi dữ liệu:**
   - Lấy khóa $K$.
   - Tính toán chỉ số $i$ bằng hàm băm: $i = \text{hash}(K) \pmod{\text{size}}$.
   - Lưu trữ dữ liệu tại vị trí $i$ trong bảng băm.
2. **Tìm kiếm dữ liệu:**
   - Lấy khóa cần tìm $K$.
   - Tính toán chỉ số $i = \text{hash}(K) \pmod{\text{size}}$.
   - Truy xuất trực tiếp phần tử tại vị trí $i$. Kiểm tra trùng khớp để xử lý va chạm nếu có.

---

## Bảng tham chiếu

### Các kỹ thuật giải quyết va chạm (Collision Resolution)
Va chạm (Collision) xảy ra khi hai khóa khác nhau cùng băm ra một chỉ số giống nhau.

| Phương pháp | Mô tả kỹ thuật | Ưu điểm / Nhược điểm |
| :--- | :--- | :--- |
| **Chaining (Liên kết chuỗi)** | Mỗi ô của bảng băm chứa một danh sách liên kết. Các phần tử va chạm sẽ được thêm vào cuối danh sách này. | **Ưu:** Dễ cài đặt, bảng băm không bao giờ bị đầy.<br>**Nhược:** Tốn bộ nhớ cấp phát động cho con trỏ danh sách. |
| **Open Addressing (Dò tìm mở)**| Tìm kiếm một ô trống khác trong bảng băm theo quy luật:<br>- Dò tuyến tính (Linear Probing)<br>- Dò bậc hai (Quadratic Probing)<br>- Băm kép (Double Hashing) | **Ưu:** Tiết kiệm bộ nhớ vì lưu trữ trực tiếp trên mảng phẳng.<br>**Nhược:** Có thể xảy ra hiện tượng gom cụm (clustering) làm giảm hiệu năng tìm kiếm. |

---

## Code triển khai (Java - Mô phỏng HashMap đơn giản dùng Chaining)
```java
import java.util.LinkedList;

public class SimpleHashMap {
    private static class Entry {
        String key;
        int value;
        Entry(String key, int value) {
            this.key = key;
            this.value = value;
        }
    }

    private final int SIZE = 16;
    private final LinkedList<Entry>[] table;

    @SuppressWarnings("unchecked")
    public SimpleHashMap() {
        table = new LinkedList[SIZE];
        for (int i = 0; i < SIZE; i++) {
            table[i] = new LinkedList<>();
        }
    }

    private int getIndex(String key) {
        return Math.abs(key.hashCode()) % SIZE;
    }

    public void put(String key, int value) {
        int idx = getIndex(key);
        for (Entry entry : table[idx]) {
            if (entry.key.equals(key)) {
                entry.value = value; // Cập nhật nếu trùng khóa
                return;
            }
        }
        table[idx].add(new Entry(key, value));
    }

    public int get(String key) {
        int idx = getIndex(key);
        for (Entry entry : table[idx]) {
            if (entry.key.equals(key)) {
                return entry.value; // Tìm thấy
            }
        }
        return -1; // Không tìm thấy
    }
}
```

---

## Lưu ý
> [!caution] Suy hao hiệu năng tệ nhất $O(N)$
> Nếu hàm băm được thiết kế kém khiến tất cả các phần tử băm ra cùng một chỉ số, bảng băm sẽ suy biến thành một danh sách liên kết tuần tự, khiến độ phức tạp tìm kiếm tăng lên thành $O(N)$. Hãy luôn chọn hoặc sử dụng các hàm băm chuẩn hóa và phân bố đều đã được chứng minh hiệu quả (như MurmurHash, FNV-1a).
