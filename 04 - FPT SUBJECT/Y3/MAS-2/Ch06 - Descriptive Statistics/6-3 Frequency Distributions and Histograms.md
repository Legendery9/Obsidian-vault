---
tags:
  - MAS291
  - Chapter6
  - DescriptiveStatistics
  - Histogram
  - FrequencyDistribution
aliases:
  - Frequency Distribution
  - Histogram
  - Bảng phân phối tần số
---

# 6.3 Phân Phối Tần Số và Histogram (Frequency Distributions and Histograms)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> **Bảng phân phối tần số (Frequency Distribution Table)** là bảng tóm tắt dữ liệu theo các **khoảng lớp (class intervals)** cùng với số lần xuất hiện trong mỗi khoảng.
>
> **Histogram** là biểu đồ dạng cột thể hiện bảng phân phối tần số — mỗi cột đại diện cho một khoảng lớp.

### Ý nghĩa thống kê

- Phân phối tần số và histogram cho phép nhìn thấy **hình dạng tổng thể** của phân phối dữ liệu.
- Phù hợp với **dữ liệu liên tục** và tập dữ liệu lớn.
- Giúp nhận diện: phân phối chuẩn, lệch phải/trái, hai đỉnh (bimodal), đều (uniform).

### Quy trình xây dựng

1. Xác định số khoảng lớp $k$ (thường $k \approx \sqrt{n}$ hoặc dùng quy tắc Sturges: $k = 1 + 3.322\log n$).
2. Tính độ rộng lớp: $h = (\text{Max} - \text{Min}) / k$ (làm tròn tiện lợi).
3. Xác định ranh giới các lớp (class boundaries).
4. Đếm tần số trong mỗi lớp.
5. Tính tần số tương đối và tần số tích lũy.

---

## 2. Ký hiệu và các tham số tham gia

> [!info] Ký hiệu

| Ký hiệu | Tên tiếng Việt (English) |
|:-------:|:------------------------|
| $k$ | Số khoảng lớp (Number of Class Intervals) |
| $h$ | Độ rộng khoảng lớp (Class Width) |
| $f_i$ | Tần số của lớp thứ $i$ (Frequency) |
| $f_i/n$ | Tần số tương đối (Relative Frequency) |
| $F_i$ | Tần số tích lũy (Cumulative Frequency) |
| $F_i/n$ | Tần số tương đối tích lũy (Cumulative Relative Frequency) |
| $n$ | Tổng số quan sát (Total Number of Observations) |

---

## 3. Phân loại và Công thức

### 3.1 Bảng phân phối tần số — Dữ liệu rời rạc

| Giá trị $x$ | Tần số $f$ | Tần số tương đối $f/n$ | Tần số tích lũy $F$ |
|:-----------:|:----------:|:----------------------:|:-------------------:|
| $x_1$ | $f_1$ | $f_1/n$ | $f_1$ |
| $x_2$ | $f_2$ | $f_2/n$ | $f_1+f_2$ |
| $\vdots$ | $\vdots$ | $\vdots$ | $\vdots$ |
| **Tổng** | $n$ | $1.000$ | — |

### 3.2 Bảng phân phối tần số — Dữ liệu liên tục (theo khoảng)

| Khoảng $[a_i, b_i)$ | Điểm giữa $m_i = (a_i+b_i)/2$ | $f_i$ | $f_i/n$ | $F_i$ |
|:-------------------:|:------------------------------:|:-----:|:-------:|:-----:|
| $[a_1, b_1)$ | $m_1$ | $f_1$ | — | $f_1$ |
| $[a_2, b_2)$ | $m_2$ | $f_2$ | — | $f_1+f_2$ |
| $\vdots$ | $\vdots$ | $\vdots$ | $\vdots$ | $\vdots$ |

### 3.3 Tính trung bình và phương sai từ bảng tần số

**Trung bình:**

$$\bar{x} = \frac{\sum f_i m_i}{n}$$

**Phương sai:**

$$s^2 = \frac{\sum f_i m_i^2 - n\bar{x}^2}{n-1}$$

---

## 4. Ví dụ minh họa

### Ví dụ 1 (Dễ)

> **Exercise:** The following data represent the number of customer service calls received per day over 10 days: 5, 3, 7, 4, 6, 5, 8, 4, 5, 3. Construct a frequency distribution table and calculate the mean and variance.

**Tóm tắt bài toán:** Bảng phân phối tần số cho dữ liệu rời rạc, $n = 10$.

**Giải:**

| Số cuộc gọi $x$ | Tần số $f$ | $f/n$ | $F$ | $fx$ | $fx^2$ |
|:--------------:|:---------:|:-----:|:---:|:----:|:------:|
| 3 | 2 | 0.20 | 2 | 6 | 18 |
| 4 | 2 | 0.20 | 4 | 8 | 32 |
| 5 | 3 | 0.30 | 7 | 15 | 75 |
| 6 | 1 | 0.10 | 8 | 6 | 36 |
| 7 | 1 | 0.10 | 9 | 7 | 49 |
| 8 | 1 | 0.10 | 10 | 8 | 64 |
| **Tổng** | **10** | **1.00** | — | **50** | **274** |

$$\bar{x} = \frac{50}{10} = 5.0 \text{ cuộc gọi/ngày}$$

$$s^2 = \frac{274 - 10 \times 25}{9} = \frac{274 - 250}{9} = \frac{24}{9} \approx 2.67$$

$$s \approx 1.63 \text{ cuộc gọi}$$

**Kết luận:** Số cuộc gọi trung bình là $5.0$/ngày với độ lệch chuẩn $1.63$.

---

### Ví dụ 2 (Trung bình)

> **Exercise:** The tensile strength (MPa) of 25 steel specimens is given. Construct a frequency distribution with 5 classes and a histogram. Data: 312, 325, 318, 342, 356, 329, 315, 348, 333, 321, 365, 308, 337, 344, 319, 352, 326, 341, 358, 330, 317, 339, 346, 323, 360.

**Tóm tắt bài toán:** Bảng phân phối cho dữ liệu liên tục với $k = 5$, $n = 25$.

**Giải:**

Min = 308, Max = 365 → Range = 57.

$$h = \lceil 57/5 \rceil = 12 \text{ MPa}$$

| Lớp $[a, b)$ | Điểm giữa $m$ | Tần số $f$ | $f/n$ | $F$ |
|:------------:|:-------------:|:----------:|:-----:|:---:|
| [308, 320) | 314 | 6 | 0.24 | 6 |
| [320, 332) | 326 | 7 | 0.28 | 13 |
| [332, 344) | 338 | 5 | 0.20 | 18 |
| [344, 356) | 350 | 5 | 0.20 | 23 |
| [356, 368) | 362 | 2 | 0.08 | 25 |
| **Tổng** | — | **25** | **1.00** | — |

**Nhận xét histogram:** Phân phối hơi lệch phải (đuôi phải dài — lớp $[356,368)$ có ít quan sát nhưng trải rộng về phía giá trị lớn).

---

### Ví dụ 3 (Khó)

> **Exercise:** Using the frequency distribution from Example 2, compute the approximate sample mean $\bar{x}$ and standard deviation $s$ using class midpoints. Compare with the exact values computed from raw data.

**Tóm tắt bài toán:** Ước lượng $\bar{x}$ và $s$ từ bảng tần số.

| $m_i$ | $f_i$ | $f_i m_i$ | $f_i m_i^2$ |
|:-----:|:-----:|:---------:|:-----------:|
| 314 | 6 | 1884 | 591,576 |
| 326 | 7 | 2282 | 744,532 |
| 338 | 5 | 1690 | 571,220 |
| 350 | 5 | 1750 | 612,500 |
| 362 | 2 | 724 | 262,088 |
| **Tổng** | **25** | **8330** | **2,781,916** |

$$\bar{x}_{approx} = \frac{8330}{25} = 333.2 \text{ MPa}$$

$$s^2_{approx} = \frac{2,781,916 - 25 \times 333.2^2}{24} = \frac{2,781,916 - 2,776,540}{24} = \frac{5376}{24} = 224$$

$$s_{approx} = \sqrt{224} \approx 14.97 \text{ MPa}$$

**Giá trị chính xác từ dữ liệu thô:** $\bar{x}_{exact} = 334.76$ MPa, $s_{exact} \approx 16.28$ MPa.

**Nhận xét:** Ước lượng từ bảng tần số có sai số nhỏ do sử dụng điểm giữa lớp thay cho giá trị thực. Đây là đánh đổi giữa **sự tiện lợi** và **độ chính xác**.

> [!warning] Sai lầm thường gặp
> - **Chọn số lớp quá ít** (k quá nhỏ): Mất chi tiết.
> - **Chọn số lớp quá nhiều**: Histogram "lởm chởm", khó nhận ra hình dạng.
> - **Khoảng lớp không đồng đều**: Gây nhầm lẫn khi đọc biểu đồ.
> - **Nhầm tần số với tần số tương đối** khi tính trung bình từ bảng.
