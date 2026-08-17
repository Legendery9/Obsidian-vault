---
tags:
  - MAS291
  - Chapter4
  - WeibullDistribution
aliases:
  - Weibull Distribution
  - Phân phối Weibull
---

# 4.10 Phân Phối Weibull (Weibull Distribution)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> **Phân phối Weibull** là phân phối liên tục linh hoạt dùng để mô hình hóa **thời gian sống (lifetime)** và **độ tin cậy (reliability)** của các hệ thống. Cho phép tốc độ hỏng hóc tăng, giảm, hoặc không đổi theo thời gian.

---

## 2. Ký hiệu và các tham số tham gia

| Ký hiệu | Tên tiếng Việt (English) |
|:-------:|:------------------------|
| $\beta > 0$ | Tham số hình dạng (Shape Parameter) |
| $\delta > 0$ | Tham số tỷ lệ (Scale Parameter) |
| $X \sim W(\beta, \delta)$ | $X$ tuân theo phân phối Weibull |

---

## 3. Công thức

**PDF:**

$$f(x) = \frac{\beta}{\delta}\left(\frac{x}{\delta}\right)^{\beta-1} e^{-(x/\delta)^\beta}, \quad x > 0$$

**CDF:**

$$F(x) = 1 - e^{-(x/\delta)^\beta}$$

**Kỳ vọng và Phương sai:**

$$E(X) = \delta\,\Gamma\!\left(1 + \frac{1}{\beta}\right) \qquad \text{Var}(X) = \delta^2\!\left[\Gamma\!\left(1+\frac{2}{\beta}\right) - \Gamma^2\!\left(1+\frac{1}{\beta}\right)\right]$$

### Quan hệ với phân phối khác

- $\beta = 1$: Weibull = Exponential($1/\delta$).
- $\beta = 2$: Weibull = Rayleigh distribution.

### Ý nghĩa của $\beta$

| $\beta$ | Tốc độ hỏng hóc (Hazard Rate) | Ứng dụng |
|:-------:|:------------------------------|:---------|
| $< 1$ | Giảm dần | Sản phẩm hỏng sớm (burn-in failures) |
| $= 1$ | Không đổi | Hỏng ngẫu nhiên (Exponential) |
| $> 1$ | Tăng dần | Hao mòn theo tuổi (wear-out) |

---

## 4. Ví dụ minh họa

> **Exercise:** The lifetime of a mechanical component follows a Weibull distribution with shape parameter $\beta = 2$ and scale parameter $\delta = 1000$ hours. Find $P(X > 1200)$.

**Giải:**

$$P(X > 1200) = 1 - F(1200) = e^{-(1200/1000)^2} = e^{-1.44} \approx 0.2369$$

**Kết luận:** Xác suất linh kiện sống sót quá $1200$ giờ là khoảng $23.7\%$.
