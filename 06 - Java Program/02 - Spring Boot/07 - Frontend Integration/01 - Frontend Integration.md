# Frontend Integration

> [!abstract] Định nghĩa
> Note này tóm tắt các kiến thức cơ bản về HTML5, JavaScript thuần (Vanilla JS), Hệ thống lưới responsive của Bootstrap, và phím tắt Emmet thường dùng để hỗ trợ lập trình viên xây dựng giao diện hiển thị cho các ứng dụng web Spring MVC.

---

## 1. Các thẻ HTML5 cơ bản thường dùng trong View

Cấu trúc tài liệu HTML5 chuẩn luôn bao gồm khai báo `<!DOCTYPE html>`, thẻ `<html>`, phần `<head>` chứa siêu dữ liệu (metadata) và phần `<body>` chứa nội dung hiển thị:

- **Thẻ cấu trúc:** `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`, `<div>`, `<span>`.
- **Thẻ nội dung:** `<h1>` → `<h6>` (Heading), `<p>` (Đoạn văn), `<ul>` / `<ol>` / `<li>` (Danh sách).
- **Thẻ liên kết & Media:** `<a href="...">` (Đường dẫn), `<img src="..." alt="...">` (Hình ảnh).
- **Thẻ bảng:** `<table>`, `<thead>`, `<tbody>`, `<tr>`, `<th>` (Cột tiêu đề), `<td>` (Ô dữ liệu).
- **Thẻ Form:** `<form>`, `<input>` (Nhập liệu), `<select>` (Dropdown), `<textarea>`, `<button>`.

```html
<!-- Cấu trúc Form chuẩn dùng cho Spring Boot Controller nhận dữ liệu -->
<form action="/submit" method="POST">
    <div class="form-group">
        <label for="username">Tên người dùng:</label>
        <input type="text" id="username" name="username" required>
    </div>
    <button type="submit">Gửi</button>
</form>
```

---

## 2. JavaScript tương tác giao diện cơ bản

JavaScript giúp tương tác và xử lý sự kiện phía client (Dynamic UI):

- **Khai báo biến:** `const` (hằng số), `let` (biến có thể thay đổi). Tránh dùng `var` (scoping cũ).
- **Truy xuất phần tử DOM:** `document.getElementById('id')` hoặc `document.querySelector('.class')`.
- **Lắng nghe sự kiện:** `addEventListener()`.

```javascript
// ✅ Nên làm (Do): Đợi DOM tải xong trước khi gắn sự kiện JS.
document.addEventListener("DOMContentLoaded", () => {
    const btn = document.getElementById("submit-btn");
    
    btn.addEventListener("click", (event) => {
        // Ngăn form submit mặc định để kiểm tra dữ liệu trước bằng JS
        event.preventDefault(); 
        
        const nameInput = document.getElementById("username").value;
        if (nameInput.trim() === "") {
            alert("Tên đăng nhập không được rỗng!");
        }
    });
});
```

---

## 3. Lưới Responsive Grid và Breakpoints của Bootstrap 5

Bootstrap cung cấp hệ thống lưới (Grid System) chia bề ngang màn hình thành **12 cột**. 
Cấu trúc cơ bản phải đi từ: **Container** → **Row (Dòng)** → **Col (Cột)**.

```html
<div class="container">
    <div class="row">
        <!-- Trên màn hình lớn chiếm 4/12 cột, trên màn hình trung bình chiếm 6/12 cột, trên màn hình nhỏ chiếm 12/12 cột -->
        <div class="col-12 col-md-6 col-lg-4">
            Cột nội dung 1
        </div>
        <div class="col-12 col-md-6 col-lg-4">
            Cột nội dung 2
        </div>
    </div>
</div>
```

### Các mốc responsive (Breakpoints) chính của Bootstrap 5:
- **`xs` (Kích thước cực nhỏ):** `< 576px` (Không cần hậu tố class, ví dụ `col-6`).
- **`sm` (Màn hình nhỏ/Mobile):** `≥ 576px` (ví dụ `col-sm-6`).
- **`md` (Màn hình trung bình/Tablet):** `≥ 768px` (ví dụ `col-md-6`).
- **`lg` (Màn hình lớn/Laptop):** `≥ 992px` (ví dụ `col-lg-4`).
- **`xl` (Màn hình cực lớn):** `≥ 1200px` (ví dụ `col-xl-3`).
- **`xxl` (Màn hình siêu lớn):** `≥ 1400px`.

---

## 4. Phím tắt Emmet thông dụng để viết code HTML nhanh

Sử dụng Emmet trong các trình soạn thảo (IntelliJ, VS Code) để sinh nhanh cấu trúc HTML bằng cách gõ ký hiệu rồi nhấn phím `Tab`:

- **Tạo thẻ có Class/ID:** `div.container` → `<div class="container"></div>` | `input#email` → `<input id="email">`
- **Quan hệ cha con (`>`):** `ul>li` → `<ul><li></li></ul>`
- **Quan hệ đồng cấp (`+`):** `h1+p` → `<h1></h1><p></p>`
- **Phép nhân tạo nhiều thẻ (`*`):** `ul>li*3` → tạo danh sách `ul` chứa 3 thẻ `li`.
- **Ghi văn bản bên trong (`{}`):** `button{Click Me}` → `<button>Click Me</button>`
