# QUY TẮC ĐỊNH DẠNG — OBSIDIAN OPTIMIZATION

## 1. Rich Markdown Hierarchy

Mọi nội dung phải được trình bày theo cấu trúc Markdown rõ ràng, ưu tiên khả năng đọc trong cả **Live Preview** và **Reading Mode** của Obsidian.
- Sử dụng `##` cho các phần chính.
- Sử dụng `###` cho các phần con.
- Sử dụng bullet points cho danh sách.
- Sử dụng **bold** cho:
    - Thuật ngữ chính.
    - Khái niệm quan trọng.
    - Quy tắc.
    - Tham số hoặc giá trị cần nhấn mạnh.
- Không lạm dụng heading hoặc bold nếu không cần thiết.
- Không tạo heading cấp `#` nếu tài liệu đã có title riêng.
## 2. Obsidian Callouts
Sử dụng Obsidian Callout khi nó thực sự giúp phân biệt loại thông tin.
### `[!abstract]`
Dùng cho:
- Định nghĩa tổng quan.
- Tóm tắt nội dung chính.
- Ý tưởng cốt lõi cần nắm trước khi đọc chi tiết.
Nên đặt ở đầu note hoặc đầu một phần lớn.
### `[!info]`
Dùng cho:
- Danh sách ký hiệu.
- Tham số.
- Thuật ngữ và ý nghĩa.
- Thông tin tham khảo cần ghi nhớ.
### `[!warning]`
Dùng cho:
- Lỗi thường gặp.
- Điều kiện đặc biệt.
- Những điểm dễ hiểu sai.
- Những điều cần tránh.
- Giới hạn hoặc ngoại lệ của một quy tắc.
### `[!note]`
**Chỉ dùng** cho:
- Phần **Solution / Lời giải**.
- Ví dụ giải thích chi tiết.
- Quá trình suy luận hoặc triển khai một lời giải.
Không sử dụng `[!note]` một cách mặc định cho mọi nội dung.
## 3. Coding Format
### 3.1. Code Block
Mọi đoạn code nhiều dòng phải sử dụng fenced code block và khai báo ngôn ngữ để hỗ trợ syntax highlighting.
Ví dụ:
```java
public class Example {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```
Không sử dụng code block không khai báo ngôn ngữ khi có thể xác định được ngôn ngữ.
### 3.2. Inline Code
Các thành phần code xuất hiện trong văn bản phải được đặt trong backtick:
- Tên biến: `variableName`
- Tên method: `calculateResult()`
- Tên class: `BaseCalculator`
- Keyword: `public`, `class`, `return`
- Kiểu dữ liệu: `String`, `int`
- Tên file: `Main.java`
- Tên annotation: `@Override`
Quy tắc này **không áp dụng cho nội dung bên trong code block**.
### 3.3. Do / Don't
Khi giải thích **coding convention hoặc quy tắc viết code**, phải trình bày ví dụ đối lập:
```java
// ✅ Nên làm (Do)
// Tên class sử dụng PascalCase theo Java naming convention.
public class BaseCalculator {
}
```
```java
// ❌ Không nên làm (Don't)
// Không tuân theo quy tắc đặt tên class của Java.
public class basecalculator {
}
```
Chỉ sử dụng Do/Don't khi đang giải thích một quy tắc coding/convention. Không bắt buộc sử dụng cho các nội dung lý thuyết không liên quan đến convention.
### 3.4. Comment giải thích
Khi đưa ví dụ code để minh họa một **coding convention**, phải có comment ngắn giải thích tại sao ví dụ đó đúng hoặc sai.
Nếu chỉ minh họa thuật toán hoặc logic chương trình, không bắt buộc thêm comment convention.
Đối với nội dung Java, nếu đang nói về coding convention thì ưu tiên **Oracle Java conventions**.
Đối với ngôn ngữ khác, sử dụng convention phù hợp với ngôn ngữ đó thay vì áp dụng Oracle Java Convention.
## 4. LaTeX
Khi nội dung chứa công thức toán học ký hiệu toán học hoặc ký tự đặc biệt cần LaTeX:
### Inline Math
Sử dụng single dollar:
```text
$H_0$
$\alpha$
$Z_0$
```
Ví dụ:
Chiều cao của cây là $h$.
### Display Math
Sử dụng double dollar cho công thức độc lập:
```text
$$
a^2 + b^2 = c^2
$$
```
Không đặt display equation trên cùng một dòng với văn bản.

## 5. Advanced Text Formatting
### 5.1. Đổi màu chữ
- Cú pháp: `<font color="#{colorCode}">context</font>`
- Sử dụng mã màu **Hexadecimal** (ví dụ: `<font color="#FF0000">text</font>`).
### 5.2. Chỉ số dưới (subscript)
- Cú pháp: `<sub>{context}</sub>` (ví dụ: `H<sub>2</sub>O`).
### 5.3. Chỉ số trên (superscript)
- Cú pháp: `<sup>{context}</sup>` (ví dụ: `m<sup>2</sup>`).
### 5.4. Highlight văn bản theo màu tuỳ chọn
- Cú pháp: `<mark style="background:#{colorCode}">{context}</mark>`
- Sử dụng mã màu **Hexadecimal** (ví dụ: `<mark style="background:#FFFF00">text</mark>`).

## 6. Links & Embeds
### 6.1. Sử dụng linh hoạt Wikilink
- `[[file.md]]` → **liên kết** đến file/note (chỉ tạo link dẫn tới file, không hiển thị nội dung).
- `![[file.md]]` → **nhúng (embed)** toàn bộ nội dung file đó vào note hiện tại.
- Agent tự quyết định dùng cái nào tuỳ ngữ cảnh:
  - Cần **tham chiếu nhanh** → dùng `[[...]]`.
  - Cần **hiển thị nội dung trực tiếp** ngay tại chỗ (ví dụ: nhúng bảng tham chiếu dùng chung nhiều nơi) → dùng `![[...]]`.
### 6.2. Link ra ngoài (external/markdown link)
- Cú pháp: `[Tên hiển thị](URL)`
  - `[...]` → text hiển thị cho người đọc.
  - `(...)` → địa chỉ đích (URL hoặc đường dẫn).

### 6.3. Block Reference
Cú pháp tổng quát:
`[[{fileMdName}#{target}|{displayText}]]`
với `{target} = {heading}` hoặc `^{blockId}`.

**a) Link đến 1 block cụ thể (không phải heading):**
- Tại block muốn được link tới, đặt `^{id}` ở cuối block đó để gán block ID.
- Từ file khác, link tới block đó bằng: `[[{fileMdName}#^{id}]]`
- Muốn hiển thị đẹp hơn (đổi tên hiển thị): `[[{fileMdName}#^{id}|{replaceContext}]]`

| Thành phần | Ý nghĩa |
|---|---|
| `{fileMdName}` | Tên file `.md` đích |
| `#` | Ký tự phân cách giữa tên file và vị trí bên trong file |
| `^{id}` | Block ID của block cần trỏ tới |
| `\|` | Ký tự phân cách giữa đích liên kết và tên hiển thị |
| `{replaceContext}` | Nội dung hiển thị thay cho tên file/block gốc |

**b) Link đến 1 Heading:**
- Cú pháp: `[[{fileMdName}#{target}]]`
- Muốn đẹp hơn (đổi tên hiển thị): `[[{fileMdName}#{heading}|{displayText}]]`

- **Ưu tiên dùng Block Reference** (thay vì chỉ link tới cả file hoặc chỉ tới heading) khi cần trỏ chính xác tới **1 đoạn/1 dòng cụ thể** trong file khác — tránh người đọc phải tự tìm trong toàn bộ file.

Ví dụ:
- Link đến Heading: `[[02 - Rules for working with Obsidian folders and notes#11. Bảng danh sách website đáng tin cậy|Danh sách website đáng tin cậy]]`
- Link đến Block: `[[02 - Rules for working with Obsidian folders and notes#^rule-20-80|Nguyên tắc 20/80]]`

## 7. Obsidian & Plugins
- Agent **được phép tự do sử dụng** mọi tính năng định dạng của Obsidian và các plugin đang có, miễn thông tin/tài liệu về tính năng đó đã có sẵn tại folder:
  `Obsidian-vault/02 - Obsidian context`
- **Không cần thông báo** trong nội dung file `.md` (hay bất kỳ đâu) là đã dùng tính năng gì hoặc plugin nào — áp dụng trực tiếp, tự nhiên như một phần định dạng bình thường của ghi chú.

## 8. Nguyên tắc ưu tiên
Khi áp dụng các quy tắc trên, ưu tiên theo thứ tự:
1. **Đúng nội dung và chính xác về mặt kỹ thuật.**
2. **Cấu trúc rõ ràng, dễ đọc.**
3. **Tương thích với Obsidian Live Preview và Reading Mode.**
4. **Sử dụng Markdown/Callout/LaTeX đúng mục đích.**
5. **Không lạm dụng formatting.**
Không thêm formatting chỉ để đáp ứng quy tắc nếu nó làm nội dung khó đọc hơn.