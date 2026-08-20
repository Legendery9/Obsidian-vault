# Quy tắc áp dụng chung

> [!important]  
> **Phạm vi áp dụng:** Các quy tắc dưới đây luôn được áp dụng khi làm việc với Obsidian cho đến khi người dùng trực tiếp yêu cầu thay đổi hoặc hủy bỏ.

---

## 1. Chuẩn hóa đặt tên
- Sử dụng định dạng `{index} - {context}` cho **thư mục và tệp tin**.
- `index` là số thứ tự.
- `context` phải là **từ hoặc cụm từ tiếng Anh**, ngắn gọn và mô tả đúng nội dung.
- Duy trì cách đặt tên nhất quán trong toàn bộ Vault.
**Ví dụ:**
```text
01 - Java
02 - Obsidian system
03 - Coding environment
```

---

## 2. Khử trùng lặp
- Không lặp lại cùng một kiến thức ở nhiều file nếu không cần thiết.
- Kiến thức chỉ nên được viết tại **một file phù hợp nhất**.
- Các file khác sử dụng Obsidian wikilink để tham chiếu:
```markdown
[[context]]
```
- Ưu tiên `[[wikilink]]` thay vì sao chép nội dung.
- Sử dụng tag khi cần phân loại hoặc nhóm nội dung.

---

## 3. Nguyên tắc 20/80
Tập trung vào **20% kiến thức cốt lõi mang lại 80% giá trị**.
- Ưu tiên kiến thức thường xuyên sử dụng.
- Loại bỏ thông tin dư thừa, trùng lặp hoặc ít giá trị.
- Không mở rộng quá sâu nếu không phục vụ mục đích thực tế.
- Ưu tiên:
    1. Khái niệm cốt lõi.
    2. Cú pháp/cách sử dụng phổ biến.
    3. Ví dụ thực tế.
    4. Lỗi và lưu ý quan trọng.
    5. So sánh khi cần phân biệt các khái niệm.

---

## 4. Visual Formatting
- Tuân thủ đầy đủ quy tắc định dạng được quy định tại [[02 - Obsidian format OPTIMIZATION]].
- Phân tách các heading lớn bằng `---`.
- Sử dụng callout phù hợp:
```markdown
> [!abstract]
> Tóm tắt hoặc ý chính.

> [!info]
> Thông tin bổ sung.

> [!note]
> Ghi chú quan trọng.

> [!warning]
> Cảnh báo hoặc lỗi dễ gặp.
```
- Code block phải có **syntax highlighting** phù hợp.
- Ví dụ Java:
```java
String name = "Long";
System.out.println(name);
```
- Sử dụng **Do / Don't** khi cách trình bày đối lập giúp làm rõ vấn đề.
- Sử dụng:
    - **Inline code** cho class, method, biến, cú pháp, command...
    - **LaTeX** cho công thức và ký hiệu toán học.
    - **Table** cho nội dung phù hợp với dạng tra cứu nhanh.

---

## 5. Hoàn thiện nội dung
Với mỗi file `.md`:
- Rà soát toàn bộ nội dung.
- Bổ sung phần còn thiếu.
- Viết lại phần chưa rõ ràng.
- Loại bỏ nội dung dư thừa hoặc trùng lặp.
- Đảm bảo nội dung tuân thủ nguyên tắc 20/80.
- Chỉ thêm các thành phần phù hợp với nội dung thực tế của file.
Có thể bổ sung các heading sau khi phù hợp:
### Định nghĩa
Giải thích khái niệm và bản chất.
### Tác dụng
Giải thích mục đích và trường hợp sử dụng.
### Bảng
Sử dụng khi nội dung phù hợp với dạng tra cứu:
- Cú pháp.
- Command.
- Attribute.
- Method.
- Property.
- Phím tắt.
- Keyword.
- Format specifier.
### Lưu ý
Chỉ sử dụng khi có điểm quan trọng cần ghi nhớ.
> [!note]  
> Không bắt buộc mọi file phải có tất cả các heading trên. Chỉ sử dụng heading phù hợp với nội dung thực tế.

---

## 6. Ghi log tiến độ
Sau mỗi mục hoàn thành, phải cập nhật **đúng file log tương ứng với folder đang được xử lý**.
### File log
- Mỗi folder có **1 file log riêng**.
- File log nằm tại:
```text
03 - Ai Prompt/Prompt progress - implementation
```
- File log sử dụng định dạng:
```text
implementation - {context}
```
- `{context}` của file log phải **trùng với `context` của folder chủ đề**.
**Ví dụ:**
```text
Folder:
02 - Obsidian system

Log:
implementation - Obsidian system
```
### Đọc log trước khi làm
> [!warning]  
> **BẮT BUỘC:** Phải đọc file log tương ứng trước khi bắt đầu xử lý một folder.

Nếu file log chưa tồn tại:
- Tạo file log mới.
- Sử dụng đúng cấu trúc chuẩn:
```markdown
# Checklist tổng

# Quy tắc áp dụng

# Nhật ký thay đổi

# Trạng thái hiện tại

# Lưu ý
```
### Cập nhật log
Sau mỗi phần hoàn thành:
- Đánh dấu checkbox đã hoàn thành.
- Ghi rõ folder/file đã được đổi tên.
- Ghi rõ file đã được chỉnh sửa.
- Ghi rõ nội dung đã hoàn thiện hoặc bổ sung.
- Ghi rõ bảng đã được thêm.
- Ghi nhận các thay đổi quan trọng khác.
Nếu dừng giữa chừng, phải ghi rõ:
- Folder đang xử lý.
- File đang xử lý.
- Phần đang làm dở.
- Công việc còn lại.
- Điểm cần tiếp tục ở phiên sau.

---

## 7. Thứ tự xử lý
> [!warning]  
> **Xử lý tuần tự từng folder. Không chuyển sang folder tiếp theo khi folder hiện tại chưa hoàn thành hoàn toàn.**

Ví dụ:
```text
02 - Obsidian system
        ↓
Hoàn thành toàn bộ
        ↓
05 - Coding environment
        ↓
Hoàn thành toàn bộ
        ↓
Folder tiếp theo
```
Không xử lý đồng thời nhiều folder, **trừ khi người dùng yêu cầu rõ ràng**.

---

## 8. Quy trình chống trùng lặp
Trước khi bổ sung kiến thức vào file:
1. Kiểm tra xem kiến thức đã tồn tại ở file khác chưa.
2. Nếu chưa tồn tại → bổ sung vào file phù hợp nhất.
3. Nếu đã tồn tại → không sao chép lại toàn bộ.
4. Sử dụng wikilink để tham chiếu:
```markdown
[[context]]
```
5. Sử dụng tag khi cần hỗ trợ phân loại hoặc tìm kiếm.
> [!note]  
> Mục tiêu là xây dựng Vault theo mô hình **mỗi kiến thức có một nơi lưu trữ chính**, các file khác tham chiếu đến nơi đó thay vì sao chép nội dung.

---

## 9. Thứ tự ưu tiên
Khi có xung đột giữa các yêu cầu trong quá trình xử lý, ưu tiên:
1. **Yêu cầu trực tiếp mới nhất của người dùng.**
2. **Quy tắc Obsidian hiện hành do người dùng thiết lập.**
3. **Tính chính xác của nội dung.**
4. **Chống trùng lặp.**
5. **Nguyên tắc 20/80.**
6. **Tính nhất quán về cấu trúc và Visual Formatting.**
> [!important]  
> Các quy tắc này tiếp tục được áp dụng trong các phiên làm việc sau **cho đến khi người dùng trực tiếp yêu cầu thay đổi hoặc hủy bỏ**.