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

| Chiều chuyển đổi                               | Thuật toán sử dụng        | Công thức toán học / Cú pháp                                                                          |
| :--------------------------------------------- | :------------------------ | :---------------------------------------------------------------------------------------------------- |
| **Hệ bất kỳ (radix $R$) $\to$ Thập phân (10)** | **Sơ đồ Horner**          | $\text{result} = \text{result} \times R + d$<br>(Duyệt chữ số $d$ từ trái sang phải)                  |
| **Thập phân (10) $\to$ Hệ bất kỳ (radix $R$)** | **Chia lấy dư liên tiếp** | - Lấy phần dư $n \pmod R$ làm chữ số từ phải sang trái.<br>- Tiếp tục chia nguyên $n \mathbin{//} R$. |

---

## Chi tiết Công thức và Ký hiệu

### 1. Sơ đồ Horner ($\text{result} = \text{result} \times R + d$)
Dùng để chuyển một số từ cơ số $R$ bất kỳ sang hệ thập phân (cơ số 10) bằng cách duyệt chuỗi ký số từ trái qua phải.

- **$\text{result}$ (Giá trị tích lũy / Kết quả thập phân):**
  - *Ý nghĩa:* Lưu trữ giá trị thập phân tạm thời của chuỗi chữ số đã duyệt qua.
  - *Tác dụng:* Kết quả cuối cùng sau khi duyệt hết tất cả các chữ số của chuỗi nguồn sẽ là giá trị thập phân hoàn chỉnh.
  - *Khởi tạo & Cách tính:* Ban đầu được gán bằng $0$. Ở mỗi bước duyệt qua chữ số tiếp theo, $\text{result}$ mới được tính bằng công thức:
    $$\text{result}_{\text{mới}} = \text{result}_{\text{cũ}} \times R + d$$
  - *Lưu ý:* Phải kiểm tra để tránh tràn số (Overflow) nếu chuỗi chữ số nguồn quá lớn. Nếu vượt quá giới hạn của kiểu `int`, hãy dùng kiểu `long` hoặc `BigInteger`.

- **$R$ (Cơ số nguồn - Radix):**
  - *Ý nghĩa:* Cơ số ban đầu của số cần chuyển đổi (ví dụ: $R = 2$ cho Nhị phân, $R = 8$ cho Bát phân, $R = 16$ cho Thập lục phân).
  - *Tác dụng:* Đóng vai trò là hệ số nhân (trọng số dịch chuyển vị trí hàng) ở mỗi bước tích lũy.
  - *Giới hạn:* Trong Java, cơ số $R$ thường nằm trong phạm vi từ `Character.MIN_RADIX` ($2$) đến `Character.MAX_RADIX` ($36$).

- **$d$ (Giá trị của chữ số hiện tại):**
  - *Ý nghĩa:* Giá trị số tương ứng của ký tự đang duyệt qua.
  - *Tác dụng:* Được cộng vào kết quả tích lũy sau khi kết quả cũ đã được dịch chuyển bằng cách nhân với cơ số $R$.
  - *Cách tính riêng:* Với một ký tự `c` trong hệ cơ số $R$, ta cần ánh xạ ký tự đó sang giá trị số tương ứng. Trong Java, ta sử dụng:
    $$d = \text{Character.digit}(c, R)$$
    Hàm này tự động chuyển đổi `'0'` - `'9'` thành $0$ - $9$, và `'a'`/`'A'` - `'z'`/`'Z'` thành $10$ - $35$. Nếu ký tự `c` không hợp lệ trong cơ số $R$, hàm trả về $-1$.
  - *Lưu ý:* Luôn kiểm tra xem $d$ có bằng $-1$ hay không trước khi tính toán để phát hiện chuỗi đầu vào sai định dạng.

---

### 2. Phép chia lấy dư liên tiếp
Dùng để chuyển một số nguyên thập phân $n$ sang hệ cơ số $R$ bất kỳ.

- **$n$ (Số thập phân cần chuyển):**
  - *Ý nghĩa:* Giá trị số thập phân còn lại cần được phân tách thành các chữ số của cơ số mới.
  - *Tác dụng:* Được cập nhật giảm dần sau mỗi bước bằng phép chia nguyên cho cơ số $R$ ($n \leftarrow n \mathbin{//} R$). Quá trình dừng lại khi $n = 0$.
  - *Lưu ý:* Thuật toán chuẩn hoạt động với các số nguyên không âm. Đối với số âm, cần xử lý riêng phần dấu âm.

- **$R$ (Cơ số đích - Radix):**
  - *Ý nghĩa:* Cơ số của hệ thống số mới mà ta muốn chuyển đổi sang.
  - *Tác dụng:* Là số chia trong cả phép chia lấy dư và phép chia nguyên ở mỗi vòng lặp.

- **$n \pmod R$ (Phần dư):**
  - *Ý nghĩa:* Chữ số tương ứng trong hệ cơ số $R$.
  - *Tác dụng:* Đại diện cho chữ số ở vị trí hiện tại, bắt đầu từ hàng đơn vị (phải nhất) và dịch dần về bên trái. Trong Java, ta dùng toán tử `%` ($n \% R$).
  - *Ví dụ chuyển đổi ký số:* Nếu phần dư là một giá trị từ $0$ đến $9$, ta chuyển trực tiếp thành ký tự `'0'` - `'9'`. Nếu phần dư $\ge 10$, ta phải ánh xạ nó sang chữ cái tương ứng (ví dụ: $10 \to 'A'$, $15 \to 'F'$). Trong Java, ta có thể dùng mảng ký tự hoặc hàm `Character.forDigit(digit, R)`.

- **$n \mathbin{//} R$ (Thương nguyên):**
  - *Ý nghĩa:* Giá trị của số thập phân sau khi đã trích xuất chữ số cuối cùng ở hệ cơ số $R$. Trong Java, ta dùng toán tử `/` ($n / R$).
  - *Tác dụng:* Là giá trị đầu vào cho bước chia tiếp theo.

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

## Code triển khai (Java)

```java
public class BaseConversion {

    /**
     * Chuyển đổi từ hệ bất kỳ sang Thập phân (Sơ đồ Horner)
     * @param digitsStr Chuỗi ký số nguồn (ví dụ: "1011", "FF")
     * @param radix Cơ số nguồn R (2 <= R <= 36)
     * @return Giá trị thập phân kiểu long
     * @throws IllegalArgumentException nếu chuỗi đầu vào chứa ký tự không hợp lệ
     */
    public static long toDecimal(String digitsStr, int radix) {
        if (digitsStr == null || digitsStr.isEmpty()) {
            throw new IllegalArgumentException("Chuỗi đầu vào không được để trống!");
        }
        if (radix < Character.MIN_RADIX || radix > Character.MAX_RADIX) {
            throw new IllegalArgumentException("Cơ số không hỗ trợ! Yêu cầu từ " + Character.MIN_RADIX + " đến " + Character.MAX_RADIX);
        }

        long result = 0;
        for (int i = 0; i < digitsStr.length(); i++) {
            char c = digitsStr.charAt(i);
            int val = Character.digit(c, radix); // Lấy giá trị chữ số d
            
            if (val == -1) {
                throw new IllegalArgumentException("Ký tự '" + c + "' không hợp lệ trong hệ cơ số " + radix);
            }
            
            result = result * radix + val; // Công thức Horner
        }
        return result;
    }

    /**
     * Chuyển đổi từ Thập phân sang hệ bất kỳ
     * @param n Số thập phân cần chuyển đổi (n >= 0)
     * @param radix Cơ số đích R (2 <= R <= 36)
     * @return Chuỗi biểu diễn trong hệ cơ số mới
     */
    public static String fromDecimal(long n, int radix) {
        if (n < 0) {
            throw new IllegalArgumentException("Số cần chuyển đổi phải là số không âm!");
        }
        if (radix < Character.MIN_RADIX || radix > Character.MAX_RADIX) {
            throw new IllegalArgumentException("Cơ số không hỗ trợ!");
        }
        if (n == 0) {
            return "0";
        }

        StringBuilder sb = new StringBuilder();
        long temp = n;
        
        while (temp > 0) {
            int remainder = (int) (temp % radix); // Lấy phần dư n % R
            char digitChar = Character.forDigit(remainder, radix); // Chuyển phần dư thành ký tự
            sb.append(Character.toUpperCase(digitChar)); // Thống nhất chữ hoa cho hệ Hex
            temp = temp / radix; // Thương nguyên n // R
        }
        
        return sb.reverse().toString(); // Đảo ngược chuỗi để có kết quả chính xác
    }

    public static void main(String[] args) {
        // Test chuyển sang Thập phân
        System.out.println(toDecimal("1011", 2));  // Output: 11
        System.out.println(toDecimal("7B", 16));   // Output: 123
        
        // Test chuyển từ Thập phân sang hệ khác
        System.out.println(fromDecimal(11, 2));    // Output: 1011
        System.out.println(fromDecimal(123, 16));  // Output: 7B
    }
}
```

---

## Lưu ý
> [!tip] Đường tắt chuyển đổi nhanh Nhị phân (Cơ số 2) $\leftrightarrow$ Thập lục phân (Cơ số 16)
> Do $16 = 2^4$, ta có thể gom nhóm **4 chữ số nhị phân** thành **1 chữ số thập lục phân** trực tiếp mà không cần đi qua hệ thập phân trung gian.
> - Ví dụ: $1101\ 0011_2 = (1101_2)(0011_2) = D3_{16}$.