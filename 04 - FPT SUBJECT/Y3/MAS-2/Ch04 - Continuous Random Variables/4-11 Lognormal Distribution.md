---
tags:
  - MAS291
  - Chapter4
  - LognormalDistribution
aliases:
  - Lognormal Distribution
  - Phân phối lognormal
---

# 4.11 Phân Phối Lognormal (Lognormal Distribution)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> $X$ có **phân phối lognormal** nếu $\ln X \sim N(\theta, \omega^2)$, tức là logarithm tự nhiên của $X$ có phân phối chuẩn.

### Ứng dụng

- Giá cổ phiếu, thu nhập, kích thước hạt phân tán, nồng độ chất ô nhiễm môi trường.

---

## 2. Ký hiệu và Công thức

| Ký hiệu | Ý nghĩa |
|:-------:|:--------|
| $\theta$ | Trung bình của $\ln X$ (Mean of Log) |
| $\omega^2$ | Phương sai của $\ln X$ (Variance of Log) |

**PDF:**

$$f(x) = \frac{1}{x\omega\sqrt{2\pi}} e^{-\frac{(\ln x - \theta)^2}{2\omega^2}}, \quad x > 0$$

**Kỳ vọng và Phương sai:**

$$E(X) = e^{\theta + \omega^2/2} \qquad \text{Var}(X) = e^{2\theta + \omega^2}(e^{\omega^2} - 1)$$

**Tính xác suất:** Chuẩn hóa bằng $Z = (\ln X - \theta)/\omega \sim N(0,1)$.

---

## 3. Ví dụ minh họa

> **Exercise:** The diameter of particles in a spray follows a lognormal distribution with $\theta = 2$ and $\omega = 0.5$. Find $P(X \le 10)$.

**Giải:**

$$P(X \le 10) = P\!\left(\frac{\ln 10 - 2}{0.5} \le Z\right) = P\!\left(\frac{2.303 - 2}{0.5} \le Z\right) = P(Z \le 0.606) \approx 0.7277$$

**Kết luận:** Khoảng $72.8\%$ hạt có đường kính $\le 10$ (đơn vị).
