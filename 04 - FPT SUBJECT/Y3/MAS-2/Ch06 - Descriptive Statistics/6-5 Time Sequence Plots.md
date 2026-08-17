---
tags:
  - MAS291
  - Chapter6
  - DescriptiveStatistics
  - TimeSeriesPlot
aliases:
  - Time Sequence Plot
  - Biểu đồ chuỗi thời gian
  - Run Chart
---

# 6.5 Biểu Đồ Chuỗi Thời Gian (Time Sequence Plots)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> **Biểu đồ chuỗi thời gian (Time Sequence Plot** hay **Run Chart)** là biểu đồ thể hiện **giá trị quan sát theo thứ tự thời gian** hoặc thứ tự lấy mẫu.

### Ý nghĩa thống kê

- Phát hiện **xu hướng (trend)**: tăng, giảm dần theo thời gian.
- Phát hiện **chu kỳ (cycle)**: dao động tuần hoàn.
- Phát hiện **biến động đột ngột (shift)**: sự thay đổi đột ngột trong giá trị trung bình.
- Phát hiện **điểm dị thường (anomaly)**: giá trị bất thường trong chuỗi.
- Được dùng nhiều trong **kiểm soát chất lượng (Statistical Process Control — SPC)**.

### Sự khác biệt với histogram

| | Time Sequence Plot | Histogram |
|:--|:--:|:--:|
| Trục x | Thời gian / thứ tự quan sát | Giá trị của biến |
| Thể hiện | Biến động theo thời gian | Phân phối tần số |
| Phát hiện | Xu hướng, chu kỳ | Hình dạng phân phối |

---

## 2. Ký hiệu và các tham số tham gia

> [!info] Ký hiệu

| Ký hiệu | Tên tiếng Việt (English) |
|:-------:|:------------------------|
| $t$ | Thời điểm hoặc thứ tự quan sát (Time Point / Order) |
| $x_t$ | Giá trị tại thời điểm $t$ (Observation at Time $t$) |
| $\bar{x}$ | Trung bình tổng thể của chuỗi (Overall Mean) |
| UCL | Giới hạn kiểm soát trên (Upper Control Limit) |
| LCL | Giới hạn kiểm soát dưới (Lower Control Limit) |

---

## 3. Phân loại và Công thức

### 3.1 Cách xây dựng

1. Trục hoành (x): thứ tự thời gian hoặc số thứ tự quan sát.
2. Trục tung (y): giá trị đo lường.
3. Vẽ các điểm và nối chúng.
4. Vẽ đường tham chiếu (ví dụ: trung bình $\bar{x}$).

### 3.2 Nhận diện mẫu (Pattern Recognition)

| Mẫu | Mô tả | Ý nghĩa |
|:----|:------|:--------|
| **Xu hướng (Trend)** | Các điểm tăng/giảm đều đặn | Quy trình đang thay đổi có hệ thống |
| **Chu kỳ (Cycle)** | Dao động lên xuống tuần hoàn | Ảnh hưởng theo mùa hoặc chu kỳ sản xuất |
| **Ổn định (Stable)** | Dao động ngẫu nhiên quanh $\bar{x}$ | Quy trình trong tầm kiểm soát |
| **Biến động đột ngột (Shift)** | Giá trị nhảy lên/xuống bất ngờ | Thay đổi máy móc, nguyên liệu, v.v. |

---

## 4. Ví dụ minh họa

### Ví dụ 1 (Dễ)

> **Exercise:** The temperature (°C) inside a laboratory refrigerator is recorded every hour for 12 hours: 4.1, 3.9, 4.0, 4.2, 4.1, 4.3, 4.2, 4.4, 4.5, 4.6, 4.7, 4.8. Describe what the time sequence plot reveals.

**Tóm tắt bài toán:** Nhận diện xu hướng từ chuỗi thời gian.

**Giải:**

Quan sát dãy số: $4.1, 3.9, 4.0, 4.2, 4.1, 4.3, 4.2, 4.4, 4.5, 4.6, 4.7, 4.8$.

$$\bar{x} = \frac{4.1+3.9+4.0+4.2+4.1+4.3+4.2+4.4+4.5+4.6+4.7+4.8}{12} = \frac{51.8}{12} \approx 4.32 \text{°C}$$

Từ giờ thứ 6 trở đi, nhiệt độ **tăng đều đặn** từ $4.3$ lên $4.8$°C.

**Kết luận:** Biểu đồ chuỗi thời gian cho thấy rõ **xu hướng tăng (upward trend)** trong nửa sau quan sát. Đây có thể là dấu hiệu tủ lạnh đang bắt đầu gặp vấn đề — cần kiểm tra thiết bị.

**Tại sao không dùng histogram?** Histogram chỉ cho thấy phân phối giá trị, không phát hiện được xu hướng theo thời gian — điều quan trọng trong bài này.

---

### Ví dụ 2 (Trung bình)

> **Exercise:** A factory monitors the diameter (mm) of bolts produced each hour. Over 10 hours, measurements are: 25.1, 25.0, 25.2, 25.1, 25.3, 24.9, 25.0, 25.1, 25.0, 25.2. Compute $\bar{x}$, identify any unusual patterns, and determine if the process appears stable.

**Tóm tắt bài toán:** Kiểm tra sự ổn định của quy trình.

$$\bar{x} = \frac{251.9}{10} = 25.19 \text{ mm}$$

$$s = \sqrt{\frac{\sum x_i^2 - 10\bar{x}^2}{9}} \approx 0.12 \text{ mm}$$

**Giới hạn tham chiếu:** $\bar{x} \pm 2s \approx [24.95, 25.43]$ mm.

Tất cả $10$ giá trị nằm trong khoảng $[24.9, 25.3]$ ⊂ $[24.95, 25.43]$ — nhưng $24.9$ (giờ 6) **hơi thấp** so với các giá trị khác.

**Kết luận:** Quy trình nhìn chung **ổn định** — các điểm dao động ngẫu nhiên quanh $\bar{x} = 25.19$ mm. Không có xu hướng rõ ràng. Cần theo dõi tiếp giờ thứ 6 (giá trị $24.9$) xem có xảy ra lại không.

---

### Ví dụ 3 (Khó)

> **Exercise:** A production process records defect counts per batch over 20 batches: 3, 2, 4, 3, 2, 3, 5, 4, 6, 7, 8, 7, 9, 8, 10, 9, 11, 10, 12, 11. The target is ≤ 5 defects/batch.
>
> (a) Compute the overall mean and describe the time sequence plot.  
> (b) At which batch does the process appear to shift above the target?  
> (c) What actions would you recommend?

**Giải:**

$$\bar{x} = \frac{3+2+4+3+2+3+5+4+6+7+8+7+9+8+10+9+11+10+12+11}{20} = \frac{143}{20} = 7.15 \text{ lỗi/mẻ}$$

**(a) Mô tả biểu đồ:** Từ mẻ $1$-$6$: số lỗi dao động ổn định ở mức $2$-$5$. Từ mẻ $7$ trở đi: số lỗi **tăng đều đặn** từ $5$ lên $12$ — xu hướng tăng rõ ràng.

**(b) Điểm shift:**

Từ mẻ 7 ($5$ lỗi → $6$ lỗi mẻ 9), quy trình bắt đầu **vượt mục tiêu**. Cụ thể, từ **mẻ 9** trở đi, số lỗi liên tục $> 5$.

**(c) Khuyến nghị:**

1. **Điều tra nguyên nhân** từ mẻ 7-9: thay đổi nhà cung cấp nguyên liệu? Bảo trì máy? Thay ca làm việc?
2. **Tạm dừng sản xuất** để kiểm tra và hiệu chỉnh máy.
3. **Lập biểu đồ kiểm soát (control chart)** để giám sát liên tục.

> [!warning] Sai lầm thường gặp
> - **Nhầm lẫn với đồ thị tán xạ (scatter plot)**: Time sequence plot có trục x là thứ tự thời gian; scatter plot có cả hai trục là biến định lượng.
> - **Chỉ nhìn vào histogram**: Histogram không cho thấy xu hướng thời gian — cần thêm time sequence plot.
> - **Bỏ qua outlier đơn lẻ**: Một điểm bất thường đơn lẻ trong chuỗi thời gian có thể là dấu hiệu sự cố cần điều tra ngay.
