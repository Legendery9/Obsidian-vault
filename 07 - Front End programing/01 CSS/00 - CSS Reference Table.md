# 00 - CSS Reference Table

Tài liệu này cung cấp bảng tham chiếu tổng hợp các thuộc tính và bộ chọn (selectors) CSS phổ biến nhất theo nguyên lý 20/80, tập trung vào việc bố cục trang và xử lý giao diện thực tế.

---

## 1. Bộ chọn (Selectors)

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `*` (Universal Selector) | Bộ chọn toàn cục. | Chọn tất cả các phần tử có trên trang web. | Thường dùng để reset CSS mặc định. Ví dụ: `* { box-sizing: border-box; margin: 0; }`. | Tránh viết các thuộc tính nặng nề ảnh hưởng tới hiệu năng render của toàn bộ trang. |
| `.class` | Bộ chọn lớp (Class Selector). | Chọn tất cả các phần tử có thuộc tính `class` tương ứng. | Sử dụng ký tự chấm `.` trước tên lớp. Ví dụ: `.btn-primary { background: blue; }`. | Một phần tử có thể có nhiều class cách nhau bởi dấu cách. Khuyên dùng class để định dạng chính. |
| `#id` | Bộ chọn định danh (ID Selector). | Chọn phần tử duy nhất có thuộc tính `id` tương ứng. | Sử dụng ký tự thăng `#` trước tên id. Ví dụ: `#header { height: 60px; }`. | ID là duy nhất trên trang web, có độ ưu tiên cao hơn class. Tránh lạm dụng ID để viết CSS; hãy để dành ID cho JS. |
| `element` | Bộ chọn thẻ (Type Selector). | Chọn toàn bộ các phần tử có tên thẻ tương ứng. | Viết trực tiếp tên thẻ. Ví dụ: `p { line-height: 1.6; }`. | Áp dụng cho diện rộng. Nên dùng cho các phần tử cơ bản của trang (body, a, input). |
| `[attr="val"]` | Bộ chọn thuộc tính (Attribute Selector). | Chọn các phần tử có thuộc tính và giá trị tương ứng. | Đặt thuộc tính trong dấu ngoặc vuông. Ví dụ: `input[type="text"] { border-radius: 4px; }`. | Hữu ích khi định dạng các phần tử form khác nhau mà không muốn thêm class mới. |
| `:hover` | Giả lớp di chuột (Pseudo-class). | Áp dụng định dạng khi người dùng di con trỏ chuột lên phần tử. | Viết liền sau bộ chọn chính. Ví dụ: `a:hover { text-decoration: underline; }`. | Rất phổ biến cho nút bấm, liên kết để tăng tính tương tác (UX). |
| `:focus` | Giả lớp tiêu điểm (Pseudo-class). | Áp dụng định dạng khi phần tử nhận tiêu điểm (được click vào hoặc tab tới). | Thường dùng cho các ô input, button. Ví dụ: `input:focus { border-color: blue; }`. | Rất quan trọng cho khả năng tiếp cận (accessibility) bằng bàn phím. |
| `:nth-child(n)` | Giả lớp chọn phần tử thứ n. | Chọn phần tử con thứ `n` của một thẻ cha. | `n` có thể là số cụ thể, `odd` (lẻ), `even` (chẵn), hoặc công thức `an + b`. Ví dụ: `li:nth-child(even) { background: #eee; }`. | Đếm từ 1. Rất hữu ích khi làm bảng xen kẽ màu (zebra striping). |
| `::before` / `::after` | Giả phần tử chèn nội dung (Pseudo-element). | Tạo và chèn nội dung ảo vào trước hoặc sau nội dung thực tế của phần tử. | Phải luôn đi kèm thuộc tính `content`. Ví dụ: `span::before { content: "★ "; color: gold; }`. | Rất mạnh mẽ để vẽ các thành phần trang trí, icon mà không làm bẩn file HTML gốc. |

---

## 2. Mô hình hộp (Box Model)

> [!important]
> Mọi phần tử HTML được hiển thị dưới dạng một chiếc hộp chữ nhật bao gồm: **Content** (Nội dung), **Padding** (Đệm trong), **Border** (Đường viền), và **Margin** (Lề ngoài).

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `width` / `height` | Chiều rộng & chiều cao của phần tử. | Thiết lập kích thước phần hiển thị nội dung (Content) của hộp. | Nhận giá trị đơn vị (`px`, `%`, `rem`, `vh`, `vw`, `em`). Ví dụ: `width: 300px;`. | Với các phần tử inline (như `<span>`), thuộc tính này không có tác dụng cho đến khi chuyển sang inline-block hoặc block. |
| `padding` | Khoảng đệm trong (Padding). | Tạo khoảng trống giữa nội dung (content) và đường viền (border) của phần tử. | Viết gộp: `padding: top right bottom left;` hoặc viết lẻ: `padding-left: 10px;`. Ví dụ: `padding: 10px 20px;` (trên-dưới 10px, trái-phải 20px). | Padding nhận giá trị màu nền của chính phần tử đó. |
| `border` | Đường viền (Border). | Tạo một đường bao quanh vùng đệm trong và nội dung. | Viết gộp bao gồm kích thước, kiểu và màu. Ví dụ: `border: 1px solid #ccc;`. | Các kiểu phổ biến: `solid` (liền mạch), `dashed` (đứt nét), `dotted` (chấm). |
| `margin` | Khoảng lề ngoài (Margin). | Tạo khoảng cách trống bao quanh bên ngoài đường viền để đẩy các phần tử khác ra xa. | Tương tự padding, có thể viết gộp hoặc viết lẻ. Ví dụ căn giữa khối block: `margin: 0 auto;`. | Margin có hiện tượng "chập lề" (margin collapsing) theo chiều dọc giữa hai khối nằm liền kề. |
| `box-sizing: border-box` | Thuộc tính định cỡ hộp. | Thay đổi cách tính kích thước phần tử: Kích thước khai báo (`width`/`height`) sẽ bao gồm cả `padding` và `border`. | Áp dụng phổ biến cho toàn bộ trang thông qua bộ chọn `*`. Ví dụ: `* { box-sizing: border-box; }`. | Giúp việc lập trình giao diện dễ dàng hơn rất nhiều, tránh việc layout bị bể khi thêm padding. |

---

## 3. Bố cục (Layout)

### A. Định vị (Positioning)

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `position: relative` | Định vị tương đối. | Định vị phần tử theo vị trí bình thường của nó trên luồng trang mà không làm ảnh hưởng phần tử khác. | Dùng làm gốc tọa độ cho các phần tử con sử dụng `position: absolute`. Ví dụ: `position: relative; top: 10px;`. | Phần tử vẫn chiếm chỗ trên trang như bình thường. |
| `position: absolute` | Định vị tuyệt đối. | Đưa phần tử ra khỏi luồng trang bình thường và định vị nó dựa theo tổ tiên gần nhất có position khác `static`. | Kết hợp với các thuộc tính `top`, `bottom`, `left`, `right`. Ví dụ: `position: absolute; top: 0; right: 0;`. | Nếu không có tổ tiên nào được định vị, phần tử sẽ căn theo thẻ `<body>`. Phần tử absolute sẽ không chiếm khoảng trống trên trang. |
| `position: fixed` | Định vị cố định. | Định vị phần tử dựa trên khung hình trình duyệt (viewport). | Phần tử không di chuyển khi cuộn trang. Ví dụ: Cố định menu header: `position: fixed; top: 0; width: 100%; z-index: 1000;`. | Tương tự absolute, phần tử bị rút khỏi luồng trang và không chiếm không gian. |
| `position: sticky` | Định vị dính. | Là sự kết hợp giữa `relative` và `fixed`: Phần tử hoạt động như relative cho đến khi cuộn tới vị trí ngưỡng chỉ định, sau đó dính lại như fixed. | Yêu cầu phải xác định ít nhất một thuộc tính định hướng (ví dụ: `top: 0;`). Ví dụ: `position: sticky; top: 0;`. | Hoạt động phụ thuộc vào kích thước của thẻ cha chứa nó. Sẽ ngừng dính khi thẻ cha của nó bị cuộn hết. |
| `z-index` | Thứ tự hiển thị lớp chồng (Stack Order). | Xác định phần tử nào nằm trên, phần tử nào nằm dưới khi các phần tử chồng lấn nhau. | Chỉ có tác dụng với các phần tử có `position` khác `static`. Nhận giá trị số nguyên. Ví dụ: `z-index: 99;`. | Số lớn hơn sẽ hiển thị đè lên trên số nhỏ hơn. |

### B. Flexbox (Bố cục 1 chiều)

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `display: flex` | Kích hoạt bộ cục Flexbox. | Biến phần tử thành một flex container, các con trực tiếp của nó trở thành flex items. | Khai báo trên thẻ cha. Ví dụ: `.parent { display: flex; }`. | Sắp xếp các con mặc định theo chiều ngang (row). |
| `flex-direction` | Hướng của trục chính. | Xác định hướng xếp của các phần tử con. | Các giá trị: `row` (ngang), `column` (dọc), `row-reverse`, `column-reverse`. | Thay đổi hướng xếp cũng sẽ hoán đổi tác dụng của trục chính (main axis) và trục phụ (cross axis). |
| `justify-content` | Căn chỉnh trên trục chính. | Phân bổ khoảng trống và căn lề cho các phần tử con dọc theo trục chính (mặc định là chiều ngang). | Các giá trị phổ biến: `flex-start`, `flex-end`, `center`, `space-between`, `space-around`, `space-evenly`. | Ví dụ: `.parent { justify-content: space-between; }`. |
| `align-items` | Căn chỉnh trên trục phụ. | Căn lề cho các phần tử con dọc theo trục phụ (mặc định là chiều dọc). | Các giá trị: `stretch` (kéo giãn), `flex-start`, `flex-end`, `center`, `baseline`. | Rất phổ biến để căn giữa theo chiều dọc: `align-items: center;`. |
| `flex-wrap` | Tự động xuống dòng. | Cho phép các phần tử con tự động xuống dòng mới khi chiều ngang của cha không đủ chứa. | Các giá trị: `nowrap` (mặc định), `wrap`, `wrap-reverse`. | Khi chia lưới, cần dùng `flex-wrap: wrap;` để tránh các cột bị bóp méo chiều rộng. |
| `gap` | Khoảng cách giữa các item. | Thiết lập khoảng cách trực tiếp giữa các hàng và cột con mà không cần dùng margin trên từng item. | Nhận giá trị đơn vị đo. Ví dụ: `gap: 15px;` hoặc `gap: 20px 10px;` (dọc ngang). | Rất tiện lợi và sạch sẽ hơn việc dùng margin cho flex item. |

### C. Grid (Bố cục 2 chiều)

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `display: grid` | Kích hoạt bố cục Grid. | Biến phần tử thành một grid container, bố cục dựa trên hệ lưới hai chiều (dòng và cột). | Khai báo trên thẻ cha. Ví dụ: `.grid-container { display: grid; }`. | Hoàn hảo cho các bố cục trang phức tạp cần chia cả hàng và cột. |
| `grid-template-columns` | Định nghĩa số cột lưới. | Xác định số lượng và độ rộng của các cột trong lưới. | Dùng các đơn vị đo hoặc đơn vị tỉ lệ `fr` (fraction). Ví dụ lưới 3 cột đều nhau: `grid-template-columns: repeat(3, 1fr);`. | Đơn vị `fr` tự động phân chia phần không gian còn trống đều nhau. |
| `grid-template-rows` | Định nghĩa số dòng lưới. | Xác định số lượng và chiều cao của các dòng trong lưới. | Ví dụ: `grid-template-rows: 100px auto 100px;`. | Dùng `auto` để dòng tự co giãn theo chiều cao nội dung. |

---

## 4. Hiệu ứng & Chuyển động (Transitions & Animations)

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `transition` | Chuyển đổi trạng thái mượt mà. | Làm mượt quá trình thay đổi giá trị thuộc tính CSS khi có sự kiện (như hover). | Viết gộp gồm: thuộc tính, thời gian, kiểu chuyển động, độ trễ. Ví dụ: `transition: all 0.3s ease-in-out;`. | Không chuyển tiếp mượt mà được cho các thuộc tính như `display: none` sang `block` (nên dùng `opacity` và `visibility`). |
| `transform` | Biến đổi hình học. | Cho phép dịch chuyển (translate), xoay (rotate), phóng to/thu nhỏ (scale) hoặc nghiêng (skew) phần tử. | Ví dụ: Di chuyển sang phải 10px và xoay 45 độ: `transform: translate(10px, 0) rotate(45deg);`. | Kết hợp cực tốt với `transition` để tạo hiệu ứng hover mượt mà mà không ảnh hưởng luồng trang. |
| `@keyframes` | Định nghĩa chuỗi chuyển động. | Tạo ra các cột mốc trạng thái (frames) cho một chu kỳ chuyển động. | Dùng tỷ lệ phần trăm (`0%` đến `100%`) hoặc `from` và `to`. Xem ví dụ bên dưới bài viết. | Đặt độc lập ngoài các selector. |
| `animation` | Kích hoạt hiệu ứng chuyển động. | Gán chuỗi `@keyframes` đã định nghĩa vào một phần tử và thiết lập cách chạy. | Viết gộp gồm: tên keyframes, thời gian, kiểu chạy, số lần lặp. Ví dụ: `animation: spin 2s linear infinite;`. | Sử dụng thuộc tính `animation-fill-mode: forwards` nếu muốn phần tử giữ nguyên trạng thái kết thúc khi kết thúc animation. |

---

## Ví dụ thực tế: Cấu trúc Flexbox & Grid

Dưới đây là mã nguồn minh họa cách dùng Flexbox để xây dựng menu điều hướng và Grid để chia lưới sản phẩm.

```css
/* --- Flexbox: Căn giữa và phân chia Menu --- */
.navbar {
    display: flex;
    justify-content: space-between; /* Đẩy Logo sang trái, Menu sang phải */
    align-items: center;            /* Căn giữa các mục theo chiều dọc */
    background-color: #1a1a1a;
    padding: 15px 30px;
}

.menu-list {
    display: flex;
    gap: 20px;                      /* Tạo khoảng cách giữa các mục menu */
    list-style: none;
}

.menu-list a {
    color: #ffffff;
    text-decoration: none;
    transition: color 0.2s ease;
}

.menu-list a:hover {
    color: #ff9900;
}

/* --- Grid: Lưới Sản Phẩm Đáp Ứng (Responsive Grid) --- */
.product-grid {
    display: grid;
    /* Tự động tính toán số cột dựa trên chiều rộng màn hình, mỗi cột tối thiểu 250px */
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    padding: 40px;
}

.product-card {
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 15px;
    text-align: center;
}
```

---

## Ví dụ thực tế: Tạo hiệu ứng với Pseudo-element & Transition

Ví dụ tạo một nút bấm có hiệu ứng vạch kẻ sáng chạy qua khi hover chuột.

```css
.btn-effect {
    position: relative;
    padding: 12px 24px;
    background-color: #007bff;
    color: white;
    border: none;
    font-size: 16px;
    cursor: pointer;
    overflow: hidden; /* Ẩn phần pseudo-element tràn ra ngoài */
    z-index: 1;
}

/* Tạo lớp phủ sáng ẩn ở bên trái nút */
.btn-effect::after {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: rgba(255, 255, 255, 0.2);
    transform: skewX(-30deg); /* Nghiêng lớp phủ sáng */
    transition: left 0.5s ease;
    z-index: -1; /* Đứng sau chữ để không che mất nội dung */
}

/* Khi hover, đẩy lớp phủ chạy ngang qua nút */
.btn-effect:hover::after {
    left: 100%;
}
```
