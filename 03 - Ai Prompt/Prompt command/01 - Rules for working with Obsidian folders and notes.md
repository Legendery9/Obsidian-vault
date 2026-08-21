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

---

## 10. Quy tắc nguồn tham khảo
- **Header nguồn tham khảo đầu mỗi file `.md`**:
    - Tại đầu mỗi file `.md`, tạo một header riêng chứa các Markdown link `[Tên hiển thị](URL)` đến những website đã thực sự được dùng làm tài nguyên, dữ liệu, thông tin hoặc nguồn tham khảo khi viết nội dung file đó.
    - Chỉ thêm website thực sự được sử dụng trong nội dung — không thêm cho có, không thêm hàng loạt link "liên quan chủ đề" nếu không thực sự dùng để lấy thông tin.
    - Nếu phải chọn giữa nhiều nguồn cùng cung cấp thông tin đã dùng → ưu tiên ghi nguồn chính thống, uy tín nhất (official docs trước, nguồn tổng hợp/cộng đồng sau).
    - Nếu file không sử dụng tài nguyên từ website bên ngoài nào (Ví dụ: nội dung tự viết dựa trên kiến thức đã có sẵn trong vault, hoặc chỉ tổng hợp từ file khác) → không cần thêm header này.
    - Header nguồn tham khảo phải nằm trước nội dung chính của file (trước mọi heading `##` nội dung).
- **Áp dụng cho các file đã tạo trước đó (không bắt buộc gấp)**:
    - Với các file `.md` đã tạo ở các phiên trước: nếu nội dung trong đó thực sự đã dựa trên/tham khảo một nguồn cụ thể (dù không ghi rõ lúc viết) → bổ sung header nguồn khi rà soát lại folder đó.
    - Không cần chủ động thêm link "cho đủ" nếu không chắc chắn nội dung trước đó có thực sự tham khảo nguồn nào — tuân đúng nguyên tắc "chỉ ghi nguồn thực sự dùng" ở trên.
- **Ghi log**:
    - Thực hiện đúng theo quy tắc ghi log đã nêu tại file rules: cập nhật `implementation.md` tương ứng của folder đang xử lý khi áp dụng quy tắc header nguồn tham khảo cho file mới hoặc file rà soát lại.

---

## 11. Bảng danh sách website đáng tin cậy
Dùng làm nguồn tra cứu ưu tiên cho người dùng, người đọc, và AI khi cần chọn nguồn tham khảo cho header ở mục 10 (không bắt buộc chỉ được dùng nguồn trong danh sách này — đây là danh sách gợi ý/ưu tiên, có thể dùng nguồn uy tín khác nếu phù hợp hơn với nội dung thực tế đã dùng).

### Lập trình / IT
| Website | Mô tả |
| :--- | :--- |
| [Oracle Java Documentation](https://docs.oracle.com/en/java/) | Tài liệu chính thức về Java |
| [MDN Web Docs](https://developer.mozilla.org/) | Tài liệu HTML, CSS, JavaScript và Web API |
| [Spring Documentation](https://docs.spring.io/) | Tài liệu chính thức về Spring và Spring Boot |
| [Microsoft Learn](https://learn.microsoft.com/) | Tài liệu C#, .NET, Azure, SQL Server, Windows... |
| [Git Documentation](https://git-scm.com/doc) | Tài liệu chính thức về Git |
| [Docker Docs](https://docs.docker.com/) | Tài liệu về Docker |
| [Linux Documentation](https://www.kernel.org/doc/) | Tài liệu về Linux và Linux Kernel |
| [PostgreSQL Documentation](https://www.postgresql.org/docs/) | Tài liệu chính thức về PostgreSQL |
| [MySQL Documentation](https://dev.mysql.com/doc/) | Tài liệu chính thức về MySQL |
| [Python Documentation](https://docs.python.org/) | Tài liệu chính thức về Python |
| [Stack Overflow](https://stackoverflow.com/) | Hỏi đáp lập trình |
| [GeeksforGeeks](https://www.geeksforgeeks.org/) | Thuật toán, cấu trúc dữ liệu, Java, C++, Python, CS |
| [Baeldung](https://www.baeldung.com/) | Java, Spring, Spring Boot, Hibernate |
| [W3Schools](https://www.w3schools.com/) | HTML, CSS, JavaScript, SQL, Java, Python |
| [freeCodeCamp](https://www.freecodecamp.org/) | Học lập trình qua bài học/thực hành |
| [Dev.to](https://dev.to/) | Bài viết, kinh nghiệm cộng đồng developer |

### Tra cứu kiến thức tổng quát
| Website | Mô tả |
| :--- | :--- |
| [Wikipedia](https://www.wikipedia.org/) | Tra cứu nhanh, tổng quan nhiều chủ đề |
| [Britannica](https://www.britannica.com/) | Kiến thức bách khoa |
| [Our World in Data](https://ourworldindata.org/) | Dữ liệu xã hội, kinh tế, môi trường, toàn cầu |
| [Google](https://www.google.com/) | Công cụ tìm kiếm |
| [Internet Archive](https://archive.org/) | Lưu trữ sách, tài liệu, website |

### Nghiên cứu khoa học / Academic
| Website | Mô tả |
| :--- | :--- |
| [Google Scholar](https://scholar.google.com/) | Bài báo, luận văn, sách, tài liệu học thuật |
| [Semantic Scholar](https://www.semanticscholar.org/) | Tìm kiếm nghiên cứu khoa học |
| [PubMed](https://pubmed.ncbi.nlm.nih.gov/) | Nghiên cứu y học, khoa học sự sống |
| [JSTOR](https://www.jstor.org/) | Tạp chí, sách, khoa học xã hội và nhân văn |
| [ScienceDirect](https://www.sciencedirect.com/) | Bài báo, nghiên cứu khoa học/kỹ thuật |
| [IEEE Xplore](https://ieeexplore.ieee.org/) | CS, Engineering, Technology, Electronics |
| [ACM Digital Library](https://dl.acm.org/) | Nghiên cứu, tài liệu Computer Science |
| [Springer Nature](https://link.springer.com/) | Sách, bài báo, nghiên cứu khoa học |
| [arXiv](https://arxiv.org/) | Preprint CS, Mathematics, Physics... |
| [DOAJ](https://doaj.org/) | Tạp chí khoa học truy cập mở |
| [CORE](https://core.ac.uk/) | Nghiên cứu khoa học truy cập mở |

### Toán / Statistics
| Website | Mô tả |
| :--- | :--- |
| [Wolfram MathWorld](https://mathworld.wolfram.com/) | Từ điển, tài liệu tham khảo toán học |
| [WolframAlpha](https://www.wolframalpha.com/) | Tính toán, giải toán, phân tích dữ liệu |
| [Desmos](https://www.desmos.com/) | Vẽ, tương tác đồ thị toán học |
| [GeoGebra](https://www.geogebra.org/) | Hình học, đại số, calculus |
| [Statlect](https://www.statlect.com/) | Probability và Statistics |

### Database / SQL
| Website | Mô tả |
| :--- | :--- |
| [SQL Server Documentation](https://learn.microsoft.com/en-us/sql/) | Tài liệu chính thức Microsoft SQL Server |
| [PostgreSQL Documentation](https://www.postgresql.org/docs/) | Tài liệu chính thức PostgreSQL |
| [MySQL Documentation](https://dev.mysql.com/doc/) | Tài liệu chính thức MySQL |
| [Oracle Database Documentation](https://docs.oracle.com/en/database/) | Tài liệu chính thức Oracle Database |
| [SQLBolt](https://sqlbolt.com/) | Học SQL qua bài tập tương tác |
| [Mode SQL Tutorial](https://mode.com/sql-tutorial/) | Học SQL kết hợp phân tích dữ liệu |

### Computer Science / Algorithms
| Website | Mô tả |
| :--- | :--- |
| [VisuAlgo](https://visualgo.net/) | Trực quan hoá cấu trúc dữ liệu, thuật toán |
| [CP-Algorithms](https://cp-algorithms.com/) | Thuật toán, Competitive Programming |
| [GeeksforGeeks](https://www.geeksforgeeks.org/) | Cấu trúc dữ liệu, thuật toán, CS |
| [LeetCode](https://leetcode.com/) | Luyện thuật toán, coding interview |
| [HackerRank](https://www.hackerrank.com/) | Bài tập lập trình, kiểm tra kỹ năng |
| [Codeforces](https://codeforces.com/) | Competitive Programming |
| [Big-O Cheat Sheet](https://www.bigocheatsheet.com/) | Tra cứu Big-O, độ phức tạp thuật toán |

### Tin tức / Thông tin thời sự
| Website | Mô tả |
| :--- | :--- |
| [Reuters](https://www.reuters.com/) | Tin tức quốc tế |
| [BBC](https://www.bbc.com/) | Tin tức quốc tế |
| [AP News](https://apnews.com/) | Tin tức quốc tế |
| [VnExpress](https://vnexpress.net/) | Tin tức Việt Nam và quốc tế |
| [VietnamPlus](https://www.vietnamplus.vn/) | Tin tức Việt Nam và quốc tế |
| [Cổng thông tin điện tử Chính phủ](https://chinhphu.vn/) | Văn bản chính thức Chính phủ Việt Nam |

### Dữ liệu / Statistics / Economics
| Website | Mô tả |
| :--- | :--- |
| [Our World in Data](https://ourworldindata.org/) | Dữ liệu toàn cầu xã hội, kinh tế, môi trường, sức khỏe |
| [World Bank Data](https://data.worldbank.org/) | Dữ liệu kinh tế, phát triển toàn cầu |
| [UN Data](https://data.un.org/) | Dữ liệu Liên Hợp Quốc |
| [WHO Data](https://data.who.int/) | Dữ liệu y tế, sức khỏe toàn cầu |
| [IMF Data](https://www.imf.org/en/Data) | Dữ liệu kinh tế, tài chính |
| [OECD Data Explorer](https://data-explorer.oecd.org/) | Dữ liệu kinh tế, xã hội, phát triển |
| [Statista](https://www.statista.com/) | Thống kê, dữ liệu thị trường |

### Sách / Tài liệu
| Website | Mô tả |
| :--- | :--- |
| [Google Books](https://books.google.com/) | Tìm kiếm, xem thông tin sách |
| [Internet Archive](https://archive.org/) | Sách, tài liệu lưu trữ |
| [Project Gutenberg](https://www.gutenberg.org/) | Sách điện tử public domain |
| [OpenStax](https://openstax.org/) | Giáo trình đại học miễn phí, OER |
| [Open Library](https://openlibrary.org/) | Thư viện sách trực tuyến |

### GitHub / Open Source
| Website | Mô tả |
| :--- | :--- |
| [GitHub](https://github.com/) | Source code, Git repository, Open Source |
| [GitLab](https://gitlab.com/) | Git repository, CI/CD, DevOps |
| [Apache Software Foundation](https://www.apache.org/) | Dự án Open Source thuộc Apache |
| [Maven Central](https://central.sonatype.com/) | Kho Java packages/dependencies |
| [npm](https://www.npmjs.com/) | Kho JavaScript packages |
| [PyPI](https://pypi.org/) | Kho Python packages |

### Video / Visual Learning
| Website | Mô tả |
| :--- | :--- |
| [YouTube](https://www.youtube.com/) | Video học tập, tutorial, bài giảng |
| [3Blue1Brown](https://www.3blue1brown.com/) | Toán học trực quan hoá |
| [Computerphile](https://www.youtube.com/@Computerphile) | Computer Science, công nghệ |
| [TED-Ed](https://ed.ted.com/) | Bài học trực quan nhiều chủ đề |

### Nguồn tin chính thức / Primary Sources
| Website | Mô tả |
| :--- | :--- |
| [United Nations](https://www.un.org/) | Thông tin, tài liệu chính thức Liên Hợp Quốc |
| [World Bank](https://www.worldbank.org/) | Thông tin, dữ liệu kinh tế, phát triển |
| [WHO](https://www.who.int/) | Thông tin chính thức y tế, sức khỏe |
| [IMF](https://www.imf.org/) | Thông tin kinh tế, tài chính quốc tế |
| [OECD](https://www.oecd.org/) | Dữ liệu, nghiên cứu, chính sách kinh tế - xã hội |

---

> [!important]  
> Các quy tắc này tiếp tục được áp dụng trong các phiên làm việc sau **cho đến khi người dùng trực tiếp yêu cầu thay đổi hoặc hủy bỏ**.