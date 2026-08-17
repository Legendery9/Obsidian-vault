---
tags:
  - MAS291
  - Chapter10
  - TwoSamples
  - Inference
aliases:
  - Statistical Inference Two Samples Introduction
  - Suy diễn thống kê hai mẫu
---

# 10.0 Suy Diễn Thống Kê cho Hai Mẫu — Giới Thiệu

## 1. Định nghĩa và tóm gọn

> [!abstract] Tổng quan Chapter 10
> Chương 10 mở rộng từ **suy diễn một mẫu** (Ch8, Ch9) sang **so sánh hai tổng thể** — trả lời các câu hỏi như:
> - Trung bình hai nhóm có khác nhau không? ($\mu_1 - \mu_2$)
> - Tỷ lệ hai nhóm có khác nhau không? ($p_1 - p_2$)
> - Phương sai hai nhóm có bằng nhau không? ($\sigma_1^2 / \sigma_2^2$)

### Phân loại

| Phần | Tham số | Phương pháp |
|:-----|:-------:|:------------|
| [[10-1 Inference on the Difference in Means - Variances Known]] | $\mu_1 - \mu_2$ | Z-test / Z-interval (biết $\sigma$) |
| [[10-2 Inference on the Difference in Means - Variances Unknown]] | $\mu_1 - \mu_2$ | t-test / t-interval (không biết $\sigma$) |
| [[10-4 Paired t-Test]] | $\mu_D$ | Paired t-test / t-interval |
| [[10-5 Inference on the Variances of Two Normal Distributions]] | $\sigma_1^2/\sigma_2^2$ | F-test / F-interval |
| [[10-6 Inference on Two Population Proportions]] | $p_1 - p_2$ | Z-test / Z-interval |

### Điều kiện chung

- Hai mẫu phải là **mẫu ngẫu nhiên độc lập** (trừ paired t-test).
- Cỡ mẫu đủ lớn hoặc tổng thể có phân phối chuẩn.
