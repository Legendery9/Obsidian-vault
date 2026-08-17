# 00 - HTML Reference Table

Tài liệu này cung cấp bảng tham chiếu tổng hợp các thẻ (tags) HTML cốt lõi theo nguyên lý 20/80, phục vụ việc tra cứu nhanh và chính xác cách sử dụng trong lập trình Front End.

---

## 1. Cấu trúc tài liệu & Meta Tags

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `<!DOCTYPE html>` | Khai báo kiểu tài liệu (Document Type Declaration). | Khai báo cho trình duyệt biết đây là tài liệu HTML5 để dựng trang chính xác. | Đặt ở dòng đầu tiên của file `.html`, trước thẻ `<html>`. Không phân biệt chữ hoa/thường nhưng khuyến nghị viết hoa. | Không phải là thẻ HTML mà là một chỉ thị cấu hình. |
| `<html>` | Phần tử gốc (Root Element). | Chứa toàn bộ nội dung của trang web (ngoại trừ `<!DOCTYPE html>`). | Bao bọc toàn bộ trang. Có thuộc tính `lang` để xác định ngôn ngữ (VD: `<html lang="vi">`). | Mọi trang HTML bắt buộc phải có duy nhất một thẻ `<html>`. |
| `<head>` | Phần đầu tài liệu (Metadata Container). | Chứa các thông tin mô tả, cấu hình trang web (charset, viewport, title, links to CSS/JS). | Đặt ngay sau thẻ mở `<html>` và trước `<body>`. | Nội dung trong `<head>` không hiển thị trực tiếp trên giao diện trang web. |
| `<body>` | Phần thân tài liệu (Document Body). | Chứa tất cả nội dung hiển thị trực tiếp với người dùng (text, images, links, tables, forms, etc.). | Đặt sau thẻ đóng `</head>`, là con trực tiếp của `<html>`. | Chỉ có duy nhất một thẻ `<body>` trên mỗi trang HTML. |
| `<meta>` | Thẻ siêu dữ liệu (Metadata Element). | Cung cấp thông tin mô tả trang (mã hóa ký tự, cấu hình khung nhìn viewport, SEO keywords/description). | Đặt bên trong thẻ `<head>`. Ví dụ: `<meta charset="UTF-8">`, `<meta name="viewport" content="width=device-width, initial-scale=1.0">`. | Là thẻ tự đóng (self-closing tag), không có thẻ đóng `</meta>`. |
| `<title>` | Tiêu đề trang (Page Title). | Thiết lập tiêu đề hiển thị trên tab của trình duyệt hoặc kết quả tìm kiếm SEO. | Đặt bên trong thẻ `<head>`. Ví dụ: `<title>Trang chủ</title>`. | Bắt buộc phải có trong mỗi tài liệu để tối ưu SEO và trải nghiệm người dùng. |
| `<link>` | Liên kết tài nguyên ngoài (External Resource Link). | Kết nối trang HTML với các tệp bên ngoài, phổ biến nhất là CSS và Favicon. | Đặt bên trong thẻ `<head>`. Ví dụ liên kết CSS: `<link rel="stylesheet" href="style.css">`. | Là thẻ tự đóng. Thuộc tính `rel` và `href` là bắt buộc. |
| `<script>` | Nhúng/Liên kết mã script (Script Element). | Nhúng mã JavaScript trực tiếp hoặc liên kết tới tệp JavaScript bên ngoài. | Có thể đặt trong `<head>` hoặc trước thẻ đóng `</body>`. Khuyến nghị đặt ở cuối `<body>` hoặc dùng thuộc tính `defer` để tránh block render giao diện. | Ví dụ liên kết file ngoài: `<script src="app.js" defer></script>`. |

---

## 2. Phần tử văn bản & Bố cục

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `<h1>` đến `<h6>` | Tiêu đề nội dung (Headings). | Định nghĩa các mức độ quan trọng của tiêu đề bài viết từ lớn nhất (`<h1>`) đến nhỏ nhất (`<h6>`). | Dùng để phân tách các mục nội dung. Ví dụ: `<h1>Tiêu đề chính</h1>`. | Tốt cho SEO. Chỉ nên có tối đa **một** thẻ `<h1>` duy nhất trên một trang. Không dùng các thẻ heading chỉ để làm chữ to hơn. |
| `<p>` | Đoạn văn bản (Paragraph). | Định nghĩa một đoạn văn bản. Tự động thêm khoảng trống (margin) trên và dưới đoạn văn. | Bao bọc các khối văn bản thuần túy. Ví dụ: `<p>Đây là một đoạn văn.</p>`. | Không nên lồng các phần tử dạng khối (block-level) như `<div>` bên trong `<p>`. |
| `<span>` | Vùng chọn nội dòng (Inline Container). | Định nhóm một đoạn văn bản nhỏ hoặc phần tử nội dòng để định dạng CSS hoặc xử lý JS. | Sử dụng trực tiếp trong dòng văn bản. Ví dụ: `<span style="color:red;">chữ đỏ</span>`. | Là phần tử nội dòng (inline), không tự động xuống dòng và không có margin/padding block theo mặc định. |
| `<div>` | Khối phân vùng (Division Container). | Định nghĩa một khu vực hoặc một khối chứa cấu trúc để dàn trang (layout) và CSS. | Bao bọc các phần tử khác. Ví dụ: `<div class="container">...</div>`. | Là phần tử khối (block-level), mặc định chiếm 100% chiều rộng của cha nó. Nên hạn chế lạm dụng (lỗi "div soup"), hãy ưu tiên các thẻ Semantic. |
| `<br>` | Xuống dòng (Line Break). | Tạo một điểm ngắt dòng thủ công trong đoạn văn. | Đặt trực tiếp tại nơi muốn xuống dòng. Ví dụ: `Dòng 1<br>Dòng 2`. | Là thẻ tự đóng. Không sử dụng `<br>` để tạo khoảng cách giữa các đoạn văn (hãy dùng CSS margin). |
| `<hr>` | Đường kẻ ngang (Horizontal Rule). | Tạo một đường kẻ ngang để phân chia chủ đề hoặc các phần nội dung khác nhau. | Đặt giữa các phần nội dung cần phân chia. | Thẻ tự đóng. Có thể định dạng lại kiểu dáng bằng CSS. |

---

## 3. Liên kết & Đa phương tiện

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `<a>` | Siêu liên kết (Anchor). | Tạo liên kết dẫn đến một trang web khác, một file, hoặc một vị trí trong trang. | Thuộc tính `href` chứa URL đích. `target="_blank"` để mở trong tab mới. Ví dụ: `<a href="https://google.com" target="_blank">Google</a>`. | Khi dùng `target="_blank"`, nên thêm `rel="noopener noreferrer"` để bảo mật. |
| `<img>` | Hình ảnh (Image). | Nhúng hình ảnh vào trang web. | Cần thuộc tính `src` (đường dẫn ảnh) và `alt` (văn bản thay thế nếu ảnh lỗi). Ví dụ: `<img src="logo.png" alt="Logo Công Ty">`. | Thẻ tự đóng. Luôn cung cấp thuộc tính `alt` để hỗ trợ thiết bị đọc màn hình (Accessibility) và SEO. |
| `<iframe>` | Khung nội dung nhúng (Inline Frame). | Nhúng một tài liệu HTML khác (ví dụ: Google Maps, video YouTube) trực tiếp vào trang hiện tại. | Thuộc tính `src` chứa liên kết nhúng. Ví dụ: `<iframe src="https://maps.google.com..."></iframe>`. | Cần kiểm soát thuộc tính bảo mật `sandbox` và kích thước hiển thị để tránh lỗi bảo mật (XSS) và bể layout. |

---

## 4. Danh sách & Bảng

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `<ul>` | Danh sách không thứ tự (Unordered List). | Định nghĩa một danh sách dạng các dấu đầu dòng (bullet points). | Bao bọc các phần tử danh sách `<li>`. | Thuộc tính CSS `list-style-type` dùng để thay đổi icon đầu dòng. |
| `<ol>` | Danh sách có thứ tự (Ordered List). | Định nghĩa một danh sách được đánh số thứ tự (1, 2, 3...) hoặc ký tự (A, B, C...). | Bao bọc các phần tử danh sách `<li>`. | Có các thuộc tính bổ sung như `type` (kiểu số/chữ) và `start` (số bắt đầu). |
| `<li>` | Phần tử danh sách (List Item). | Định nghĩa một mục con trong danh sách. | Phải nằm trực tiếp bên trong `<ul>` hoặc `<ol>`. Ví dụ: `<li>Mục 1</li>`. | Không được đặt trực tiếp bên ngoài `<ul>`/`<ol>`. |
| `<table>` | Bảng dữ liệu (Table). | Định nghĩa một bảng chứa dữ liệu dạng lưới dòng và cột. | Bao bọc toàn bộ cấu trúc bảng bao gồm `<thead>`, `<tbody>`, `<tr>`, v.v. | Dàn trang bằng `table` đã lỗi thời; chỉ dùng `table` để hiển thị dữ liệu dạng bảng biểu. |
| `<tr>` | Dòng của bảng (Table Row). | Định nghĩa một hàng trong bảng. | Nằm trong `<table>`, `<thead>` hoặc `<tbody>`. Chứa các thẻ `<th>` hoặc `<td>`. | Số lượng dòng tương đương với số lượng thẻ `<tr>`. |
| `<td>` | Ô dữ liệu (Table Data). | Định nghĩa một ô chứa dữ liệu thông thường trong hàng. | Nằm bên trong `<tr>`. Ví dụ: `<td>Nguyễn Văn A</td>`. | Có thuộc tính `colspan` (gộp cột) và `rowspan` (gộp dòng) để tùy biến giao diện bảng. |
| `<th>` | Ô tiêu đề (Table Header). | Định nghĩa ô tiêu đề cho cột hoặc hàng. Mặc định chữ sẽ in đậm và căn giữa. | Nằm trong hàng tiêu đề `<tr>` (thường thuộc `<thead>`). | Giúp tăng tính tiếp cận (accessibility) cho người dùng sử dụng trình đọc màn hình. |

---

## 5. Biểu mẫu & Nhập liệu

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `<form>` | Biểu mẫu nhập liệu (Form). | Thu thập thông tin nhập vào từ người dùng để gửi lên máy chủ (server). | Bao bọc các input, button. Có thuộc tính `action` (URL xử lý dữ liệu) và `method` (`GET` hoặc `POST`). | Ví dụ: `<form action="/submit" method="post">...</form>`. |
| `<input>` | Ô nhập liệu (Input Control). | Cho phép người dùng nhập dữ liệu với nhiều định dạng khác nhau tùy thuộc vào thuộc tính `type`. | Đặt trong form hoặc độc lập kèm JS. Các type phổ biến: `text`, `password`, `email`, `number`, `checkbox`, `radio`, `submit`, `file`. | Thẻ tự đóng. Luôn sử dụng thuộc tính `name` để server định danh dữ liệu gửi lên. |
| `<button>` | Nút bấm (Button). | Tạo nút bấm có thể nhấp được để thực thi hành động (submit form, reset form hoặc chạy JS). | Thuộc tính `type` gồm `submit` (mặc định trong form), `button` (chạy JS), `reset`. Ví dụ: `<button type="submit">Gửi</button>`. | Khuyên dùng `<button>` thay vì `<input type="button">` vì hỗ trợ chèn HTML/Icon bên trong linh hoạt hơn. |
| `<select>` | Trình đơn thả xuống (Drop-down List). | Tạo một danh sách lựa chọn thả xuống để người dùng chọn một hoặc nhiều giá trị. | Bao bọc các thẻ `<option>`. Ví dụ: `<select name="city">...</select>`. | Dùng thuộc tính `multiple` để cho phép chọn nhiều mục cùng lúc. |
| `<option>` | Lựa chọn (Option). | Định nghĩa một mục chọn cụ thể trong thẻ `<select>`. | Nằm bên trong `<select>`. Thuộc tính `value` xác định giá trị gửi lên server. Ví dụ: `<option value="hn">Hà Nội</option>`. | Thuộc tính `selected` dùng để đặt mục chọn mặc định ban đầu. |
| `<textarea>` | Vùng nhập văn bản lớn (Text Area). | Cho phép nhập văn bản nhiều dòng (như ý kiến đóng góp, địa chỉ). | Ví dụ: `<textarea name="comment" rows="4" cols="50"></textarea>`. | Kích thước có thể thay đổi bằng thuộc tính `rows`/`cols` hoặc thông qua CSS `resize`. |
| `<label>` | Nhãn phần tử nhập liệu (Label). | Định nghĩa nhãn mô tả cho một thẻ nhập liệu (đặc biệt là checkbox/radio). | Liên kết với `<input>` thông qua thuộc tính `for` khớp với `id` của input. Ví dụ: `<label for="username">Tên</label><input id="username">`. | Nhấp vào nhãn sẽ tự động kích hoạt/focus vào ô nhập liệu tương ứng, cải thiện UX đáng kể. |

---

## 6. Phần tử ngữ nghĩa (Semantic HTML)

> [!important]
> Sử dụng các thẻ Semantic giúp cải thiện cấu trúc mã nguồn, hỗ trợ công cụ tìm kiếm (SEO) thu thập thông tin và giúp các trình đọc màn hình hoạt động hiệu quả hơn. Hãy hạn chế lạm dụng thẻ `<div>` vô nghĩa.

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `<header>` | Đầu trang/Khu vực giới thiệu. | Chứa logo, thanh điều hướng, tiêu đề chính của trang hoặc của một phần nội dung. | Thường đặt ở phần trên cùng của trang web hoặc đầu các bài viết `<article>`. | Không nhầm lẫn thẻ `<header>` với thẻ `<head>`. |
| `<nav>` | Thanh điều hướng (Navigation). | Định nghĩa một tập hợp các liên kết điều hướng chính của trang web. | Bao bọc danh sách menu liên kết. Ví dụ: `<nav><a href="/">Trang chủ</a> | <a href="/about">Giới thiệu</a></nav>`. | Chỉ dùng cho các liên kết điều hướng chính, không dùng cho toàn bộ liên kết trên trang. |
| `<section>` | Phân đoạn nội dung (Section). | Nhóm các nội dung liên quan có chung một chủ đề lớn lại với nhau. | Dùng phân chia bố cục trang. Nên chứa một heading (`<h2>`-`<h6>`) bên trong để xác định chủ đề. | Tránh dùng `<section>` thay thế hoàn toàn cho `<div>` nếu khối đó chỉ dùng để định dạng CSS/giao diện. |
| `<article>` | Bài viết độc lập (Article). | Chứa nội dung tự cung cấp thông tin độc lập, có thể tái sử dụng hoặc phân phối độc lập (bài báo, blog post, bình luận). | Bao bọc nội dung bài đăng. Ví dụ: `<article><h2>Tên bài viết</h2><p>Nội dung...</p></article>`. | Một trang có thể chứa nhiều thẻ `<article>` khác nhau. |
| `<aside>` | Nội dung phụ (Aside). | Chứa nội dung nằm ngoài luồng chính nhưng có liên quan gián tiếp (ví dụ: thanh bên sidebar, quảng cáo, danh sách bài viết liên quan). | Đặt bên cạnh nội dung chính của trang. | Thường được định dạng hiển thị ở cột bên trái hoặc bên phải bằng CSS Flexbox/Grid. |
| `<footer>` | Chân trang (Footer). | Chứa thông tin bản quyền, thông tin liên hệ, liên kết mạng xã hội, hoặc liên kết phụ. | Đặt ở cuối trang web hoặc ở cuối một phân đoạn nội dung lớn. | Tương tự `<header>`, có thể có nhiều `<footer>` trên một trang nếu nằm trong các `<section>` hoặc `<article>` khác nhau. |

---

## Ví dụ thực tế: Trang HTML hoàn chỉnh

Dưới đây là một ví dụ thực tế về cách kết hợp các thẻ cấu trúc, semantic và form nhập liệu để tạo nên một trang web chuẩn chỉnh.

```html
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trang Đăng Ký Thành Viên</title>
    <link rel="stylesheet" href="style.css">
    <script src="app.js" defer></script>
</head>
<body>

    <!-- Thanh đầu trang -->
    <header>
        <div class="logo">
            <h1>Cộng Đồng Java Việt Nam</h1>
        </div>
        <nav>
            <ul>
                <li><a href="/">Trang chủ</a></li>
                <li><a href="/forum">Diễn đàn</a></li>
                <li><a href="/about">Liên hệ</a></li>
            </ul>
        </nav>
    </header>

    <!-- Khu vực nội dung chính -->
    <main>
        <section class="form-section">
            <article>
                <h2>Đăng Ký Tài Khoản</h2>
                <p>Vui lòng điền đầy đủ thông tin dưới đây để tham gia cộng đồng.</p>

                <!-- Biểu mẫu nhập liệu -->
                <form action="/api/register" method="POST">
                    <div class="form-group">
                        <label for="username">Tên tài khoản:</label>
                        <input type="text" id="username" name="username" placeholder="Nhập tên đăng nhập" required>
                    </div>

                    <div class="form-group">
                        <label for="email">Địa chỉ Email:</label>
                        <input type="email" id="email" name="email" placeholder="example@gmail.com" required>
                    </div>

                    <div class="form-group">
                        <label for="city">Thành phố:</label>
                        <select id="city" name="city">
                            <option value="hn">Hà Nội</option>
                            <option value="hcm" selected>TP. Hồ Chí Minh</option>
                            <option value="dn">Đà Nẵng</option>
                        </select>
                    </div>

                    <button type="submit">Đăng Ký Ngay</button>
                </form>
            </article>
        </section>
    </main>

    <!-- Chân trang -->
    <footer>
        <p>&copy; 2026 Cộng Đồng Java. Bảo lưu mọi quyền.</p>
    </footer>

</body>
</html>
```
