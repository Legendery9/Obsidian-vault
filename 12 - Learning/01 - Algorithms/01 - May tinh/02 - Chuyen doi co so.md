# Chuyển đổi Cơ số (Base Conversion)

---

## Định nghĩa
Chuyển đổi cơ số là quá trình thay đổi cách biểu diễn một số từ hệ cơ số này sang hệ cơ số khác (ví dụ: chuyển từ hệ Thập phân - Cơ số 10 sang hệ Nhị phân - Cơ số 2 hoặc hệ Thập lục phân - Cơ số 16).

---

## Tác dụng
- **Biểu diễn dữ liệu:** Giúp con người đọc hiểu các dữ liệu nhị phân thô của máy tính thông qua hệ Hex (Cơ số 16).
- **Lập trình hệ thống:** Cần thiết khi làm việc với thanh ghi, lập trình nhúng, hoặc tối ưu hóa thao tác bit (Bitwise).

---

## Bảng tham chiếu

### 2 Công thức cốt lõi (Nguyên lý 20/80)

| Chiều chuyển đổi | Thuật toán sử dụng | Công thức toán học / Cú pháp |
| :--- | :--- | :--- |
| **Hệ bất kỳ (radix $R$) $\to$ Thập phân (10)** | **Sơ đồ Horner** | $\text{result} = \text{result} \times R + d$<br>(Duyệt chữ số $d$ từ trái sang phải) |
| **Thập phân (10) $\to$ Hệ bất kỳ (radix $R$)** | **Chia lấy dư liên tiếp** | - Lấy phần dư $n \pmod R$ làm chữ số từ phải sang trái.<br>- Tiếp tục chia nguyên $n \mathbin{//} R$. |

---

## Ví dụ

### 1. Áp dụng Horner chuyển `1011` từ hệ 2 sang hệ 10 ($R = 2$)
- Khởi tạo: $\text{result} = 0$
- Bước 1: $\text{result} = 0 \times 2 + 1 = 1$
- Bước 2: $\text{result} = 1 \times 2 + 0 = 2$
- Bước 3: $\text{result} = 2 \times 2 + 1 = 5$
- Bước 4: $\text{result} = 5 \times 2 + 1 = \mathbf{11}$
$\Rightarrow 1011_2 = 11_{10}$ ✅

### 2. Áp dụng phép chia lấy dư chuyển `11` từ hệ 10 sang hệ 2 ($R = 2$)
- $11 \div 2 = 5$ dư $\mathbf{1}$ (chữ số cuối cùng)
- $5 \div 2 = 2$ dư $\mathbf{1}$
- $2 \div 2 = 1$ dư $\mathbf{0}$
- $1 \div 2 = 0$ dư $\mathbf{1}$ (chữ số đầu tiên)
$\Rightarrow 11_{10} = 1011_2$ ✅ (Ghép các số dư từ dưới lên)

---

## Code triển khai (Python)
```python
def to_decimal(digits_str, radix):
    """Chuyển đổi từ hệ bất kỳ sang Thập phân (Horner)"""
    result = 0
    for digit in digits_str:
        # Chuyển đổi ký tự thành giá trị số tương ứng (ví dụ 'F' -> 15)
        val = int(digit, radix)
        result = result * radix + val
    return result

def from_decimal(n, radix):
    """Chuyển đổi từ Thập phân sang hệ bất kỳ"""
    if n == 0: return "0"
    digits = []
    # Bản đồ ký tự cho hệ số lớn hơn 10
    chars = "0123456789ABCDEF"
    while n > 0:
        digits.append(chars[n % radix])
        n //= radix
    return "".join(reversed(digits))
```

---

## Lưu ý
> [!tip] Đường tắt chuyển đổi nhanh Nhị phân (Cơ số 2) $\leftrightarrow$ Thập lục phân (Cơ số 16)
> Do $16 = 2^4$, ta có thể gom nhóm **4 chữ số nhị phân** thành **1 chữ số thập lục phân** trực tiếp mà không cần đi qua hệ thập phân trung gian.
> - Ví dụ: $1101\ 0011_2 = (1101_2)(0011_2) = D3_{16}$.