---
tags:
  - MAS291
  - Chapter6
  - DescriptiveStatistics
  - StemLeaf
aliases:
  - Stem and Leaf Diagram
  - Biểu đồ thân lá
---

# 6.2 Biểu Đồ Thân-Lá (Stem-and-Leaf Diagrams)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> **Biểu đồ thân-lá (Stem-and-Leaf Diagram)** là phương pháp trình bày dữ liệu số bằng cách tách mỗi giá trị thành hai phần:
> - **Thân (Stem):** Các chữ số đầu (tens, hundreds, …)
> - **Lá (Leaf):** Chữ số cuối cùng (ones)

### Ý nghĩa thống kê

- Giữ nguyên **giá trị thực** của dữ liệu (khác histogram chỉ hiện tần số).
- Cho thấy **hình dạng phân phối** và **các giá trị cụ thể** cùng lúc.
- Phù hợp với dữ liệu cỡ nhỏ đến trung bình ($n \le 100$).

### Quy trình xây dựng

1. Xác định range dữ liệu.
2. Chọn **thân** (thường là chữ số hàng chục trở lên).
3. Liệt kê tất cả các thân theo thứ tự tăng dần.
4. Gắn **lá** tương ứng vào từng thân.
5. Sắp xếp lá trong mỗi hàng tăng dần.

---

## 2. Ký hiệu và các tham số tham gia

> [!info] Ký hiệu

| Thuật ngữ | Tên tiếng Việt (English) |
|:---------|:------------------------|
| Stem | Thân — các chữ số đứng trước (Leading Digits) |
| Leaf | Lá — chữ số cuối cùng (Trailing Digit) |
| Back-to-back | Biểu đồ thân-lá kép để so sánh hai tập dữ liệu |

---

## 3. Phân loại và Công thức

### 3.1 Biểu đồ thân-lá đơn (Single Stem-and-Leaf)

**Cách tách số:**
- $37$ → Stem: $3$, Leaf: $7$
- $127$ → Stem: $12$, Leaf: $7$
- $2.4$ → Stem: $2$, Leaf: $4$

### 3.2 Biểu đồ thân-lá kép (Back-to-Back / Two-sided)

Dùng để **so sánh hai nhóm** — lá của nhóm 1 bên trái, lá nhóm 2 bên phải, thân ở giữa.

### 3.3 Đọc thông tin từ biểu đồ

- Hàng có **lá dày nhất** → khoảng giá trị phổ biến nhất.
- Hình dạng tổng thể → phân phối lệch phải/trái/đối xứng.
- Các lá đơn độc ở đầu/cuối → có thể là ngoại lệ.

---

## 4. Ví dụ minh họa

### Ví dụ 1 (Dễ)

> **Exercise:** The following are the scores of 12 students on a quiz: 45, 52, 67, 71, 58, 63, 79, 84, 56, 72, 88, 61. Construct a stem-and-leaf diagram.

**Tóm tắt bài toán:** Dựng biểu đồ thân-lá cho $n = 12$ quan sát.

**Giải:**

**Bước 1:** Xác định range: Min = 45, Max = 88 → thân là hàng chục.

**Bước 2:** Dựng biểu đồ:

| Thân (Stem) | Lá (Leaf) | Giá trị |
|:-----------:|:---------:|:-------:|
| 4 | 5 | 45 |
| 5 | 2, 6, 8 | 52, 56, 58 |
| 6 | 1, 3, 7 | 61, 63, 67 |
| 7 | 1, 2, 9 | 71, 72, 79 |
| 8 | 4, 8 | 84, 88 |

```
4 | 5
5 | 2 6 8
6 | 1 3 7
7 | 1 2 9
8 | 4 8
```

**Đọc biểu đồ:**
- Phần lớn điểm số tập trung ở $50$-$79$.
- Phân phối tương đối đồng đều, hơi thưa ở đầu và cuối.

---

### Ví dụ 2 (Trung bình)

> **Exercise:** The compressive strength (MPa) of 20 concrete specimens is: 34, 41, 38, 29, 45, 52, 37, 43, 30, 48, 56, 39, 46, 33, 51, 42, 35, 49, 27, 44. Construct a stem-and-leaf diagram and find the median.

**Tóm tắt bài toán:** Biểu đồ thân-lá và tìm trung vị.

**Giải:**

```
Stem | Leaf (sorted)
2    | 7  9
3    | 0  3  4  5  7  8  9
4    | 1  2  3  4  5  6  8  9
5    | 1  2  6
```

$n = 20$ (chẵn): Median = trung bình của giá trị thứ 10 và thứ 11.

Đếm từ nhỏ đến lớn: ..., giá trị thứ 10 = 43, thứ 11 = 44.

$$\tilde{x} = \frac{43 + 44}{2} = 43.5 \text{ MPa}$$

**Đọc hình dạng:** Phân phối hơi lệch phải (đuôi phải dài hơn ở $50$-$56$, dữ liệu thưa ở $27$-$29$).

---

### Ví dụ 3 (Khó)

> **Exercise:** Compare the performance of two classes on a midterm exam using a back-to-back stem-and-leaf diagram. Class A ($n = 10$): 71, 65, 78, 82, 69, 74, 88, 76, 80, 73. Class B ($n = 10$): 58, 62, 70, 75, 68, 63, 81, 79, 66, 72.

**Tóm tắt bài toán:** Biểu đồ thân-lá kép để so sánh hai lớp.

**Giải:**

```
Class A (leaf) | Stem | Class B (leaf)
               |  5   | 8
               |  6   | 2  3  6  8
9  5           |  6   | (hàng 6 đã liệt kê)
8  6  4  3  1  |  7   | 0  2  5  9
8  2  0        |  8   | 1
```

Viết lại chuẩn (lá Class A đọc từ phải sang trái):

```
Class A       | Stem | Class B
              |  5   | 8
         9 5  |  6   | 2 3 6 8
  8 6 4 3 1   |  7   | 0 2 5 9
      8 2 0   |  8   | 1
```

**Tóm tắt so sánh:**

| Đo lường | Class A | Class B |
|:---------|:-------:|:-------:|
| Trung bình | $\bar{x}_A = 75.6$ | $\bar{x}_B = 69.4$ |
| Median | $76$ | $69$ |
| Min | $65$ | $58$ |
| Max | $88$ | $81$ |

**Kết luận:** Lớp A có kết quả **cao hơn** và tập trung ở vùng $70$-$88$; Lớp B thấp hơn và phân tán hơn ($58$-$81$).

> [!warning] Sai lầm thường gặp
> - **Không sắp xếp lá** tăng dần trong mỗi hàng → khó đọc và không tìm được median dễ dàng.
> - **Chọn thân không phù hợp**: Nếu thân quá thô (ít hàng), mất thông tin; quá mịn (quá nhiều hàng), biểu đồ trống.
> - **Biểu đồ thân-lá kép**: Lá Class A viết **từ thân ra ngoài về phía trái** — không cùng chiều với Class B.
