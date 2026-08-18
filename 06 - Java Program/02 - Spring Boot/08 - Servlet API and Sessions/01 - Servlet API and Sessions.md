# Servlet API and Sessions

> [!abstract] Định nghĩa
> **Servlet API** là tập hợp các giao diện và lớp nền tảng thấp (low-level) trong Java EE / Jakarta EE mà Spring Boot Web được xây dựng dựa trên nó để giao tiếp với Web Server (Tomcat).
> Cung cấp khả năng thao tác trực tiếp trên Request, Response, Session và Cookie của client.

---

## 1. HttpServletRequest (Yêu cầu từ Client)

Dùng để đọc các thông tin gửi lên từ trình duyệt của Client. Có thể inject trực tiếp làm đối số trong phương thức Controller của Spring Boot.

### Các hàm phổ biến:
- `getParameter(String name)`: Lấy giá trị của một form input hoặc query parameter. Trả về `String`.
- `getAttribute(String name)` / `setAttribute(String name, Object o)`: Đọc và ghi các thuộc tính trong phạm vi request (thường dùng để truyền dữ liệu qua các Filter/Interceptor).
- `getHeader(String name)`: Lấy giá trị của HTTP Header (ví dụ: `User-Agent`, `Authorization`).
- `getCookies()`: Trả về một mảng `Cookie[]` chứa toàn bộ cookies client gửi lên.
- `getSession()` / `getSession(boolean create)`: Lấy Session hiện tại, hoặc tự động tạo mới nếu chưa tồn tại.

---

## 2. HttpServletResponse (Phản hồi về Client)

Dùng để cấu hình dữ liệu gửi trả về cho Client.

### Các hàm phổ biến:
- `setStatus(int sc)`: Đặt mã trạng thái HTTP (ví dụ: `200`, `201`, `401`).
- `sendRedirect(String location)`: Gửi lệnh chuyển hướng HTTP 302 về trình duyệt.
- `setHeader(String name, String value)`: Ghi giá trị HTTP Header.
- `setContentType(String type)` / `setCharacterEncoding(String charset)`: Đặt kiểu định dạng dữ liệu (ví dụ: `text/html`, `application/json`) và bộ gõ ngôn ngữ (thường dùng `UTF-8`).
- `addCookie(Cookie cookie)`: Thêm một cookie mới xuống trình duyệt của client.
- `getWriter()`: Trả về đối tượng `PrintWriter` để ghi trực tiếp văn bản thô vào thân phản hồi (HTTP response body).

---

## 3. HttpSession (Quản lý phiên làm việc)

Lưu trữ trạng thái của người dùng trên Server giữa nhiều request khác nhau (ví dụ: lưu thông tin người dùng đã đăng nhập).

```java
// ✅ Nên làm (Do): Sử dụng HttpSession để lưu giữ trạng thái đăng nhập.
@PostMapping("/login")
public String login(@RequestParam String username, HttpSession session) {
    User user = userService.authenticate(username);
    if (user != null) {
        // Gán đối tượng user vào session
        session.setAttribute("currentUser", user);
    }
    return "redirect:/dashboard";
}
```

### Các hàm quản lý Session:
- `setAttribute(String name, Object value)`: Lưu trữ dữ liệu vào session.
- `getAttribute(String name)`: Lấy dữ liệu từ session. Trả về `Object` (cần ép kiểu).
- `removeAttribute(String name)`: Xóa một dữ liệu cụ thể trong session.
- `invalidate()`: Hủy hoàn toàn phiên làm việc hiện tại (thường dùng khi Đăng xuất).
- `setMaxInactiveInterval(int interval)`: Đặt thời gian tự động hết hạn session (timeout) sau `interval` giây không hoạt động.

---

## 4. Cookie (Lưu trữ phía Client)

Cookie là các cặp key-value nhỏ được server gửi xuống trình duyệt để lưu lại và tự động gửi ngược lên server ở các request sau.

```java
import jakarta.servlet.http.Cookie;
import jakarta.servlet.http.HttpServletResponse;

public void createCookie(HttpServletResponse response) {
    Cookie cookie = new Cookie("userTheme", "dark");
    
    // ✅ Nên làm (Do): Sử dụng HttpOnly và Secure để bảo vệ Cookie khỏi tấn công XSS và trộm cắp session.
    cookie.setHttpOnly(true); // Ngăn JavaScript đọc cookie
    cookie.setSecure(true);   // Chỉ truyền qua kênh mã hóa HTTPS
    cookie.setMaxAge(7 * 24 * 60 * 60); // Sống trong 7 ngày (tính bằng giây)
    
    response.addCookie(cookie);
}
```
