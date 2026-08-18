# Java Objects

> [!abstract] Định nghĩa
> **Object (Đối tượng)** là một thực thể cụ thể (instance) được tạo ra từ bản thiết kế [[01 - Classes|Class]], sở hữu trạng thái (properties/fields) và hành vi (methods) riêng, được cấp phát vùng nhớ độc lập trong Heap memory.

---

## 1. Khởi tạo đối tượng (Instantiation)

Để tạo một đối tượng từ một Class, ta sử dụng từ khóa `new` kết hợp với **Constructor** của lớp đó:

```java
// ✅ Nên làm (Do): Khai báo và khởi tạo đối tượng trực tiếp
Student student = new Student("An", 20);
```

### Quá trình khởi chạy khi gọi `new`:
1. **Cấp phát bộ nhớ:** JVM cấp phát một vùng nhớ đủ lớn trên **Heap memory** để chứa tất cả các thuộc tính của đối tượng.
2. **Khởi tạo giá trị mặc định:** Tất cả các thuộc tính của đối tượng được gán giá trị mặc định (`0`, `false`, `null`).
3. **Chạy Constructor:** JVM thực thi mã nguồn bên trong Constructor để gán các giá trị tùy chỉnh được truyền vào.
4. **Trả về tham chiếu:** Toán tử `new` trả về địa chỉ vùng nhớ (tham chiếu) của đối tượng vừa tạo, được gán vào biến tham chiếu (ví dụ: biến `student` nằm trên bộ nhớ Stack).

---

## 2. Quản lý đối tượng trên bộ nhớ Stack và Heap

Hiểu cách JVM phân tách bộ nhớ khi làm việc với đối tượng giúp tránh các lỗi logic về tham chiếu:

```java
Student s1 = new Student("Bình");
Student s2 = s1; // s2 trỏ cùng vùng nhớ với s1 trên Heap!
s2.setName("Cường");

System.out.println(s1.getName()); // In ra "Cường" vì cả hai biến cùng trỏ vào một đối tượng.
```

- **Stack Memory:** Lưu trữ biến tham chiếu (`s1`, `s2`). Biến tham chiếu này chỉ chứa địa chỉ của đối tượng chứ không chứa chính đối tượng đó.
- **Heap Memory:** Lưu trữ đối tượng thực tế `new Student("Bình")`.

---

## 3. Vòng đời đối tượng và thu hồi bộ nhớ (Garbage Collection)

- **Vòng đời:** Bắt đầu khi đối tượng được tạo bằng `new` và kết thúc khi đối tượng không còn được sử dụng (không còn biến tham chiếu nào trỏ tới nó).
- **Garbage Collector (GC):** Bộ dọn rác của Java chạy ngầm và tự động giải phóng các vùng nhớ Heap của các đối tượng không còn bất kỳ liên kết tham chiếu nào trỏ tới, giúp lập trình viên không phải giải phóng bộ nhớ thủ công như C/C++.

```java
Student s = new Student("Dũng");
s = null; // Đối tượng "Dũng" giờ đây không còn tham chiếu nào trỏ tới, sẽ bị GC thu hồi ở lần chạy tiếp theo.
```
