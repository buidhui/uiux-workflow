---
description: Stage D3 Alignment. Đẩy chiến lược thiết kế lên repo của PO theo template của họ, chờ các bên đồng thuận, đồng bộ thay đổi. Alignment Gate: chỉ khi các bên đã OK mới vẽ lên Figma. Gọi qua /ux
argument-hint: <intent-slug>
---
# D3 Alignment

| | |
|---|---|
| Stage | D3 Alignment |
| Slug | alignment |
| Phase | discovery |
| Execution | always |
| Produces | file thiết kế UX trên repo của PO (theo KB mục 2) · `discovery/alignment/alignment-log.md` |
| Consumes | `design-strategy.md` đã duyệt (bắt buộc) · `flow-prototype.html` nếu có · tài liệu đồng thuận của PO (ví dụ Decision Brief) và `decisions.md` của intent PO, chỉ đọc |
| Requires | design-strategy |
| Áp dụng | Cả intent |
| Reviewer | none, các bên là người duyệt |
| Archive | yes, cho bản đã đẩy lên |
| Template | template file thiết kế UX của PO, đường dẫn ở KB mục 2; không có thì `engine/templates/design-strategy.md` mục 1 đến 7 |
| Checklist | `engine/verification/alignment.md` |
| Knowledge | KB mục 2: repo của PO, đường dẫn intent, template, quy ước commit, cách đồng thuận |

Chạy theo `engine/protocol/stage-protocol.md`.

## Mục đích
Chiến lược thiết kế được các bên đọc và đồng thuận trước khi Designer đầu tư vào Figma. Điểm lệch giữa yêu cầu và thiết kế lộ ra ở đây, khi sửa còn ít tốn công. Đây là điểm duy nhất bên ngoài tham gia đồng thuận ở cấp định hướng; phần chi tiết sau đó do Designer quyết định.

## 1. Đẩy lên repo của PO
Cách làm theo KB mục 2, một trong ba trường hợp ở `USER-GUIDE.md` mục A4:
- Repo có quyền push: các bước dưới đây.
- Repo chỉ đọc: làm bước 1 đến 3, lưu file vào `discovery/alignment/`; Designer gửi PO hoặc mở pull request theo quy ước.
- Không có repo: render theo template của PO nếu có, không có thì theo `design-strategy.md` mục 1 đến 7; lưu vào `discovery/alignment/`; Designer đưa lên nơi PO dùng.

1. Tìm intent của PO theo `intent.md` mục Nguồn yêu cầu. Pull repo của PO trước khi sửa.
2. Render nội dung từ `design-strategy.md` sang template file thiết kế UX của PO, giữ đúng heading và frontmatter của họ, trỏ về mã trong PRD. Chỉ đưa phần các bên cần đọc: danh sách màn, luồng và tương tác, thành phần giao diện và component cần bổ sung, accessibility, ý kiến về PRD, rủi ro và câu hỏi. Không đưa bảng duyệt nội bộ, thẻ nguồn, ghi chú quy trình.
3. Flow prototype nếu có: đặt cạnh file theo KB mục 2, hoặc ghi link.
4. Chỉ sửa file thiết kế UX của Designer trên repo PO. Không sửa PRD, không sửa file của team khác.
5. Trình Designer diff trước khi commit. Commit theo quy ước ở KB mục 2 (ví dụ `design(<intent>): ux`). Push chỉ khi Designer yêu cầu.
6. Ghi vào `alignment-log.md`: version đẩy lên, commit, ngày, link.

## 2. Chờ đồng thuận
Ghi Parked, lý do "chờ đồng thuận chiến lược thiết kế", hạn theo lịch họp nếu có. Designer làm việc khác trong lúc chờ.

## 3. Đồng bộ khi có phản hồi
Khi Designer gọi `/ux`: pull repo PO, đọc tài liệu đồng thuận và quyết định liên quan tới thiết kế.
- Quyết định làm đổi thiết kế: sửa `design-strategy.md` (tăng version), render lại, đẩy lại, ghi log. Không cần quay lại D2 trừ khi đổi flow chính hoặc danh sách màn.
- Quyết định làm đổi PRD: chờ PO sửa PRD theo quy trình của họ, đọc bản mới, sau đó cập nhật chiến lược.
- Câu hỏi của Designer được trả lời: ghi vào `decisions.md` mục Câu trả lời.

## Gate
Alignment Gate. Qua khi các bên đã đồng thuận và không còn chỉnh sửa: theo KB mục 2, ví dụ tài liệu đồng thuận của PO đã được duyệt và Designer đã ký. Việc nhỏ mà PO không có buổi đồng thuận: PO xác nhận đã đọc, Designer dán nguyên văn vào `decisions.md`. Designer xác nhận lần cuối bằng Approved.
Sau Approved: phạm vi thiết kế cố định; thay đổi về sau chuyển sang `/change-request`. Stage kế: E1 nếu có màn L2, L3; không thì E2.
