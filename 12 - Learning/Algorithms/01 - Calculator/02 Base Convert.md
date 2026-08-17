# Công thức tổng quát (nguyên lý 20% quan trọng nhất)

Chỉ cần nắm **2 công thức lõi** dưới đây, bạn suy ra được mọi phép chuyển đổi giữa bất kỳ hệ số nào (2, 8, 10, 16...).

---

## Công thức 1: "Bất kỳ hệ nào → Decimal" — dùng thuật toán Horner

```
result = 0
for mỗi chữ số (từ trái sang phải):
    result = result * radix + digitValue
```

**Đây là 20% quan trọng nhất — hiểu cái này là hiểu tất cả.**

### Tại sao công thức này đúng?

Cách "học thuộc" (nhân lũy thừa) và cách Horner thực chất là một, chỉ là Horner **rút gọn phép tính** bằng cách đặt thừa số chung ra ngoài (giống phân tích đa thức).

Ví dụ `1011₂` viết dưới dạng đa thức:

```
1×2³ + 0×2² + 1×2¹ + 1×2⁰
```

Horner "gói" nó lại bằng cách đặt 2 ra làm nhân tử chung liên tục:

```
1×2³ + 0×2² + 1×2¹ + 1×2⁰ = (1×2² + 0×2 + 1)×2 + 1 = ((1×2 + 0)×2 + 1)×2 + 1
```

→ Đây chính là lý do có công thức `result = result * radix + digit`: mỗi bước bạn **nhân kết quả cũ với radix rồi cộng chữ số mới vào**, thay vì tính lũy thừa riêng lẻ rồi cộng hết một lần.

### Áp dụng cho `1011₂` (radix = 2):

| Bước    | digit | result = result×2 + digit |
| ------- | ----- | ------------------------- |
| Bắt đầu | —     | result = 0                |
| 1       | 1     | 0×2+1 = *1*               |
| 2       | 0     | *1*×2+0 = 2               |
| 3       | 1     | 2×2+1 = 5                 |
| 4       | 1     | 5×2+1 = **11**            |

→ `1011₂ = 11₁₀` ✅ (khớp với cách tính lũy thừa ở câu trước)

### Áp dụng cho `2F₁₆` (radix = 16):

|Bước|digit|result = result×16 + digit|
|---|---|---|
|1|2|0×16+2 = 2|
|2|F(=15)|2×16+15 = **47**|

→ `2F₁₆ = 47₁₀` ✅

**Điểm mấu chốt:** công thức này **giống hệt nhau cho mọi hệ số**, chỉ cần đổi `radix` (2, 8, 16...) và cách đọc `digitValue` (ví dụ F → 15). Đây là lý do một hàm code duy nhất xử lý được mọi hệ:

```python
def to_decimal(digits, radix):
    result = 0
    for d in digits:
        result = result * radix + value_of(d)  # value_of('F') = 15
    return result
```

---

## Công thức 2: "Decimal → bất kỳ hệ nào" — chia lấy dư (ngược của Horner)

```
digits = []
while n > 0:
    digits.insert(0, n % radix)   # lấy dư, đây là chữ số (từ phải sang trái)
    n = n // radix                 # chia nguyên, tiếp tục
```

### Vì sao là phép ngược?

Ở công thức 1, mỗi bước bạn "gói" digit vào bằng `×radix + digit`. 
Ở công thức 2, bạn làm ngược lại: **"bóc" digit ra** bằng cách lấy phần dư khi chia cho radix, rồi bỏ nó đi (`// radix`) để lộ ra digit tiếp theo.

```python
def from_decimal(n, radix):
    digits = []
    while n > 0:
        digits.insert(0, n % radix)
        n //= radix
    return digits
```

Đây chính là thứ bạn đã làm bằng tay ở câu trả lời trước (`13 ÷ 2 dư 1`, `47 ÷ 16 dư 15`...) — chỉ là viết thành vòng lặp tổng quát.

---

## Tóm lại theo tinh thần 80/20

- **80% giá trị nằm ở 1 công thức duy nhất:** `result = result * radix + digit` (Horner) — dùng để đọc số ở bất kỳ hệ nào ra decimal.
- Phép ngược của nó (`% radix` rồi `// radix`) cho bạn chiều còn lại.
- **Binary ↔ Hex không cần công thức trên** vì có đường tắt riêng (nhóm 4-bit) do 16 = 2⁴ — đây là ngoại lệ đáng nhớ vì nó nhanh hơn hẳn việc đi vòng qua decimal.

Bạn có muốn mình viết code minh họa (Python/JS/C) áp dụng 2 công thức này để tự viết hàm chuyển đổi không?