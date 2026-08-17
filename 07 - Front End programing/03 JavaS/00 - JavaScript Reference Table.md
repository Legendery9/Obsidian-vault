# 00 - JavaScript Reference Table

Tài liệu này cung cấp bảng tham chiếu tổng hợp các câu lệnh, phương thức và DOM API cốt lõi trong JavaScript (ES6+) theo nguyên lý 20/80, tối ưu hóa cho phát triển web hiện đại.

---

## 1. Cú pháp cơ bản & Câu lệnh (Statements & Control Flow)

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `let` | Khai báo biến có thể gán lại giá trị. | Giới hạn trong phạm vi khối lệnh (block scope: `{...}`). | Dùng thay thế hoàn toàn cho `var`. Ví dụ: `let count = 0; count++;`. | Không thể khai báo lại biến trùng tên trong cùng một block. |
| `const` | Khai báo hằng số. | Giá trị của hằng số không thể gán lại trực tiếp. Giới hạn phạm vi block scope. | Dùng làm khai báo mặc định trừ khi biến cần thay đổi giá trị. Ví dụ: `const PI = 3.14;`. | Đối với Object hoặc Array khai báo bằng `const`, ta vẫn có thể sửa đổi các thuộc tính/phần tử bên trong. |
| `if` ... `else` | Câu lệnh điều kiện rẽ nhánh. | Thực thi khối mã lệnh dựa trên kết quả kiểm tra điều kiện (đúng/sai). | Ví dụ: `if (score >= 50) { console.log("Pass"); } else { console.log("Fail"); }`. | Nên sử dụng Toán tử ba ngôi (Ternary Operator `cond ? val1 : val2`) cho các điều kiện gán giá trị đơn giản để code ngắn gọn. |
| `switch` | Câu lệnh rẽ nhánh nhiều trường hợp. | Thay thế chuỗi `if...else` dài khi so sánh một biến với nhiều giá trị cố định. | So sánh nghiêm ngặt (`===`). Mỗi `case` cần có câu lệnh `break` để tránh rơi xuống các case dưới. | Có thể dùng `default` để bắt các trường hợp còn lại. |
| `for...of` | Vòng lặp duyệt phần tử. | Lặp qua các phần tử của một đối tượng lặp được (Iterable: Array, String, Map, Set). | Trả về trực tiếp giá trị của từng phần tử. Ví dụ: `for (const item of items) { console.log(item); }`. | Không lấy được index trực tiếp (nếu muốn lấy index, hãy dùng `forEach` hoặc `.entries()`). |
| `for...in` | Vòng lặp duyệt thuộc tính. | Lặp qua các thuộc tính có thể duyệt (enumerable properties) của một Object. | Trả về các khóa (keys/properties) của đối tượng. Ví dụ: `for (const key in obj) { console.log(key, obj[key]); }`. | Tránh dùng `for...in` để duyệt mảng vì thứ tự lặp không được bảo đảm và có thể duyệt cả các thuộc tính prototype. |
| `try` ... `catch` ... `finally` | Cơ chế xử lý ngoại lệ (Error handling). | Bắt các lỗi xảy ra trong khối `try` để tránh crash ứng dụng, xử lý lỗi trong `catch` và dọn dẹp tài nguyên trong `finally`. | `finally` luôn luôn chạy bất kể có lỗi xảy ra hay không. | Rất quan trọng khi gọi API hoặc thực hiện các tác vụ I/O có khả năng thất bại. |
| `() => {}` (Arrow Function) | Hàm mũi tên. | Cú pháp viết hàm ngắn gọn hơn, không tự tạo ngữ cảnh `this` riêng. | Thừa hưởng `this` từ phạm vi cha bao bọc nó (lexical scoping). Ví dụ: `const add = (a, b) => a + b;`. | Không thể dùng làm hàm dựng (constructor) để `new` đối tượng. Không có đối tượng `arguments`. |
| `import` / `export` | Quản lý Module. | Chia sẻ mã nguồn giữa các tệp tin JS khác nhau. | `export default ...` để xuất mặc định, `import { name } from './module.js'` để nhập các xuất có tên (named exports). | Yêu cầu cấu hình thẻ script trong HTML là `<script type="module">`. |

---

## 2. Phương thức xử lý Mảng & Đối tượng (Array & Object Methods)

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `map()` | Biến đổi mảng. | Tạo ra một mảng mới có kích thước bằng mảng cũ, với các phần tử đã được biến đổi qua callback. | Không làm thay đổi mảng gốc. Ví dụ: `const doubled = arr.map(x => x * 2);`. | Luôn phải trả về giá trị (`return`) trong callback function. |
| `filter()` | Lọc phần tử mảng. | Tạo một mảng mới chứa các phần tử thỏa mãn điều kiện logic của hàm callback. | Không thay đổi mảng gốc. Trả về mảng rỗng nếu không có phần tử nào thỏa mãn. Ví dụ: `const evens = arr.filter(x => x % 2 === 0);`. | Callback trả về giá trị truthy để giữ lại phần tử, falsy để loại bỏ. |
| `reduce()` | Tích lũy giá trị mảng. | Thu gọn mảng thành một giá trị duy nhất (số, chuỗi, object, mảng khác) bằng cách chạy một hàm accumulator qua từng phần tử. | Nhận 2 tham số: callback function và giá trị khởi tạo (`initialValue`). Ví dụ: `const total = arr.reduce((sum, val) => sum + val, 0);`. | Nếu không truyền `initialValue`, phần tử đầu tiên của mảng sẽ được lấy làm giá trị khởi tạo ban đầu. |
| `forEach()` | Duyệt mảng. | Thực thi một hàm callback trên từng phần tử của mảng. | Không trả về giá trị (trả về `undefined`). Không thay đổi mảng gốc trực tiếp trừ khi chỉnh sửa tham chiếu. | Không thể sử dụng `break` hay `continue` để ngắt vòng lặp này giữa chừng (dùng `for...of` nếu cần ngắt). |
| `find()` | Tìm kiếm phần tử đầu tiên. | Trả về giá trị của phần tử đầu tiên trong mảng thỏa mãn điều kiện. | Trả về `undefined` nếu không tìm thấy. Ví dụ: `const user = users.find(u => u.id === 1);`. | Nhanh hơn `filter` khi chỉ cần tìm một phần tử duy nhất vì sẽ dừng lặp ngay khi tìm thấy. |
| `some()` | Kiểm tra tồn tại ít nhất một. | Trả về `true` nếu có ít nhất một phần tử trong mảng thỏa mãn điều kiện. | Ví dụ: `const hasNegative = arr.some(x => x < 0);`. | Dừng lặp sớm ngay khi tìm thấy phần tử đầu tiên thỏa mãn. |
| `every()` | Kiểm tra tất cả thỏa mãn. | Trả về `true` chỉ khi tất cả phần tử trong mảng đều thỏa mãn điều kiện. | Ví dụ: `const allAdults = users.every(u => u.age >= 18);`. | Trả về `true` đối với mảng rỗng (vacuous truth). |
| `Object.keys()` | Trích xuất khóa đối tượng. | Trả về một mảng chứa toàn bộ các khóa (property names) của đối tượng. | Ví dụ: `const keys = Object.keys(user);`. | Thường dùng để đếm số thuộc tính hoặc dùng làm cơ sở để duyệt qua Object. |
| `Object.values()` | Trích xuất giá trị đối tượng. | Trả về một mảng chứa toàn bộ giá trị (property values) của đối tượng. | Ví dụ: `const values = Object.values(user);`. | Tiện lợi khi cần kiểm tra xem một giá trị có tồn tại trong đối tượng hay không. |
| `Object.entries()` | Trích xuất cặp khóa-giá trị. | Trả về một mảng chứa các mảng con dạng `[key, value]`. | Rất phù hợp khi kết hợp với vòng lặp `for...of` giải cấu trúc (destructuring). | Ví dụ: `for (const [key, val] of Object.entries(obj)) { ... }`. |

---

## 3. Lập trình bất đồng bộ (Promises & Async/Await)

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `Promise` | Đối tượng đại diện cho tác vụ bất đồng bộ. | Quản lý kết quả của một hành động bất đồng bộ ở 3 trạng thái: `pending` (đang xử lý), `fulfilled` (thành công), `rejected` (thất bại). | Sử dụng `.then()` để nhận kết quả thành công và `.catch()` để xử lý lỗi. | Tránh rơi vào tình trạng "Promise Hell" bằng cách chuỗi hóa các Promise (Promise chaining). |
| `async` / `await` | Cú pháp viết code bất đồng bộ tuần tự. | Viết code bất đồng bộ trông giống như đồng bộ, giúp dễ đọc và bảo trì hơn. | Khai báo `async` trước hàm. Sử dụng từ khóa `await` trước một Promise để dừng đợi kết quả. | Luôn bọc khối mã `await` trong `try...catch` để bắt lỗi khi Promise bị từ chối (reject). |
| `Promise.all()` | Chạy song song nhiều Promise. | Nhận vào một mảng các Promise và chỉ hoàn thành khi toàn bộ các Promise trong mảng thành công. | Trả về một mảng kết quả theo đúng thứ tự truyền vào. Ví dụ: `const [res1, res2] = await Promise.all([p1, p2]);`. | Sẽ bị lỗi (`reject`) ngay lập tức nếu có bất kỳ một Promise con nào trong mảng bị lỗi (fail-fast). |

---

## 4. Tương tác DOM & Sự kiện (DOM APIs & Event Listeners)

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `document.getElementById()` | Lấy phần tử theo ID. | Tìm và trả về phần tử đầu tiên có thuộc tính ID trùng khớp. | Ví dụ: `const el = document.getElementById("my-id");`. | Trả về `null` nếu không tìm thấy. Hiệu năng cực tốt vì được tối ưu hóa ở cấp độ trình duyệt. |
| `document.querySelector()` | Tìm phần tử theo CSS Selector. | Trả về phần tử đầu tiên khớp với bộ chọn CSS chỉ định. | Ví dụ: `const firstBtn = document.querySelector(".container .btn");`. | Rất linh hoạt, cho phép tìm kiếm theo class, tag, attribute phức tạp. Trả về `null` nếu không khớp. |
| `document.querySelectorAll()` | Tìm danh sách phần tử theo CSS. | Trả về danh sách tất cả phần tử khớp với bộ chọn dưới dạng một mảng tĩnh (NodeList). | Ví dụ: `const items = document.querySelectorAll(".list-item");`. | NodeList không phải là mảng thực thụ nhưng có sẵn phương thức `.forEach()`. |
| `document.createElement()` | Tạo phần tử mới. | Khởi tạo một nút phần tử HTML mới trong bộ nhớ, chưa chèn vào giao diện. | Nhận tên thẻ HTML cần tạo. Ví dụ: `const newDiv = document.createElement("div");`. | Cần sử dụng các phương thức như `appendChild()` hoặc `prepend()` của thẻ cha để chèn nó vào DOM. |
| `element.classList` (`add`/`remove`/`toggle`) | Quản lý các lớp CSS của phần tử. | Thêm, xóa hoặc đảo trạng thái (ẩn/hiện) class CSS của phần tử mà không cần can thiệp trực tiếp vào `className`. | Ví dụ: `el.classList.add("active"); el.classList.toggle("hidden");`. | Phương thức sạch sẽ nhất để kích hoạt CSS hiệu ứng động từ JS. |
| `element.innerHTML` | Lấy/Thay thế nội dung HTML. | Lấy ra hoặc ghi đè toàn bộ cấu trúc HTML bên trong phần tử. | Ví dụ: `el.innerHTML = "<p>Nội dung mới</p>";`. | [!WARNING] Nguy cơ dính lỗi bảo mật **XSS** nếu chèn nội dung nhập từ phía người dùng mà không lọc. |
| `element.textContent` | Lấy/Thay thế nội dung văn bản thuần. | Chỉ lấy hoặc thay thế nội dung dạng chữ thuần túy bên trong phần tử, loại bỏ tất cả thẻ HTML. | Ví dụ: `el.textContent = "Chữ thuần túy";`. | An toàn trước các cuộc tấn công XSS. Nhanh và nhẹ hơn `innerHTML`. |
| `element.addEventListener()` | Đăng ký sự kiện. | Gắn một bộ lắng nghe sự kiện (như `click`, `submit`, `keydown`) vào phần tử để chạy hàm callback khi sự kiện xảy ra. | Nhận tên sự kiện và hàm xử lý. Ví dụ: `btn.addEventListener("click", (e) => { ... });`. | Tham số `e` (Event Object) chứa các thông tin như phần tử bị click, vị trí chuột, v.v. Dùng `e.preventDefault()` để chặn hành vi mặc định (như submit form). |

---

## Ví dụ thực tế: Xử lý mảng nâng cao (Map, Filter, Reduce)

Giả sử ta có danh sách đơn hàng của người dùng, cần tính tổng tiền của các đơn hàng đã thanh toán có giá trị từ 100$ trở lên.

```javascript
const orders = [
    { id: 101, product: "Laptop", price: 1200, status: "completed" },
    { id: 102, product: "Mouse", price: 25, status: "completed" },
    { id: 103, product: "Keyboard", price: 80, status: "pending" },
    { id: 104, product: "Monitor", price: 300, status: "completed" },
    { id: 105, product: "USB Drive", price: 15, status: "completed" }
];

// Thực hiện chuỗi xử lý (Chaining)
const totalHighValuePaid = orders
    // 1. Lọc ra các đơn hàng đã thanh toán (completed)
    .filter(order => order.status === "completed")
    // 2. Lọc ra các sản phẩm có giá trị >= 100$
    .filter(order => order.price >= 100)
    // 3. Tích lũy cộng tổng giá tiền
    .reduce((sum, order) => sum + order.price, 0);

console.log("Tổng tiền đơn hàng giá trị cao đã thanh toán:", totalHighValuePaid);
// Kết quả mong đợi: 1200 + 300 = 1500
```

---

## Ví dụ thực tế: Gọi API với Async/Await & Render DOM

Gọi danh sách người dùng từ API công cộng giả lập và render hiển thị lên danh sách HTML.

```javascript
// Hàm bất đồng bộ lấy dữ liệu người dùng
async function fetchAndRenderUsers() {
    const listContainer = document.getElementById("user-list");
    
    // Hiển thị trạng thái đang tải
    listContainer.innerHTML = "<li>Đang tải dữ liệu...</li>";

    try {
        const response = await fetch("https://jsonplaceholder.typicode.com/users");
        
        // Kiểm tra xem phản hồi có thành công (200-299) hay không
        if (!response.ok) {
            throw new Error(`Lỗi HTTP! Trạng thái: ${response.status}`);
        }

        const users = await response.json();

        // Xóa nội dung cũ trước khi render danh sách mới
        listContainer.innerHTML = "";

        // Duyệt danh sách và tạo phần tử DOM
        users.forEach(user => {
            const li = document.createElement("li");
            li.classList.add("user-item");
            
            // Sử dụng textContent để chống tấn công XSS bảo mật thông tin
            li.textContent = `${user.name} - Email: ${user.email}`;
            
            listContainer.appendChild(li);
        });

    } catch (error) {
        console.error("Lỗi khi fetch dữ liệu:", error);
        listContainer.innerHTML = `<li class="error-msg">Không thể tải danh sách: ${error.message}</li>`;
    }
}

// Chạy hàm khi trang tải xong
document.addEventListener("DOMContentLoaded", fetchAndRenderUsers);
```
