---
tags:
  - MAS291
  - Chapter7
  - SamplingDistribution
  - CentralLimitTheorem
aliases:
  - CLT
  - Sampling Distribution
  - Phân phối mẫu
  - Định lý giới hạn trung tâm
---

# 7.2 Phân Phối Mẫu và Định Lý Giới Hạn Trung Tâm (Sampling Distributions and CLT)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> **Phân phối mẫu (Sampling Distribution)** của một thống kê là phân phối xác suất của thống kê đó khi được tính từ **tất cả các mẫu kích thước $n$ có thể lấy từ tổng thể**.

### Ý nghĩa thống kê

- Mỗi mẫu ngẫu nhiên cho một giá trị $\bar{x}$ khác nhau — $\bar{X}$ là **biến ngẫu nhiên**.
- Phân phối mẫu mô tả hành vi của $\bar{X}$ qua **rất nhiều mẫu** lấy từ cùng tổng thể.
- Hiểu phân phối mẫu là nền tảng để xây dựng **khoảng tin cậy** và **kiểm định giả thuyết**.

### Diễn giải trực quan

Hãy tưởng tượng lấy $1000$ mẫu mỗi mẫu $n = 25$ từ một tổng thể. Vẽ histogram của $1000$ giá trị $\bar{x}$ → histogram đó xấp xỉ **phân phối mẫu** của $\bar{X}$.

---

## 2. Ký hiệu và các tham số tham gia

> [!info] Ký hiệu

| Ký hiệu | Tên tiếng Việt (English) |
|:-------:|:------------------------|
| $\mu$ | Trung bình tổng thể (Population Mean) |
| $\sigma^2$ | Phương sai tổng thể (Population Variance) |
| $\sigma$ | Độ lệch chuẩn tổng thể (Population Standard Deviation) |
| $n$ | Cỡ mẫu (Sample Size) |
| $\bar{X}$ | Trung bình mẫu (Sample Mean — biến ngẫu nhiên) |
| $E(\bar{X})$ | Kỳ vọng của $\bar{X}$ (Expected Value of Sample Mean) |
| $\text{Var}(\bar{X})$ | Phương sai của $\bar{X}$ (Variance of Sample Mean) |
| $SE(\bar{X})$ | Sai số chuẩn (Standard Error): $SE(\bar{X}) = \sigma/\sqrt{n}$ |
| $Z$ | Biến ngẫu nhiên chuẩn hóa (Standardized Normal Variable) |

---

## 3. Phân loại và Công thức

### 3.1 Phân phối mẫu của $\bar{X}$ khi tổng thể chuẩn

**Định lý:** Nếu $X_1, X_2, \ldots, X_n$ là mẫu ngẫu nhiên từ $N(\mu, \sigma^2)$, thì:

$$\bar{X} = \frac{1}{n}\sum_{i=1}^n X_i \sim N\!\left(\mu, \frac{\sigma^2}{n}\right)$$

Tức là:

$$E(\bar{X}) = \mu \qquad \text{Var}(\bar{X}) = \frac{\sigma^2}{n} \qquad SE(\bar{X}) = \frac{\sigma}{\sqrt{n}}$$

**Chuẩn hóa:**

$$Z = \frac{\bar{X} - \mu}{\sigma/\sqrt{n}} \sim N(0, 1)$$

---

### 3.2 Định lý Giới Hạn Trung Tâm (Central Limit Theorem — CLT)

> [!abstract] Định lý Giới Hạn Trung Tâm
> Cho $X_1, X_2, \ldots, X_n$ là mẫu ngẫu nhiên từ **bất kỳ phân phối nào** (không cần chuẩn) với $E(X_i) = \mu$ và $\text{Var}(X_i) = \sigma^2 < \infty$. Khi $n \to \infty$:
>
> $$\frac{\bar{X} - \mu}{\sigma/\sqrt{n}} \xrightarrow{d} N(0, 1)$$
>
> Hay tương đương: $\bar{X} \approx N\!\left(\mu, \sigma^2/n\right)$ khi $n$ đủ lớn.

#### Quy tắc thực hành

- Với **hầu hết phân phối không chuẩn**: $n \ge 30$ thường đủ để CLT có hiệu lực.
- Với **phân phối rất lệch hoặc đuôi nặng**: Cần $n$ lớn hơn (có thể $n \ge 50$ hoặc hơn).
- Với **tổng thể chuẩn**: CLT có hiệu lực với **mọi** $n$ (kể cả $n = 1$).

> [!note] Tại sao CLT quan trọng?
> CLT cho phép ta dùng phân phối chuẩn để tính xác suất và xây dựng khoảng tin cậy **ngay cả khi tổng thể không chuẩn**, miễn là $n$ đủ lớn. Đây là lý do phân phối chuẩn xuất hiện khắp nơi trong thống kê ứng dụng.

---

### 3.3 Phân phối mẫu của $S^2$

Khi tổng thể $\sim N(\mu, \sigma^2)$:

$$\frac{(n-1)S^2}{\sigma^2} \sim \chi^2_{n-1}$$

Do đó:

$$E(S^2) = \sigma^2 \qquad \text{Var}(S^2) = \frac{2\sigma^4}{n-1}$$

---

### 3.4 Phân phối mẫu của $\hat{p}$

Với mẫu lớn, theo CLT:

$$\hat{p} = \frac{X}{n} \approx N\!\left(p, \frac{p(1-p)}{n}\right)$$

Sai số chuẩn:

$$SE(\hat{p}) = \sqrt{\frac{p(1-p)}{n}}$$

---

### 3.5 Tóm tắt phân phối mẫu

| Thống kê | Điều kiện | Phân phối mẫu |
|:--------:|:---------:|:------------:|
| $\bar{X}$ | Tổng thể chuẩn | $N(\mu, \sigma^2/n)$ — **chính xác** |
| $\bar{X}$ | Bất kỳ, $n$ lớn | $\approx N(\mu, \sigma^2/n)$ — CLT |
| $(n-1)S^2/\sigma^2$ | Tổng thể chuẩn | $\chi^2_{n-1}$ — chính xác |
| $(\bar{X}-\mu)/(S/\sqrt{n})$ | Tổng thể chuẩn, $\sigma$ chưa biết | $t_{n-1}$ — chính xác |
| $\hat{p}$ | $np \ge 5$, $n(1-p) \ge 5$ | $\approx N(p, p(1-p)/n)$ — CLT |

---

## 4. Ví dụ minh họa

### Ví dụ 1 (Dễ)

> **Exercise:** The time (in minutes) customers wait at a bank is exponentially distributed with $\mu = 5$ minutes and $\sigma = 5$ minutes. A random sample of **$n = 100$ customers** is taken. What is the probability that the sample mean wait time is **between 4.5 and 5.5 minutes**?

**Tóm tắt bài toán:** Tổng thể không chuẩn (mũ), $n = 100$ đủ lớn → dùng CLT.

$$\mu = 5,\quad \sigma = 5,\quad n = 100$$

**Giải:**

Theo CLT:

$$\bar{X} \approx N\!\left(5, \frac{25}{100}\right) = N(5, 0.25) \quad \Rightarrow \quad SE(\bar{X}) = \frac{5}{\sqrt{100}} = 0.5$$

Chuẩn hóa:

$$Z_1 = \frac{4.5 - 5}{0.5} = \frac{-0.5}{0.5} = -1.0$$

$$Z_2 = \frac{5.5 - 5}{0.5} = \frac{0.5}{0.5} = 1.0$$

$$P(4.5 \le \bar{X} \le 5.5) = P(-1.0 \le Z \le 1.0) = 2\Phi(1.0) - 1 = 2 \times 0.8413 - 1 = 0.6826$$

$$\boxed{P(4.5 \le \bar{X} \le 5.5) \approx 68.26\%}$$

**Kết luận:** Xác suất để thời gian chờ trung bình của $100$ khách nằm trong khoảng $4.5$ đến $5.5$ phút là khoảng $68.26\%$.

**Lý do dùng CLT:** Phân phối mũ không phải phân phối chuẩn, nhưng $n = 100 \ge 30$ → CLT có hiệu lực.

---

### Ví dụ 2 (Trung bình)

> **Exercise:** Exam scores at a university are normally distributed with $\mu = 70$ and $\sigma = 12$.
>
> (a) Find the probability that a **single student** scores above 80.  
> (b) Find the probability that the **sample mean** of $n = 36$ students is above 73.  
> (c) Why is the answer to (b) smaller than (a)?

**Tóm tắt bài toán:** Tổng thể chuẩn — so sánh phân phối cá thể với phân phối mẫu.

$$\mu = 70,\quad \sigma = 12$$

**(a) Xác suất một sinh viên > 80:**

$$Z = \frac{80 - 70}{12} = \frac{10}{12} = 0.833$$

$$P(X > 80) = P(Z > 0.833) = 1 - \Phi(0.833) = 1 - 0.7976 = 0.2024$$

**(b) Xác suất $\bar{X}_{36} > 73$:**

$$SE(\bar{X}) = \frac{12}{\sqrt{36}} = \frac{12}{6} = 2$$

$$Z = \frac{73 - 70}{2} = \frac{3}{2} = 1.5$$

$$P(\bar{X} > 73) = P(Z > 1.5) = 1 - \Phi(1.5) = 1 - 0.9332 = 0.0668$$

**(c) Tại sao kết quả (b) nhỏ hơn (a)?**

Phân phối mẫu $\bar{X}$ có **phương sai nhỏ hơn** phân phối tổng thể $X$:

$$\text{Var}(X) = 144 \gg \text{Var}(\bar{X}_{36}) = \frac{144}{36} = 4$$

$\bar{X}$ ít biến động hơn nhiều so với một quan sát đơn lẻ → xác suất đạt giá trị cực đoan thấp hơn nhiều.

$$\boxed{P(X > 80) = 20.24\% \gg P(\bar{X}_{36} > 73) = 6.68\%}$$

---

### Ví dụ 3 (Khó)

> **Exercise:** A production line produces electrical resistors. The resistance follows an **unknown distribution** with $\mu = 100$ ohms and $\sigma = 8$ ohms.
>
> (a) Can we use the CLT for $n = 16$? For $n = 50$?  
> (b) For $n = 64$, find the value $c$ such that $P(\bar{X} > c) = 0.05$.  
> (c) If the true mean shifts to $\mu = 103$ ohms, what is $P(\bar{X} > c)$ with the same $c$?

**Tóm tắt bài toán:** Phân phối chưa biết — ứng dụng CLT và phân tích power.

$$\mu = 100,\quad \sigma = 8$$

**(a) Điều kiện CLT:**

- $n = 16$: Với $n = 16 < 30$, CLT **chưa chắc đủ tin cậy** nếu phân phối gốc rất lệch. Cần thêm thông tin về hình dạng phân phối.
- $n = 50$: $n = 50 \ge 30$, CLT **áp dụng được** cho hầu hết phân phối.

**(b) Tìm $c$ với $n = 64$:**

$$SE(\bar{X}) = \frac{8}{\sqrt{64}} = \frac{8}{8} = 1 \quad \text{ohm}$$

$$P(\bar{X} > c) = 0.05 \Rightarrow P\!\left(Z > \frac{c-100}{1}\right) = 0.05$$

$$\frac{c-100}{1} = z_{0.05} = 1.645 \Rightarrow c = 100 + 1.645 = 101.645$$

$$\boxed{c = 101.645 \text{ ohm}}$$

**(c) $P(\bar{X} > 101.645)$ khi $\mu = 103$:**

$$SE(\bar{X}) = 1 \quad \text{(không thay đổi)}$$

$$Z = \frac{101.645 - 103}{1} = \frac{-1.355}{1} = -1.355$$

$$P(\bar{X} > 101.645 \mid \mu = 103) = P(Z > -1.355) = \Phi(1.355) \approx 0.9124$$

$$\boxed{P(\bar{X} > c \mid \mu = 103) \approx 91.24\%}$$

**Diễn giải:** Nếu trung bình thật sự dịch chuyển lên $103$ ohm (sản phẩm bị lỗi), quy trình kiểm định sẽ phát hiện ra điều này với xác suất khoảng $91.24\%$ — đây chính là **năng lực kiểm định (Power)** của quy trình này.

> [!warning] Sai lầm thường gặp
> - **Dùng $\sigma$ thay vì $\sigma/\sqrt{n}$** khi tính xác suất cho $\bar{X}$ — phải dùng sai số chuẩn.
> - **Dùng phân phối mẫu cho quan sát đơn lẻ**: $P(X > c)$ dùng phân phối gốc; $P(\bar{X} > c)$ dùng phân phối mẫu.
> - **Áp dụng CLT không điều kiện với $n$ nhỏ** — CLT cần $n$ đủ lớn.
