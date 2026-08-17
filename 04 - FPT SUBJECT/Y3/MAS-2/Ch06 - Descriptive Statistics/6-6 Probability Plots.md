---
tags:
  - MAS291
  - Chapter6
  - DescriptiveStatistics
  - NormalProbabilityPlot
  - QQPlot
aliases:
  - Probability Plot
  - Normal Probability Plot
  - Q-Q Plot
  - Biểu đồ xác suất chuẩn
---

# 6.6 Biểu Đồ Xác Suất (Probability Plots)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> **Biểu đồ xác suất (Probability Plot)**, đặc biệt là **biểu đồ xác suất chuẩn (Normal Probability Plot** hay **Q-Q Plot)**, là công cụ đồ thị dùng để **kiểm tra giả định phân phối chuẩn** của dữ liệu.

### Ý nghĩa thống kê

- Nhiều phương pháp thống kê (t-test, ANOVA, hồi quy) yêu cầu giả định tổng thể có **phân phối chuẩn**.
- Biểu đồ xác suất chuẩn là cách trực quan để **kiểm tra giả định này** trước khi áp dụng các phương pháp đó.
- Nếu dữ liệu chuẩn → các điểm trên biểu đồ xấp xỉ **thẳng hàng** trên một đường thẳng.

### Nguyên tắc

Nếu $X \sim N(\mu, \sigma^2)$, thì quantile thứ $p$ của $X$ là:

$$x_p = \mu + \sigma \cdot z_p$$

trong đó $z_p = \Phi^{-1}(p)$ là quantile chuẩn hóa tương ứng.

Vẽ $(z_p, x_{(i)})$ → nếu dữ liệu chuẩn, phải là đường thẳng.

---

## 2. Ký hiệu và các tham số tham gia

> [!info] Ký hiệu

| Ký hiệu | Tên tiếng Việt (English) |
|:-------:|:------------------------|
| $x_{(i)}$ | Thống kê thứ tự (Order Statistic): giá trị thứ $i$ sau khi sắp xếp tăng dần |
| $z_{p_i}$ | Quantile chuẩn hóa (Normal Score / Theoretical Quantile) |
| $p_i$ | Xác suất tích lũy ứng với quan sát thứ $i$ |
| $\Phi^{-1}(p)$ | Hàm phân vị nghịch đảo của phân phối chuẩn (Inverse Normal CDF) |

---

## 3. Phân loại và Công thức

### 3.1 Quy trình xây dựng Normal Probability Plot

1. Sắp xếp dữ liệu tăng dần: $x_{(1)} \le x_{(2)} \le \cdots \le x_{(n)}$.
2. Tính $p_i$ ứng với mỗi quan sát: 

$$p_i = \frac{i - 0.5}{n} \quad \text{(công thức phổ biến)}$$

3. Tính normal score: $z_i = \Phi^{-1}(p_i)$ (tra bảng $Z$ nghịch đảo).
4. Vẽ điểm $(z_i, x_{(i)})$.
5. Đánh giá mức độ thẳng hàng.

### 3.2 Diễn giải biểu đồ

| Hình dạng | Kết luận |
|:---------|:---------|
| Gần thẳng hàng trên đường thẳng | Dữ liệu **tuân theo phân phối chuẩn** |
| Cong lên ở đuôi phải | Phân phối **lệch phải** (right-skewed) |
| Cong xuống ở đuôi trái | Phân phối **lệch trái** (left-skewed) |
| Cong kiểu chữ S | Phân phối **đuôi dày** (heavy-tailed) hơn chuẩn |
| Điểm ngoại lệ rõ ràng | Có **ngoại lệ** hoặc sai sót dữ liệu |

> [!warning]
> Biểu đồ xác suất chỉ là kiểm tra **trực quan** — với mẫu nhỏ ($n < 30$), dễ nhầm lẫn. Nên kết hợp với kiểm định thống kê (Shapiro-Wilk, Anderson-Darling) để có kết luận chắc chắn hơn.

---

## 4. Ví dụ minh họa

### Ví dụ 1 (Dễ)

> **Exercise:** A sample of $n = 8$ measurements yields (sorted): 12.1, 13.4, 14.2, 15.0, 15.8, 16.5, 17.3, 18.9. Construct a normal probability plot and assess normality.

**Tóm tắt bài toán:** Xây dựng và đọc biểu đồ xác suất chuẩn.

**Giải:**

| $i$ | $x_{(i)}$ | $p_i = (i-0.5)/8$ | $z_i = \Phi^{-1}(p_i)$ |
|:---:|:---------:|:-----------------:|:----------------------:|
| 1 | 12.1 | 0.0625 | $-1.534$ |
| 2 | 13.4 | 0.1875 | $-0.887$ |
| 3 | 14.2 | 0.3125 | $-0.489$ |
| 4 | 15.0 | 0.4375 | $-0.157$ |
| 5 | 15.8 | 0.5625 | $+0.157$ |
| 6 | 16.5 | 0.6875 | $+0.489$ |
| 7 | 17.3 | 0.8125 | $+0.887$ |
| 8 | 18.9 | 0.9375 | $+1.534$ |

Vẽ $z_i$ trên trục x, $x_{(i)}$ trên trục y:

Các điểm: $(-1.534, 12.1)$, $(-0.887, 13.4)$, ..., $(1.534, 18.9)$.

**Nhận xét:** Các điểm xấp xỉ thẳng hàng → dữ liệu **có thể tuân theo phân phối chuẩn**.

---

### Ví dụ 2 (Trung bình)

> **Exercise:** Explain what each of the following normal probability plot shapes indicates:
> (a) Points curve upward at the right tail.
> (b) Points lie closely along a straight line except for one point far above at the right.
> (c) Points form an S-curve.

**Giải:**

**(a) Cong lên ở đuôi phải:**

$$\Rightarrow \text{Phân phối \textbf{lệch phải (right-skewed)}}$$

Giá trị thực ở đuôi phải lớn hơn kỳ vọng theo phân phối chuẩn. Ví dụ: thu nhập, giá cổ phiếu, thời gian sửa chữa.

**(b) Hầu hết thẳng hàng, trừ một điểm xa ở phải:**

$$\Rightarrow \text{Dữ liệu \textbf{gần chuẩn} nhưng có một \textbf{ngoại lệ (outlier)}}$$

Cần điều tra điểm bất thường đó — có thể là sai số nhập liệu hoặc hiện tượng đặc biệt.

**(c) Đường cong chữ S:**

$$\Rightarrow \text{Phân phối \textbf{đuôi dày hơn chuẩn (heavy-tailed / leptokurtic)}}$$

Ví dụ: phân phối $t$ với bậc tự do nhỏ, hoặc phân phối Laplace. Giá trị ở cả hai đuôi lớn hơn kỳ vọng chuẩn.

---

### Ví dụ 3 (Khó)

> **Exercise:** A chemical process produces batches. The yield (%) from 10 batches is: 91.2, 88.5, 93.1, 90.0, 87.8, 94.5, 89.3, 92.0, 86.7, 95.3. 
>
> (a) Construct a normal probability plot.  
> (b) Is the normality assumption reasonable?  
> (c) Based on your answer, is it appropriate to use a one-sample t-test on this data?

**Giải:**

**Sắp xếp:** 86.7, 87.8, 88.5, 89.3, 90.0, 91.2, 92.0, 93.1, 94.5, 95.3. $\quad n = 10$.

| $i$ | $x_{(i)}$ | $p_i$ | $z_i$ |
|:---:|:---------:|:-----:|:-----:|
| 1 | 86.7 | 0.05 | $-1.645$ |
| 2 | 87.8 | 0.15 | $-1.036$ |
| 3 | 88.5 | 0.25 | $-0.674$ |
| 4 | 89.3 | 0.35 | $-0.385$ |
| 5 | 90.0 | 0.45 | $-0.126$ |
| 6 | 91.2 | 0.55 | $+0.126$ |
| 7 | 92.0 | 0.65 | $+0.385$ |
| 8 | 93.1 | 0.75 | $+0.674$ |
| 9 | 94.5 | 0.85 | $+1.036$ |
| 10 | 95.3 | 0.95 | $+1.645$ |

**Nhận xét:** Các điểm phân bố khá đều quanh đường thẳng $(z_i, x_{(i)})$ → không có dấu hiệu vi phạm chuẩn.

**(b) Kết luận về chuẩn:** Với $n = 10$, biểu đồ không cho thấy sự lệch rõ ràng khỏi đường thẳng → giả định chuẩn **hợp lý** (nhưng với $n$ nhỏ, khó kết luận chắc chắn).

**(c) Phù hợp dùng t-test?** Có — vì giả định tổng thể chuẩn được hỗ trợ bởi biểu đồ xác suất, và đây là điều kiện cần cho one-sample t-test khi $n$ nhỏ.

> [!warning] Sai lầm thường gặp
> - **Kỳ vọng đường hoàn toàn thẳng**: Với mẫu nhỏ, biến động ngẫu nhiên khiến đường có thể hơi cong dù dữ liệu thực sự chuẩn.
> - **Bỏ qua kiểm định hình thức**: Biểu đồ xác suất chỉ là kiểm tra trực quan — nên kết hợp kiểm định Shapiro-Wilk với mẫu nhỏ.
> - **Nhầm biểu đồ xác suất với biểu đồ tán xạ thông thường**: Trục x là **normal score** ($z$), không phải giá trị quan sát.
