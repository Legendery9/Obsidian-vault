# Block Reference trong Obsidian

---

## Định nghĩa
**Block Reference** là một tính năng mạnh mẽ của Obsidian cho phép liên kết trực tiếp đến một đoạn văn bản (block) hoặc một tiêu đề (heading) cụ thể trong cùng một file hoặc giữa các file khác nhau trong Vault, thay vì chỉ liên kết đến toàn bộ tệp ghi chú.

---

## Tác dụng
- **Tham chiếu chính xác:** Trỏ thẳng tới dòng hoặc đoạn cần đọc, tiết kiệm thời gian tìm kiếm của người đọc.
- **Tránh trùng lặp:** Giúp tái sử dụng thông tin từ một nguồn duy nhất mà không cần sao chép nội dung sang nhiều nơi.
- **Tạo mối liên kết chặt chẽ:** Tăng tính kết nối phi tuyến tính giữa các khối kiến thức.

---

## Cú pháp chi tiết

Cú pháp tổng quát:
```markdown
[[{fileMdName}#{target}|{displayText}]]
```
với `{target} = {heading}` hoặc `^{blockId}`.

### a) Liên kết đến một Block cụ thể (không phải Heading)
- **Bước 1 (Gán ID):** Tại vị trí block muốn liên kết tới trong file đích, đặt dấu cách kèm theo `^{id}` ở cuối block đó.
- **Bước 2 (Tạo Link):** Từ file khác, liên kết tới block đó bằng: `[[{fileMdName}#^{id}]]`
- **Đổi tên hiển thị (tùy chọn):** `[[{fileMdName}#^{id}|{replaceContext}]]`

### b) Liên kết đến một Heading
- **Tạo Link:** `[[{fileMdName}#{heading}]]`
- **Đổi tên hiển thị (tùy chọn):** `[[{fileMdName}#{heading}|{displayText}]]`

### Chi tiết các thành phần cú pháp

| Thành phần | Ý nghĩa |
|---|---|
| `{fileMdName}` | Tên file `.md` đích |
| `#` | Ký tự phân cách giữa tên file và vị trí bên trong file |
| `^{id}` | Block ID của block cần trỏ tới (phần ID tự định nghĩa hoặc do Obsidian sinh ra) |
| `\|` | Ký tự phân cách giữa đích liên kết và tên hiển thị |
| `{replaceContext}` / `{displayText}` | Nội dung hiển thị thay cho tên file/block gốc |

---

## Ví dụ minh họa thực tế

### Ví dụ 1: Liên kết đến một Heading cụ thể
Để trỏ tới danh sách website đáng tin cậy trong file Quy tắc Obsidian:
```markdown
[[02 - Rules for working with Obsidian folders and notes#11. Bảng danh sách website đáng tin cậy|Danh sách website đáng tin cậy]]
```
Hiển thị: [[02 - Rules for working with Obsidian folders and notes#11. Bảng danh sách website đáng tin cậy|Danh sách website đáng tin cậy]]

### Ví dụ 2: Liên kết đến một Block cụ thể bằng Block ID
Tại file đích `02 - Rules for working with Obsidian folders and notes.md`, ta có block:
```markdown
Tập trung vào 20% kiến thức cốt lõi mang lại 80% giá trị. ^rule-20-80
```
Từ một file khác, ta tham chiếu tới quy tắc này:
```markdown
[[02 - Rules for working with Obsidian folders and notes#^rule-20-80|Nguyên tắc 20/80]]
```
Hiển thị: [[02 - Rules for working with Obsidian folders and notes#^rule-20-80|Nguyên tắc 20/80]]

---

## Lưu ý
> [!important] Ưu tiên sử dụng Block Reference
> Khi cần trỏ chính xác tới một dòng hoặc một đoạn nội dung cụ thể trong file khác, hãy luôn ưu tiên sử dụng Block Reference thay vì chỉ liên kết tới cả file hoặc tiêu đề lớn. Điều này giúp tăng tính chính xác và cải thiện trải nghiệm đọc trong Obsidian.
