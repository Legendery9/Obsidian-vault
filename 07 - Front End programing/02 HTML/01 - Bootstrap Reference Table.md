# 01 - Bootstrap Reference Table

Tài liệu này cung cấp bảng tham chiếu tổng hợp các class, utility, component và data-attribute phổ biến nhất của **Bootstrap** (phiên bản v5) phục vụ việc thiết kế giao diện nhanh chóng và nhất quán.

---

## 1. Grid System (Hệ thống lưới)

| Class / Attribute / Component | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `container` | Lớp bao bọc có chiều rộng cố định (responsive pixel widths). | Căn giữa nội dung, tạo lề hai bên tự động thay đổi theo kích thước màn hình. | Bao bọc toàn bộ bố cục hoặc một phần lớn của trang. Ví dụ: `<div class="container">...</div>`. | Có thiết lập `padding-left` và `padding-right` mặc định (gutter). Không lồng `container` trong một `container` khác. |
| `container-fluid` | Lớp bao bọc có chiều rộng đầy đủ (100% viewport width). | Tạo khung hiển thị tràn viền (Full width) ở mọi kích thước màn hình. | Dùng khi thiết kế dashboard, bảng điều khiển hoặc thanh điều hướng tràn màn hình. | Vẫn giữ padding biên tương tự `container` thông thường. |
| `row` | Lớp hàng, bao bọc trực tiếp các cột (`col-*`). | Tạo một dòng chứa lưới và thiết lập flexbox để chứa các cột con. | Đặt trực tiếp bên trong `container`. Các phần tử con trực tiếp của `row` bắt buộc phải là các lớp cột (`col-*`). | Có thuộc tính `margin-left` và `margin-right` âm để triệt tiêu padding của `container`. |
| `col-*` | Lớp cột (Column) trong hệ thống lưới 12 cột. | Xác định độ rộng của cột trên các kích thước màn hình khác nhau (ví dụ: `col-md-6`, `col-lg-4`). | Đặt bên trong `row`. Định dạng: `col-{breakpoint}-{size}` (VD: `col-sm-12 col-md-6`). | Nếu tổng số cột (`size`) trong một `row` vượt quá 12, cột thừa sẽ tự động xuống dòng mới. |

---

## 2. Spacing Utilities (Tiện ích căn lề & Khoảng cách)

Định dạng chung: `{property}{sides}-{size}` (ví dụ: `mt-3`, `px-2`).
- `m`: `margin` | `p`: `padding`
- `t`: `top` | `b`: `bottom` | `s`: `start` (trái) | `e`: `end` (phải) | `x`: `left + right` | `y`: `top + bottom` | bỏ trống: `all 4 sides`
- `size`: `0` (xóa lề), `1` (0.25rem), `2` (0.5rem), `3` (1rem), `4` (1.5rem), `5` (3rem), `auto` (chỉ dùng cho margin để căn giữa).

| Class / Attribute / Component | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `m-*` / `p-*` | Căn lề ngoài (margin) hoặc lề trong (padding) cho cả 4 phía. | Tạo khoảng cách bao quanh phần tử một cách nhanh chóng. | Áp dụng trực tiếp vào thẻ HTML. Ví dụ: `class="m-3"`, `class="p-2"`. | Thích hợp cho các block cô lập cần giãn cách đồng đều. |
| `mt-*` / `mb-*` | Tiện ích khoảng cách phía trên (top) hoặc phía dưới (bottom). | Tạo khoảng giãn cách theo chiều dọc giữa các phần tử xếp chồng. | Ví dụ: `<h2 class="mb-3">Tiêu đề</h2>` để tạo khoảng trống phía dưới tiêu đề. | Tránh dùng quá nhiều làm mất tính nhất quán khoảng cách dọc. |
| `ms-*` / `me-*` | Tiện ích khoảng cách phía trái (start) hoặc phía phải (end). | Tạo khoảng giãn cách theo chiều ngang giữa các phần tử thẳng hàng. | Thích hợp cho các inline/inline-block elements như button, icon. Ví dụ: `class="me-2"`. | Tên gọi `start` và `end` hỗ trợ thiết kế đa ngôn ngữ từ phải sang trái (RTL). |
| `mx-*` / `my-*` | Tiện ích khoảng cách theo trục ngang X (trái+phải) hoặc trục dọc Y (trên+dưới). | Viết tắt giúp thu gọn code khi cần chỉnh khoảng cách hai bên đối xứng. | Ví dụ: `<div class="mx-auto" style="width: 200px;">` để căn giữa khối. | `mx-auto` yêu cầu phần tử phải có chiều rộng cố định (`width`) và là block element. |

---

## 3. UI Components (Thành phần giao diện phổ biến)

| Class / Attribute / Component | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `btn` / `btn-*` | Class nút bấm (Button). | Thiết lập style cơ bản cho nút (hover, active, border) và màu sắc chủ đề (VD: `btn-primary`, `btn-outline-danger`). | Sử dụng cho thẻ `<button>` hoặc thẻ `<a>`. Ví dụ: `class="btn btn-primary"`. | Không nên lạm dụng thẻ `<a>` làm nút trừ khi đó là liên kết chuyển trang thực tế. |
| `card` | Khung nội dung dạng thẻ (Card component). | Gom nhóm thông tin liên quan vào một chiếc hộp có bo góc, đổ bóng và viền mờ. | Cấu trúc chuẩn bao gồm: `card`, `card-header`, `card-body`, `card-footer`. | Rất thích hợp để dựng layout dạng bảng tin, danh sách sản phẩm hoặc biểu đồ điều khiển. |
| `modal` | Hộp thoại tương tác (Modal Dialog). | Hiển thị nội dung ghi đè lên trang hiện tại (overlay), yêu cầu tương tác trực tiếp. | Cấu trúc: `modal` -> `modal-dialog` -> `modal-content` -> `modal-header` / `modal-body` / `modal-footer`. | Mặc định bị ẩn bằng class `fade`. Cần javascript hoặc data attributes để kích hoạt hiển thị. |
| `navbar` | Thanh điều hướng (Navigation Bar). | Tạo thanh menu chính ở đầu trang web, hỗ trợ responsive thu gọn trên mobile. | Sử dụng kết hợp: `navbar`, `navbar-expand-lg`, `navbar-dark`, `bg-dark`... | Thường chứa logo, liên kết trang và form tìm kiếm nhanh. |
| `alert` / `alert-*` | Hộp thông báo trạng thái (Alert component). | Hiển thị các phản hồi trạng thái nổi bật cho người dùng (VD: `alert-success`, `alert-danger`). | Ví dụ: `<div class="alert alert-success" role="alert">Thành công!</div>`. | Nên có vai trò `role="alert"` để hỗ trợ trình đọc màn hình (accessibility). |

---

## 4. Data Attributes (Thuộc tính kích hoạt bằng dữ liệu)

Các thuộc tính HTML5 đặc trưng giúp tương tác với các component Bootstrap bằng JS mà không cần viết code JS thủ công.

| Class / Attribute / Component | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `data-bs-toggle` | Thuộc tính chỉ định cơ chế kích hoạt (toggle) của component. | Bật/tắt trạng thái ẩn/hiện hoặc hành vi của một component (như `modal`, `collapse`, `dropdown`). | Khai báo trên thẻ kích hoạt (ví dụ: button kích hoạt modal: `data-bs-toggle="modal"`). | Giá trị truyền vào phải viết thường chính xác tên loại component. |
| `data-bs-target` | Thuộc tính chỉ định ID đối tượng chịu tác động. | Trỏ tới selector CSS (thường là ID) của khối HTML cần thay đổi trạng thái ẩn/hiện. | Dùng kèm với `data-bs-toggle`. Ví dụ: `data-bs-target="#myModal"`. | Bắt buộc phải có dấu thăng `#` nếu trỏ tới một `id`. |
| `data-bs-dismiss` | Thuộc tính dùng để đóng component. | Đóng trực tiếp một modal hoặc xóa bỏ một alert ra khỏi giao diện khi người dùng click vào. | Đặt trên nút Đóng bên trong modal hoặc alert. Ví dụ: `data-bs-dismiss="modal"`. | Tự động giải phóng các overlay nền (backdrop) liên quan khi đóng modal. |

---

## 5. Các ví dụ HTML minh họa thực tế

### 5.1. Ví dụ hệ thống Lưới (Grid System) và Spacing
```html
<!-- Bố cục 3 cột đều nhau trên Desktop, xếp chồng trên Mobile -->
<div class="container my-5">
    <div class="row g-3"> <!-- g-3: tạo khoảng cách gutter giữa các cột -->
        <div class="col-12 col-md-4">
            <div class="p-3 border bg-light text-center">Cột 1</div>
        </div>
        <div class="col-12 col-md-4">
            <div class="p-3 border bg-light text-center">Cột 2</div>
        </div>
        <div class="col-12 col-md-4">
            <div class="p-3 border bg-light text-center">Cột 3</div>
        </div>
    </div>
</div>
```

---

### 5.2. Ví dụ Card Component
```html
<div class="card" style="width: 18rem;">
    <div class="card-header bg-primary text-white">
        Phân loại thiết bị
    </div>
    <div class="card-body">
        <h5 class="card-title">Thiết bị IoT</h5>
        <p class="card-text">Hệ thống cảm biến đo nhiệt độ và độ ẩm phòng máy chủ.</p>
        <a href="#" class="btn btn-outline-primary btn-sm">Xem chi tiết</a>
    </div>
    <div class="card-footer text-muted text-center">
        Cập nhật: 5 phút trước
    </div>
</div>
```

---

### 5.3. Ví dụ Alert Component có nút đóng
```html
<div class="alert alert-warning alert-dismissible fade show m-3" role="alert">
    <strong>Cảnh báo!</strong> Thiết bị Server 01 đang vượt quá nhiệt độ an toàn.
    <!-- data-bs-dismiss="alert" kích hoạt tính năng tự tắt của Alert -->
    <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
</div>
```

---

### 5.4. Ví dụ Modal Dialog kích hoạt bằng Button
```html
<!-- 1. Nút bấm kích hoạt Modal -->
<button type="button" class="btn btn-danger" data-bs-toggle="modal" data-bs-target="#deleteConfirmModal">
    Xóa thiết bị
</button>

<!-- 2. Cấu trúc Modal ẩn -->
<div class="modal fade" id="deleteConfirmModal" tabindex="-1" aria-labelledby="modalTitle" aria-hidden="true">
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="modalTitle">Xác nhận xóa tài nguyên</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                Hành động này không thể hoàn tác. Bạn có chắc chắn muốn xóa thiết bị này không?
            </div>
            <div class="modal-footer">
                <!-- data-bs-dismiss="modal" dùng để đóng Modal -->
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Hủy bỏ</button>
                <button type="button" class="btn class-danger">Đồng ý xóa</button>
            </div>
        </div>
    </div>
</div>
```

---

### 5.5. Ví dụ Navbar hoàn chỉnh
```html
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container-fluid">
        <a class="navbar-brand" href="#">DeviceManager</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#mainMenu" aria-controls="mainMenu" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="mainMenu">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                <li class="nav-item">
                    <a class="nav-link active" aria-current="page" href="#">Trang chủ</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Thiết bị</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Báo cáo</a>
                </li>
            </ul>
            <form class="d-flex">
                <input class="form-control me-2" type="search" placeholder="Từ khóa..." aria-label="Search">
                <button class="btn btn-outline-success" type="submit">Tìm</button>
            </form>
        </div>
    </div>
</nav>
```
