# Question Format

Cách hỏi và ghi câu trả lời của Designer. File câu hỏi là nguồn sự thật: mọi câu trả lời, dù Designer nói trong chat hoặc sửa file, cuối cùng đều nằm trong file.

## File
`<thư mục stage>/<slug>-questions.md`, tạo từ `engine/templates/questions.md`.

## Hai loại câu hỏi

| Loại | Ai trả lời | Ghi ở đâu |
|---|---|---|
| Quyết định thiết kế: modal hoặc page, màn mới hoặc sửa màn cũ, state nào làm ở đợt này, ưu tiên | Designer | Questions file của stage |
| Nghiệp vụ: rule, quyền, dữ liệu, điều kiện mà tài liệu không nói | BA, PO | Mục "Câu hỏi cho BA, PO" trong artifact, mã `OQ-NN`, gắn `❓PO`. Designer chuyển đi |

Không hỏi Designer quyết định thay BA, PO một rule nghiệp vụ. Không hỏi BA, PO một quyết định thiết kế.

## Quy tắc đặt câu hỏi
- Chỉ hỏi câu mà đáp án làm đổi danh sách màn, flow, state, hành vi, hoặc nội dung hiển thị.
- Tra tài liệu yêu cầu, app-map, `decisions.md` trước. Đã có đáp án thì không hỏi.
- Mỗi câu tự giải thích. Mã nào xuất hiện thì kèm nội dung.
- Tối đa bốn lựa chọn mỗi câu, vì hộp chọn chỉ hiện bốn và tự thêm lối "Khác". Khi không chắc có lựa chọn nào hợp, một trong bốn là "Chưa xác định".
- `[đề xuất]` là đáp án AI thấy hợp lý nhất, kèm nguồn: pattern màn liền kề, app-map, luật design system, chuẩn ngành.
- Chặn: có khi thiếu đáp án thì không viết được artifact đúng.
- Hỏi theo lô tối đa bốn câu. Câu chặn hỏi trước.

## Cách trả lời
Mặc định hỏi bằng hộp chọn AskUserQuestion, mỗi câu có lối "Khác" để nói bằng lời. Không hỏi Designer chọn cách trả lời ở đầu intent. Designer muốn trả lời trong chat, gửi ảnh, hoặc tự điền file thì làm theo; AI trích quyết định, ghi vào đúng câu, trình lại để Designer xác nhận.

## Câu hỏi cho BA, PO, dạng dán thẳng
Mục "Câu hỏi cho BA, PO" của artifact kết thúc bằng một khối tin nhắn Designer chép gửi BA, PO được ngay: một dòng ngữ cảnh (tính năng, màn), các câu đánh số, mỗi câu có lựa chọn gợi ý nếu có, câu chặn đứng trước, hạn cần trả lời. Có câu trả lời thì dán nguyên văn vào `decisions.md` mục Câu trả lời của BA, PO.

## Ghi câu trả lời
- Nguyên văn lời Designer sau `[Answer]:`, kể cả khi chọn bằng chữ cái: `A, "<lời nói thêm>"`.
- Diễn giải của AI, nếu cần, dòng dưới: `Hiểu là: ...`.
- Designer uỷ quyền ("tuỳ em"): chọn theo `[đề xuất]`, ghi `[uỷ quyền]` kèm nguyên văn, nói một dòng đã chọn gì.
- Không bao giờ tự điền `[Answer]:` khi Designer chưa nói.

## Soát sau khi có câu trả lời
- Từ mơ hồ: "tuỳ", "chắc là", "cả hai". Hỏi lại cho tới khi rõ.
- Mâu thuẫn giữa các câu, hoặc với `decisions.md`: trình hai câu cạnh nhau, hỏi một câu để thống nhất.

## Thẻ nguồn trong artifact nội bộ

| Thẻ | Nghĩa |
|---|---|
| `[req:<mã>]` | Tài liệu yêu cầu của PO, kèm mã gốc nếu có: `[req:US3]`, `[req:PRD §4.2]` |
| `[Q3]` | Câu trả lời số 3 của stage này. Stage khác ghi `[D1 Q3]` |
| `[app-map:<file>]` | App-map của domain |
| `[figma:<node>]` | Đọc trực tiếp trên Figma |
| `[ds:<mục>]` | Luật design system của domain |
| `[DEC5]` | Quyết định đã ghi |
| `[assumption]` | Giả định, chưa xác nhận |
| `[suy ra]` | AI suy luận từ nguồn |

Mỗi khối khẳng định trong artifact nội bộ có ít nhất một thẻ. Không nâng assumption thành fact ở stage sau khi Designer, BA hoặc PO chưa xác nhận.
