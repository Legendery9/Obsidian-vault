---
tags:
  - MAS291
  - Chapter6
  - DescriptiveStatistics
  - NumericalSummary
aliases:
  - Numerical Summaries
  - Tóm tắt số
  - Thống kê mô tả
---

# 6.1 Tóm Tắt Số của Dữ Liệu (Numerical Summaries of Data)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> **Thống kê mô tả (Descriptive Statistics)** sử dụng các **đại lượng số** để mô tả và tóm tắt đặc điểm của tập dữ liệu, bao gồm: **vị trí trung tâm, độ phân tán, và hình dạng phân phối**.

### Ý nghĩa thống kê

Tóm tắt số giúp:
1. **Mô tả trung tâm**: dữ liệu tập trung quanh giá trị nào?
2. **Mô tả phân tán**: dữ liệu trải rộng đến mức nào?
3. **Mô tả hình dạng**: phân phối lệch trái, lệch phải, hay đối xứng?

### Quy trình cơ bản

1. Thu thập dữ liệu mẫu $x_1, x_2, \ldots, x_n$.
2. Tính các đo lường trung tâm ($\bar{x}$, median, mode).
3. Tính các đo lường phân tán ($s^2$, $s$, $IQR$).
4. Tính các đo lường hình dạng (skewness, kurtosis nếu cần).

---

## 2. Ký hiệu và các tham số tham gia

> [!info] Ký hiệu

| Ký hiệu | Tên tiếng Việt (English) |
|:-------:|:------------------------|
| $n$ | Cỡ mẫu (Sample Size) |
| $x_i$ | Giá trị quan sát thứ $i$ (Observation) |
| $\bar{x}$ | Trung bình mẫu (Sample Mean) |
| $\tilde{x}$ | Trung vị mẫu (Sample Median) |
| $s^2$ | Phương sai mẫu (Sample Variance) |
| $s$ | Độ lệch chuẩn mẫu (Sample Standard Deviation) |
| $Q_1, Q_2, Q_3$ | Tứ phân vị (Quartiles) |
| $IQR$ | Khoảng tứ phân vị (Interquartile Range) |

---

## 3. Phân loại và Công thức

### 3.1 Đo lường trung tâm (Measures of Central Tendency)

#### Trung bình mẫu (Sample Mean)

$$\bar{x} = \frac{1}{n}\sum_{i=1}^n x_i = \frac{x_1 + x_2 + \cdots + x_n}{n}$$

- Bị ảnh hưởng bởi **ngoại lệ (outliers)**.
- Là ước lượng của $\mu$ (trung bình tổng thể).

#### Trung vị mẫu (Sample Median)

Sắp xếp dữ liệu tăng dần $x_{(1)} \le x_{(2)} \le \cdots \le x_{(n)}$:

$$\tilde{x} = \begin{cases} x_{(n+1)/2} & \text{nếu } n \text{ lẻ} \\ \dfrac{x_{(n/2)} + x_{(n/2+1)}}{2} & \text{nếu } n \text{ chẵn} \end{cases}$$

- **Không bị ảnh hưởng** bởi ngoại lệ → phù hợp khi có giá trị cực đoan.

#### Mode (Yếu vị)

Giá trị xuất hiện **nhiều lần nhất** trong tập dữ liệu.

---

### 3.2 Đo lường phân tán (Measures of Variability)

#### Phương sai mẫu (Sample Variance)

$$s^2 = \frac{\sum_{i=1}^n (x_i - \bar{x})^2}{n-1} = \frac{\sum x_i^2 - n\bar{x}^2}{n-1}$$

#### Độ lệch chuẩn mẫu (Sample Standard Deviation)

$$s = \sqrt{s^2}$$

#### Khoảng biến thiên (Range)

$$R = x_{(n)} - x_{(1)} = \text{Max} - \text{Min}$$

#### Khoảng tứ phân vị (IQR)

$$IQR = Q_3 - Q_1$$

---

### 3.3 Tóm tắt 5 số (Five-Number Summary)

$$\{Q_0 = \text{Min},\; Q_1,\; Q_2 = \text{Median},\; Q_3,\; Q_4 = \text{Max}\}$$

---

### 3.4 Phát hiện ngoại lệ (Outlier Detection)

$$\text{Lower Fence} = Q_1 - 1.5 \times IQR$$

$$\text{Upper Fence} = Q_3 + 1.5 \times IQR$$

Nếu $x_i < \text{Lower Fence}$ hoặc $x_i > \text{Upper Fence}$ → $x_i$ là **ngoại lệ**.

---

## 4. Ví dụ minh họa

### Ví dụ 1 (Dễ)

> **Exercise:** The following data represent the ages (in years) of $n = 9$ employees: 25, 32, 28, 35, 29, 31, 26, 40, 30. Compute $\bar{x}$, median, and $s^2$.

**Tóm tắt bài toán:** Tính các đo lường trung tâm và phân tán.

**Giải:**

**Bước 1:** Sắp xếp: $25, 26, 28, 29, 30, 31, 32, 35, 40$.

**Trung bình:**

$$\bar{x} = \frac{25+26+28+29+30+31+32+35+40}{9} = \frac{276}{9} = 30.67 \text{ tuổi}$$

**Trung vị:** $n = 9$ lẻ → vị trí $(9+1)/2 = 5$ → $\tilde{x} = 30$ tuổi.

**Phương sai:**

$$\sum x_i^2 = 625+676+784+841+900+961+1024+1225+1600 = 8636$$

$$s^2 = \frac{8636 - 9 \times 30.67^2}{8} = \frac{8636 - 8463.4}{8} = \frac{172.6}{8} \approx 21.58$$

$$s \approx 4.65 \text{ tuổi}$$

**Kết luận:** Tuổi trung bình nhân viên là $30.67$ tuổi, trung vị là $30$ tuổi, với độ lệch chuẩn $4.65$ tuổi.

---

### Ví dụ 2 (Trung bình)

> **Exercise:** The monthly salaries (in \$1000) of $n = 8$ employees are: 3.2, 4.5, 3.8, 5.1, 4.0, 3.6, 8.5, 4.2. Compute the five-number summary and identify any outliers using the IQR method.

**Tóm tắt bài toán:** Tóm tắt 5 số và phát hiện ngoại lệ.

**Sắp xếp:** $3.2, 3.6, 3.8, 4.0, 4.2, 4.5, 5.1, 8.5$. $\quad n = 8$.

$$\tilde{x} = \frac{4.0 + 4.2}{2} = 4.1$$

$$Q_1: \text{vị trí } \frac{8+1}{4} = 2.25 \Rightarrow Q_1 = 3.6 + 0.25(3.8-3.6) = 3.65$$

$$Q_3: \text{vị trí } \frac{3(8+1)}{4} = 6.75 \Rightarrow Q_3 = 4.5 + 0.75(5.1-4.5) = 4.95$$

$$IQR = 4.95 - 3.65 = 1.30$$

$$\text{Lower Fence} = 3.65 - 1.5 \times 1.30 = 3.65 - 1.95 = 1.70$$

$$\text{Upper Fence} = 4.95 + 1.5 \times 1.30 = 4.95 + 1.95 = 6.90$$

Kiểm tra: $8.5 > 6.90$ → **$8.5$ là ngoại lệ** (outlier).

**Tóm tắt 5 số:** $\{3.2, 3.65, 4.1, 4.95, 8.5\}$ (min, $Q_1$, median, $Q_3$, max).

**Kết luận:** Có một nhân viên có lương $\$8,500$ — là ngoại lệ so với phần còn lại.

---

### Ví dụ 3 (Khó)

> **Exercise:** Two machines produce bolts. Machine A: 22 samples with $\bar{x}_A = 50.2$ mm, $s_A = 0.8$ mm. Machine B: 30 samples with $\bar{x}_B = 49.8$ mm, $s_B = 1.5$ mm. 
>
> (a) Which machine produces bolts with more consistent length?  
> (b) Compute the **combined sample mean** of all 52 bolts.  
> (c) If the target is $50 \pm 2$ mm, which machine performs better?

**Giải:**

**(a) Tính hệ số biến thiên (Coefficient of Variation — CV):**

$$CV_A = \frac{s_A}{\bar{x}_A} = \frac{0.8}{50.2} \approx 1.59\%$$

$$CV_B = \frac{s_B}{\bar{x}_B} = \frac{1.5}{49.8} \approx 3.01\%$$

$CV_A < CV_B$ → **Máy A nhất quán hơn** (ít biến thiên hơn tương đối với trung bình).

**(b) Trung bình tổ hợp (Combined Mean):**

$$\bar{x}_{combined} = \frac{n_A \bar{x}_A + n_B \bar{x}_B}{n_A + n_B} = \frac{22 \times 50.2 + 30 \times 49.8}{52} = \frac{1104.4 + 1494}{52} = \frac{2598.4}{52} \approx 49.97 \text{ mm}$$

**(c) Phân tích theo yêu cầu kỹ thuật:**

| Máy | $\bar{x}$ | $s$ | $\bar{x} \pm 3s$ (99.7% sản phẩm) |
|:---:|:---------:|:---:|:----------------------------------:|
| A | 50.2 | 0.8 | $[47.8, 52.6]$ |
| B | 49.8 | 1.5 | $[45.3, 54.3]$ |

Giới hạn kỹ thuật: $[48, 52]$.

Máy A: $[47.8, 52.6]$ — hầu hết nằm trong giới hạn nhưng đuôi trái hơi vượt quá.
Máy B: $[45.3, 54.3]$ — phân tán nhiều hơn, một số sản phẩm sẽ nằm ngoài giới hạn.

**Kết luận:** **Máy A** hoạt động tốt hơn — trung bình gần mục tiêu hơn và độ phân tán nhỏ hơn.

> [!warning] Sai lầm thường gặp
> - **Nhầm trung bình với trung vị**: Khi có ngoại lệ, nên dùng trung vị thay trung bình.
> - **Dùng $n$ thay $n-1$** trong $s^2$: Luôn dùng $n-1$ cho **phương sai mẫu**.
> - **Quên sắp xếp dữ liệu** trước khi tính median và quartiles.
