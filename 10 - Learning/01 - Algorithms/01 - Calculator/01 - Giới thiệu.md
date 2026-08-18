# Giới thiệu nhóm Thuật toán Máy tính (Calculator)

---

## Định nghĩa
Nhóm thuật toán máy tính bao gồm các phương pháp tính toán cơ sở và biểu diễn số học nền tảng phục vụ cho phần cứng và phần mềm máy tính (như chuyển đổi hệ cơ số, nhân ma trận, tính toán độ chính xác cao).

---

## Tác dụng
- **Nền tảng của Khoa học máy tính:** Mọi dữ liệu (hình ảnh, âm thanh, văn bản) cuối cùng đều được máy tính biểu diễn dưới dạng số nhị phân ($0$ và $1$).
- **Tối ưu hóa các phép tính phức tạp:** Sử dụng các thuật toán như Horner để chuyển đổi hệ cơ số hoặc Strassen để nhân ma trận giúp giảm thiểu tối đa số lượng phép nhân/phép cộng cần thực hiện trên CPU/GPU.

---

## Bảng tham chiếu

### Tóm tắt các chủ đề cốt lõi của nhóm Máy tính

| Chủ đề | Thuật toán / Nguyên lý cốt lõi | Ý nghĩa & Ứng dụng |
| :--- | :--- | :--- |
| **Chuyển đổi cơ số** | - Thuật toán Horner (Hệ bất kỳ $\to$ Thập phân)<br>- Phép chia lấy dư ngược (Thập phân $\to$ Hệ bất kỳ) | Chuyển đổi qua lại giữa các hệ nhị phân (Binary - 2), bát phân (Octal - 8), thập phân (Decimal - 10), thập lục phân (Hex - 16). |
| **Nhân ma trận** | - Thuật toán nhân ma trận ngây thơ ($O(N^3)$)<br>- Thuật toán Strassen ($O(N^{2.807})$) | Cơ sở cho tính toán đồ họa 3D, học sâu (Deep Learning) và xử lý ảnh số. |

---

## Ví dụ
Xem chi tiết các phương pháp triển khai cụ thể tại:
- [[02 - Base Conversion]] (Chuyển đổi giữa các hệ số)
- [[03 - Matrix Multiplication]] (Thuật toán nhân hai ma trận)
