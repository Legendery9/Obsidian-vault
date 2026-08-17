---
tags:
  - MAS291
  - Chapter10
  - TwoSamples
  - FTest
  - VarianceTest
aliases:
  - F-test for Variances
  - Kiểm định F cho phương sai hai mẫu
---

# 10.5 Suy Diễn về Phương Sai của Hai Phân Phối Chuẩn (Inference on Variances of Two Normal Distributions)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> Suy diễn về **tỷ lệ phương sai** $\sigma_1^2/\sigma_2^2$ của hai tổng thể chuẩn — dùng phân phối **$F$**.

### Ứng dụng

- Kiểm tra xem phương sai hai tổng thể có bằng nhau không (tiền đề cho kiểm định pooled t-test).
- So sánh độ biến động của hai quy trình sản xuất.

### Điều kiện áp dụng

- Hai mẫu **độc lập** ngẫu nhiên.
- Cả hai tổng thể có phân phối **chuẩn** (bắt buộc — F-test nhạy cảm với vi phạm chuẩn).

---

## 2. Ký hiệu và các tham số tham gia

> [!info] Ký hiệu

| Ký hiệu | Tên tiếng Việt (English) |
|:-------:|:------------------------|
| $\sigma_1^2, \sigma_2^2$ | Phương sai tổng thể (Population Variances) |
| $s_1^2, s_2^2$ | Phương sai mẫu (Sample Variances) |
| $n_1, n_2$ | Cỡ mẫu (Sample Sizes) |
| $F_0$ | Giá trị thống kê kiểm định F (F Test Statistic) |
| $f_{\alpha/2,\,\nu_1,\,\nu_2}$ | Giá trị tới hạn F (Critical Value from F-distribution) |
| $\nu_1 = n_1 - 1$ | Bậc tự do tử (Numerator Degrees of Freedom) |
| $\nu_2 = n_2 - 1$ | Bậc tự do mẫu (Denominator Degrees of Freedom) |

---

## 3. Phân loại và Công thức

### 3.1 Phân phối F

$$\frac{S_1^2/\sigma_1^2}{S_2^2/\sigma_2^2} \sim F_{n_1-1,\,n_2-1}$$

### 3.2 Thống kê kiểm định

$$F_0 = \frac{s_1^2}{s_2^2}$$

**(Giả sử $H_0: \sigma_1^2 = \sigma_2^2$)**

### 3.3 Miền bác bỏ

| Dạng $H_1$ | Miền bác bỏ |
|:----------:|:-----------:|
| $\sigma_1^2 \ne \sigma_2^2$ | $F_0 > f_{\alpha/2,\,n_1-1,\,n_2-1}$ hoặc $F_0 < f_{1-\alpha/2,\,n_1-1,\,n_2-1}$ |
| $\sigma_1^2 > \sigma_2^2$ | $F_0 > f_{\alpha,\,n_1-1,\,n_2-1}$ |
| $\sigma_1^2 < \sigma_2^2$ | $F_0 < f_{1-\alpha,\,n_1-1,\,n_2-1}$ |

> [!note] Tính giá trị tới hạn đuôi trái
> $$f_{1-\alpha/2,\,\nu_1,\,\nu_2} = \frac{1}{f_{\alpha/2,\,\nu_2,\,\nu_1}}$$
> (đổi ngược vị trí hai bậc tự do)

### 3.4 Khoảng tin cậy cho $\sigma_1^2/\sigma_2^2$

$$\left[\frac{s_1^2}{s_2^2} \cdot \frac{1}{f_{\alpha/2,\,n_1-1,\,n_2-1}},\; \frac{s_1^2}{s_2^2} \cdot f_{\alpha/2,\,n_2-1,\,n_1-1}\right]$$

---

## 4. Ví dụ minh họa

### Ví dụ 1 (Dễ)

> **Exercise:** Two production processes produce metal rods. Process 1 ($n_1 = 16$): $s_1 = 0.035$ mm. Process 2 ($n_2 = 21$): $s_2 = 0.062$ mm. At $\alpha = 0.05$, test whether $\sigma_1^2 \ne \sigma_2^2$.

**Giải:**

$$F_0 = \frac{s_1^2}{s_2^2} = \frac{(0.035)^2}{(0.062)^2} = \frac{0.001225}{0.003844} = 0.319$$

**Giá trị tới hạn:** $\nu_1 = 15$, $\nu_2 = 20$, kiểm định hai phía:

$$f_{0.025,\,15,\,20} \approx 2.57 \qquad f_{0.975,\,15,\,20} = \frac{1}{f_{0.025,\,20,\,15}} \approx \frac{1}{2.76} \approx 0.362$$

**Miền bác bỏ:** $F_0 > 2.57$ hoặc $F_0 < 0.362$.

Vì $F_0 = 0.319 < 0.362$ → **Bác bỏ $H_0$**.

**Kết luận:** Có đủ bằng chứng thống kê để kết luận phương sai hai quy trình **khác nhau**. Quy trình 1 có phương sai nhỏ hơn — ổn định hơn.

---

### Ví dụ 2 (Trung bình — CI)

> **Exercise:** Using data from Example 1, construct a 95% CI for $\sigma_1^2/\sigma_2^2$.

**Giải:**

$$\frac{s_1^2}{s_2^2} = 0.319$$

$$CI = \left[\frac{0.319}{f_{0.025,15,20}}, \frac{0.319}{f_{0.975,15,20}}\right] = \left[\frac{0.319}{2.57}, 0.319 \times 2.76\right] = [0.124, 0.880]$$

Khoảng tin cậy $95\%$ cho $\sigma_1^2/\sigma_2^2$ là $[0.124, 0.880]$.

**Kết luận:** Khoảng tin cậy không chứa $1$ → phương sai hai quy trình **khác nhau** ở mức $5\%$.

---

### Ví dụ 3 (Khó — Ứng dụng thực tế)

> **Exercise:** Before performing a two-sample t-test, an engineer checks whether variances are equal. Sample 1 ($n_1 = 12$): $s_1 = 1.8$. Sample 2 ($n_2 = 15$): $s_2 = 3.2$. At $\alpha = 0.10$, test $H_1: \sigma_1^2 \ne \sigma_2^2$.

**Giải:**

$$F_0 = \frac{1.8^2}{3.2^2} = \frac{3.24}{10.24} = 0.316$$

$\nu_1 = 11$, $\nu_2 = 14$: $f_{0.05,11,14} \approx 2.74$; $f_{0.95,11,14} = 1/f_{0.05,14,11} \approx 1/2.84 \approx 0.352$.

**Miền bác bỏ:** $F_0 < 0.352$ → $0.316 < 0.352$ → **Bác bỏ $H_0$** ở mức $\alpha = 0.10$.

**Kết luận:** Phương sai hai mẫu **khác nhau** ở mức ý nghĩa $10\%$ → **nên dùng Welch's t-test** (không phải pooled t-test) cho kiểm định tiếp theo.

**Bài học:** F-test cho phương sai thường được thực hiện như bước kiểm tra điều kiện trước khi chọn loại two-sample t-test phù hợp.

> [!warning] Sai lầm thường gặp
> - **Nhầm bậc tự do**: Khi tính $f_{1-\alpha/2,\nu_1,\nu_2}$, phải đổi vị trí: $1/f_{\alpha/2,\nu_2,\nu_1}$.
> - **Cho rằng $F_0 = s_1^2/s_2^2$ luôn $\ge 1$**: $F_0 < 1$ hoàn toàn có thể xảy ra và có ý nghĩa.
> - **F-test nhạy cảm với vi phạm chuẩn**: Nếu tổng thể không chuẩn, kết quả F-test không đáng tin cậy.
