# Common Regex Patterns

> [!abstract] Định nghĩa
> Tài liệu này tổng hợp các biểu thức chính quy (Regex Pattern) phổ biến, thường gặp nhất trong lập trình thực tế (nguyên lý 20/80) dùng để xác thực dữ liệu đầu vào. Do ký tự `\` là ký tự thoát (escape character) trong Java, hãy nhớ viết **double backslash (`\\`)** trong chuỗi Java.

---

> [!info] Ký hiệu Regex cơ bản đi kèm
> - `^` : Bắt đầu chuỗi.
> - `$` : Kết thúc chuỗi.
> - `\d` (Java: `\\d`) : Chữ số `[0-9]`.
> - `\w` (Java: `\\w`) : Chữ cái, chữ số, hoặc dấu gạch dưới `_`.
> - `\s` (Java: `\\s`) : Khoảng trắng (dấu cách, tab, xuống dòng).
> - `+` : Lặp lại 1 hoặc nhiều lần.
> - `*` : Lặp lại 0 hoặc nhiều lần.
> - `?` : Lặp lại 0 hoặc 1 lần (tùy chọn).
> - `{n}` : Khớp đúng `n` lần.
> - `{n,}` : Khớp tối thiểu `n` lần.
> - `{n,m}` : Khớp từ `n` đến `m` lần.
> - `(?=...)` : Lookahead khẳng định (kiểm tra điều kiện khớp mà không tiêu thụ ký tự).

---

## Bảng tham chiếu các biểu thức chính quy phổ biến

| Mục đích | Regex Pattern (Standard / Java String) | Giải thích | Ví dụ khớp (Match) / Không khớp (Not Match) | Lưu ý |
|---|---|---|---|---|
| **Email** | `^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$`<br><br>Java: `^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$` | Kiểm tra định dạng email tiêu chuẩn. Cho phép chữ, số, chấm, gạch dưới trước `@`, và tên miền hợp lệ sau `@`. | **Khớp**: `user.name@domain.com`<br>**Không khớp**: `user@domain`, `@domain.com` | Tên miền cuối cùng phải dài từ 2 ký tự trở lên (ví dụ: `.com`, `.org`, `.vn`). |
| **Số điện thoại (Việt Nam)** | `^(0\|\+84)(3\|5\|7\|8\|9)\d{8}$`<br><br>Java: `^(0\|\\+84)(3\|5\|7\|8\|9)\\d{8}$` | Xác thực số điện thoại di động Việt Nam. Bắt đầu bằng `0` hoặc mã vùng quốc gia `+84`, tiếp theo là các đầu số di động phổ biến (`3`, `5`, `7`, `8`, `9`), sau cùng là 8 chữ số. | **Khớp**: `0912345678`, `+84398765432`<br>**Không khớp**: `0243123456` (số bàn), `091234567` (thiếu số) | Đầu số di động Việt Nam đã chuyển đổi sang 10 chữ số từ năm 2018. |
| **Số điện thoại (Quốc tế)** | `^\+\d{1,3}\d{6,14}$`<br><br>Java: `^\\+\\d{1,3}\\d{6,14}$` | Xác thực số điện thoại theo định dạng chuẩn quốc tế E.164. Bắt đầu bằng `+`, tiếp theo là mã quốc gia (1-3 số) và số điện thoại (6-14 số). | **Khớp**: `+14155552671`, `+84912345678`<br>**Không khớp**: `0912345678` (thiếu dấu `+`), `+1` (quá ngắn) | Không chứa khoảng trắng hoặc ký tự đặc biệt khác ngoài dấu `+` ở đầu. |
| **URL / Link** | `^(https?://)?(www\.)?[a-zA-Z0-9-]+(\.[a-zA-Z]{2,})+(/[a-zA-Z0-9-._~:/?#[\]@!$&'()*+,;=]*)?$`<br><br>Java: `^(https?://)?(www\\.)?[a-zA-Z0-9-]+(\\.[a-zA-Z]{2,})+(/[a-zA-Z0-9-._~:/?#[\\]@!$&'()*+,;=]*)?$` | Xác thực đường dẫn URL. Hỗ trợ cả giao thức `http`, `https`, tên miền con `www` và đường dẫn tài nguyên kèm theo. | **Khớp**: `https://google.com`, `www.example.com/index.html`<br>**Không khớp**: `http://`, `http://invalid_domain` | Có thể tùy biến thêm nếu cần bắt buộc có giao thức mạng (`https?://`). |
| **Ngày tháng (dd/MM/yyyy)** | `^(0[1-9]\|[12][0-9]\|3[01])/(0[1-9]\|1[0-2])/\d{4}$`<br><br>Java: `^(0[1-9]\|[12][0-9]\|3[01])/(0[1-9]\|1[0-2])/\\d{4}$` | Xác thực ngày tháng định dạng ngày trước, tháng sau. Ngày từ `01` - `31`, tháng từ `01` - `12`, năm gồm 4 chữ số. | **Khớp**: `25/12/2026`<br>**Không khớp**: `32/01/2026` (sai ngày), `12-12-2026` (sai ký tự phân tách) | Regex này không kiểm tra logic số ngày trong tháng (ví dụ: ngày 31/02 hoặc năm nhuận). Nên dùng `DateTimeFormatter` để parse logic này. |
| **Ngày tháng (yyyy-MM-dd)** | `^\d{4}-(0[1-9]\|1[0-2])-(0[1-9]\|[12][0-9]\|3[01])$`<br><br>Java: `^\\d{4}-(0[1-9]\|1[0-2])-(0[1-9]\|[12][0-9]\|3[01])$` | Định dạng ngày chuẩn ISO 8601. Năm trước, tháng giữa, ngày sau, cách nhau bởi dấu gạch ngang `-`. | **Khớp**: `2026-08-18`<br>**Không khớp**: `2026/08/18`, `2026-13-01` | Rất phổ biến khi lưu trữ ngày vào cơ sở dữ liệu (ví dụ MySQL DATE). |
| **Mật khẩu mạnh** | `^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$`<br><br>Java: `^(?=.*[a-z])(?=.*[A-Z])(?=.*\\d)(?=.*[@$!%*?&])[A-Za-z\\d@$!%*?&]{8,}$` | Yêu cầu độ dài tối thiểu 8 ký tự. Phải chứa ít nhất 1 chữ thường, 1 chữ hoa, 1 chữ số, và 1 ký tự đặc biệt trong tập hợp `[@$!%*?&]`. | **Khớp**: `P@ssw0rd123`, `Admin@2026`<br>**Không khớp**: `Password` (thiếu số và ký tự đặc biệt), `12345678` (thiếu chữ) | Sử dụng kỹ thuật tích cực Lookahead `(?=...)` để kiểm tra song song nhiều điều kiện. |
| **Số nguyên (Integer)** | `^-?\d+$`<br><br>Java: `^-?\\d+$` | Xác thực số nguyên tùy chọn có dấu âm `-` ở trước. | **Khớp**: `123`, `-456`, `0`<br>**Không khớp**: `12.3` (chứa dấu chấm thập phân), `abc` | Để bắt buộc chỉ nhận số nguyên dương, loại bỏ `-?`. |
| **Số thực (Decimal)** | `^-?\d+(\.\d+)?$`<br><br>Java: `^-?\\d+(\\.\\d+)?$` | Xác thực số thực (hoặc số nguyên). Cho phép có dấu âm và phần thập phân ngăn cách bởi dấu chấm `.`. | **Khớp**: `3.14`, `-0.005`, `100`<br>**Không khớp**: `3,14` (dùng dấu phẩy), `1.2.3` | Tùy biến dấu phân cách nếu hệ thống dùng dấu phẩy `,` cho số thập phân. |
| **Alphanumeric** | `^[a-zA-Z0-9]+$`<br><br>Java: `^[a-zA-Z0-9]+$` | Chỉ chấp nhận các ký tự chữ cái (không dấu) và chữ số. Không chứa khoảng trắng hoặc ký tự đặc biệt. | **Khớp**: `Username123`<br>**Không khớp**: `User Name`, `User@123` | Thường dùng để đặt tên đăng nhập (username) đơn giản. |
| **CMND / CCCD (Việt Nam)** | `^(\d{9}\|\d{12})$`<br><br>Java: `^(\\d{9}\|\\d{12})$` | Xác thực số CMND cũ (9 chữ số) hoặc thẻ Căn cước công dân mới (12 chữ số). | **Khớp**: `012345678`, `037123456789`<br>**Không khớp**: `12345`, `03712345678a` | Chỉ chấp nhận toàn bộ chữ số và đúng chiều dài quy định. |
| **Mã số thuế (MST - VN)** | `^\d{10}(-\d{3})?$`<br><br>Java: `^\\d{10}(-\\d{3})?$` | Xác thực Mã số thuế của Việt Nam. Bao gồm 10 chữ số cho doanh nghiệp chính, hoặc có thể thêm nhánh 3 số phụ sau dấu gạch ngang. | **Khớp**: `0102030405`, `0102030405-001`<br>**Không khớp**: `01020304`, `0102030405_001` | |
| **IP Address (IPv4)** | `^((25[0-5]\|2[0-4]\d\|[01]?\d\d?)\.){3}(25[0-5]\|2[0-4]\d\|[01]?\d\d?)$`<br><br>Java: `^((25[0-5]\|2[0-4]\\d\|[01]?\\d\\d?)\\.){3}(25[0-5]\|2[0-4]\\d\|[01]?\\d\\d?)$` | Xác thực địa chỉ IPv4 hợp lệ với mỗi nhóm số chạy từ `0` đến `255`. | **Khớp**: `192.168.1.1`, `127.0.0.1`<br>**Không khớp**: `256.1.1.1` (vượt 255), `192.168.1` (thiếu nhóm) | Chia nhỏ 250-255 thành `25[0-5]`, 200-249 thành `2[0-4]\d`, và 0-199 thành `[01]?\d\d?`. |
| **HTML Tag cơ bản** | `^<([a-z1-6]+)([^>]*)>.*</\1>$`<br><br>Java: `^<([a-z1-6]+)([^>]*)>.*</\\1>$` | Khớp thẻ đóng-mở HTML cơ bản có thể chứa các thuộc tính bên trong thẻ mở. | **Khớp**: `<a href="url">Click here</a>`, `<div>content</div>`<br>**Không khớp**: `<div>content</span>`, `<br/>` (thẻ tự đóng) | Nhóm `\1` bắt giữ thẻ mở để so sánh tương ứng với thẻ đóng ở cuối. |
