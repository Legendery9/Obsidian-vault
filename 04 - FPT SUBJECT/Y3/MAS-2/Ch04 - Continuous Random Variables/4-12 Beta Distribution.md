---
tags:
  - MAS291
  - Chapter4
  - BetaDistribution
aliases:
  - Beta Distribution
  - Phân phối Beta
---

# 4.12 Phân Phối Beta (Beta Distribution)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> **Phân phối Beta** là phân phối liên tục trên khoảng $[0, 1]$, thường dùng để mô hình hóa **tỷ lệ, xác suất, và phần trăm**.

### Ứng dụng

- Mô hình hóa xác suất thành công của một quy trình.
- Phân phối tiên nghiệm (prior distribution) trong thống kê Bayes.
- Tỷ lệ lỗi, tỷ lệ bộ phận đạt chuẩn.

---

## 2. Ký hiệu và Công thức

| Ký hiệu | Ý nghĩa |
|:-------:|:--------|
| $\alpha > 0$ | Tham số hình dạng thứ nhất (Shape Parameter) |
| $\beta > 0$ | Tham số hình dạng thứ hai (Shape Parameter) |
| $B(\alpha, \beta)$ | Hàm Beta: $B(\alpha, \beta) = \dfrac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)}$ |

**PDF:**

$$f(x) = \frac{x^{\alpha-1}(1-x)^{\beta-1}}{B(\alpha,\beta)}, \quad 0 \le x \le 1$$

**Kỳ vọng và Phương sai:**

$$E(X) = \frac{\alpha}{\alpha+\beta} \qquad \text{Var}(X) = \frac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)}$$

### Hình dạng

| $\alpha, \beta$ | Hình dạng |
|:---------------|:---------|
| $\alpha = \beta = 1$ | Đều (Uniform[0,1]) |
| $\alpha < 1, \beta < 1$ | Hình chữ U |
| $\alpha > 1, \beta > 1$ | Hình chuông (có một đỉnh) |
| $\alpha > \beta$ | Lệch trái |
| $\alpha < \beta$ | Lệch phải |

---

## 3. Ví dụ minh họa

> **Exercise:** The proportion of time a machine is idle follows a Beta distribution with $\alpha = 2$ and $\beta = 5$. Find the mean proportion and variance.

**Giải:**

$$E(X) = \frac{2}{2+5} = \frac{2}{7} \approx 0.286$$

$$\text{Var}(X) = \frac{2 \times 5}{7^2 \times 8} = \frac{10}{392} \approx 0.0255$$

**Kết luận:** Máy nhàn rỗi trung bình $28.6\%$ thời gian với độ lệch chuẩn $\approx 15.97\%$.
