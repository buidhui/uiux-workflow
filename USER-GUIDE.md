# User Guide: UIUX-Workflow

Hướng dẫn thao tác cho Designer, đi từng bước một việc từ lúc PRD được duyệt tới lúc bàn giao. Phương pháp và lý do ở [README.md](README.md).

Ví dụ xuyên suốt: tính năng Chứng chỉ, ba màn. Danh sách chứng chỉ ghép từ bảng và bộ lọc có sẵn trong kit (L1). Chi tiết chứng chỉ cần một khối lịch sử cấp mà kit chưa có (L2). Trang chứng chỉ công khai để người học chia sẻ, cần gây ấn tượng (L3).

## Bước 0. Chuẩn bị, làm một lần

Mỗi mục dưới đây có nhiều cách làm; chọn cách phù hợp theo [SETUP.md](SETUP.md).

1. Công cụ AI: Claude Code (cách chính) hoặc công cụ AI khác đọc `AGENTS.md`. Mở đúng thư mục repo `uiux-workflow`; lệnh của quy trình chỉ có khi mở đúng thư mục này.
2. Kết nối Figma: một trong bốn lựa chọn ở `SETUP.md` mục 2, kể cả lựa chọn không kết nối và gửi ảnh.
3. Tài liệu của PO: repo có quyền push, repo chỉ đọc, hoặc không có repo (`SETUP.md` mục 3).
4. Product KB của sản phẩm ở mức Tối thiểu (`DOMAIN-SETUP.md`). Khi chưa có, lần đầu AI hỏi bù.
5. Kiểm tra theo `SETUP.md` mục 7. Với Claude Code, gõ `/` và thấy `/ux`, `/new-intent`.

## Bước 1. Tạo việc khi PRD đã duyệt

```
PRD tính năng Chứng chỉ đã duyệt, intent <đường dẫn intent của PO>.
Trang chứng chỉ công khai cần làm mới, ref đây: <link 1>, <link 2>.
```

Hoặc `/new-intent Chứng chỉ <đường dẫn>`. AI tạo việc và đọc PRD ngay.

## Bước 2. D1 Context Overview

AI trình tóm tắt tính năng, các vai, việc người dùng làm trên giao diện, phần wireframe của PO đã quyết định, các màn dự kiến và mức của từng màn, số lần duyệt dự kiến, câu hỏi cho PO kèm tin nhắn chép gửi được.

Designer sửa phần AI hiểu sai, gửi câu hỏi cho PO, sau đó phản hồi `Approved`. Câu hỏi chặn chưa có trả lời thì `Blocked`.

## Bước 3. D2 Design Strategy (Strategy Gate)

AI hỏi vài câu: modal hoặc trang riêng, màn phát sinh ngoài yêu cầu, mức của màn, màn nào AI dựng UI. Sau đó trình `design-strategy.md`:
- Danh sách màn gắn user story, mức thiết kế.
- Sơ đồ luồng, bảy state từng màn, trường hợp biên.
- Component của UI kit cho từng vùng; phần kit còn thiếu và cách xử lý tạm.
- Accessibility, màn cần sáng tạo, ý kiến về PRD, rủi ro và câu hỏi.

Luồng mới phức tạp: nói "làm flow prototype" để có bản khung xám thao tác thử, gửi kèm cho các bên.

Designer duyệt từng dòng của bảng duyệt, nhất là mức của từng màn và ý kiến về PRD. Phản hồi `Approved` hoặc `Need Revision`.

## Bước 4. D3 Alignment (Alignment Gate)

AI render chiến lược vào file thiết kế UX theo template của PO. Khi có quyền push vào repo của PO, AI cho Designer xem diff, commit khi Designer đồng ý, push khi Designer yêu cầu. Khi repo chỉ đọc hoặc không có repo, AI lưu file trong intent để Designer gửi PO.

Việc chuyển sang trạng thái chờ đồng thuận. Designer làm việc khác. Sau buổi họp hoặc khi PO báo:
```
PO họp xong rồi, làm tiếp.
```
AI pull repo PO, đọc kết quả. Có quyết định đổi thiết kế thì AI sửa chiến lược, đẩy lại. Các bên đã đồng ý và không còn chỉnh sửa thì Designer phản hồi `Approved`. Từ đây mới vẽ lên Figma.

## Bước 5. E1 UX Brief (chỉ khi có màn mở rộng hoặc sáng tạo)

- Màn sáng tạo: AI phân tích design ref, đưa hai đến ba hướng; Designer chọn một. Chưa có ref thì AI dừng lại và hỏi.
- Màn mở rộng: AI đề xuất cách làm phần kit chưa có; Designer chọn. AI chạy `/kit-proposal` để ghi đề xuất cho người phụ trách kit; màn dùng xử lý tạm trong lúc chờ.
- Mọi màn: thứ bậc thông tin, wireframe dạng khối, nội dung chữ, tương tác, state.

Phản hồi tại UX Brief Gate.

## Bước 6. E2 UI Design

Khi công cụ Figma có quyền ghi (`SETUP.md` mục 2), kit có hướng dẫn dùng và mức sẵn sàng cho phép, AI dựng màn L1, L2 bằng instance của kit:
1. AI lưu version Figma, sau đó dựng trong khu vực nháp; thiết kế chính không bị sửa.
2. Màn lớn thì AI trình kế hoạch chia đợt; Designer duyệt, xem ảnh chụp cuối mỗi đợt, góp ý thì AI sửa ngay.
3. Gặp phần kit chưa có: AI dùng xử lý tạm đã ghi và chạy `/kit-proposal`; không tự vẽ component.

Màn sáng tạo, mọi màn Designer muốn tự làm, và mọi màn khi công cụ Figma không có quyền ghi: Designer dựng trên Figma, dán link (hoặc ảnh với lựa chọn không kết nối) vào chat; AI đọc và tự kiểm.

## Bước 7. E3 Prototype

AI sinh prototype HTML một file từ màn trên Figma: thao tác được trọn luồng, có bảng điều khiển đổi vai, đổi bộ dữ liệu (rỗng, nhiều, chuỗi dài), ép state (đang tải, lỗi, không có quyền). Mở bằng trình duyệt. Muốn trình bày trên Figma thì nói "nối prototype trên Figma"; AI nối điều hướng giữa các frame.

## Bước 8. R1 Review & Refine (UI Gate)

Vòng 1: reviewer độc lập chấm điểm, chỉ lỗi kèm vị trí, số đo, cách sửa. Designer sửa lỗi bắt buộc.

Vòng 2: AI soạn tin nhắn mời BA, Dev, Reviewer góp ý kèm link Figma và cách mở prototype. Góp ý tới thì dán vào chat; AI gom vào feedback matrix. Dev nói khó làm thì AI đưa phương án kèm trade-off. Mỗi vòng sửa, AI lưu version Figma và cập nhật prototype.

Phản hồi `Approved` khi không còn góp ý bắt buộc. Sau đó Designer chuyển frame từ khu vực nháp sang page chính.

## Bước 9. H1 Handoff & Done (Delivery Gate)

AI ghi chú bàn giao cạnh frame trên Figma, cập nhật file thiết kế UX trên repo PO (link Figma từng màn, link prototype), viết `delivery-summary.md`, soạn nội dung chuyển task sang Done. Designer xem diff, gửi link cho Dev, cập nhật task, phản hồi `Approved`. AI hỏi một câu cuối: có gì cần nhớ cho lần sau.

Dev góp ý trong lúc làm: nói "Dev góp ý về chứng chỉ: ...". AI mở lại bước review cho màn đó.

## Tình huống ngoài luồng chuẩn

| Tình huống | Cách làm |
|---|---|
| PRD chưa được duyệt | Luồng bắt đầu từ PRD đã duyệt. Muốn đọc trước bản nháp thì tạo việc như thường; AI ghi mức hoàn thiện của PRD là Nháp. Khi bản đã duyệt đến, chạy `/change-request` cho phần khác biệt |
| CR trên màn có sẵn, mọi màn L1, logic thường | AI chạy D1 liền với D2, không dừng ở D1; bốn gate (`design-levels.md`) |
| Designer tự đề xuất cải tiến một màn đang chạy | Chạy `/ux-review --shadow` trên màn đó, sau đó `/new-intent` với file review làm đầu vào |
| Không có kết nối Figma | Gửi ảnh và link frame; AI làm mọi việc chỉ cần đọc, Designer làm phần ghi vào Figma (`SETUP.md` mục 2) |
| Sản phẩm chưa có UI kit | Designer dựng UI; AI vẫn làm chiến lược, prototype, review, bàn giao |
| PO đổi yêu cầu sau khi đã đồng thuận | Nói "PO đổi yêu cầu"; AI mở `/change-request`, chạy lại D3 cho phần đổi |
| Dev góp ý sau khi đã bàn giao | Nói "Dev góp ý về <tính năng>: ..."; AI mở lại R1 cho màn liên quan |
| Người xem prototype không có repo | Gửi file `index.html`; mở bằng trình duyệt, không cần cài đặt |
| Dùng công cụ AI khác Claude Code | Yêu cầu AI đọc `AGENTS.md`; review độc lập chạy ở một phiên riêng |

## Phản hồi tại các điểm duyệt

| Phản hồi | Khi nào |
|---|---|
| `Approved` | Đã ổn, đi tiếp. Trả lời "ok" hoặc "duyệt" được hiểu là Approved |
| `Approved with Notes:` kèm ghi chú | Cơ bản ổn, cần lưu ý ở bước sau |
| `Need Revision:` kèm điểm cần sửa | Chưa đạt |
| `Blocked:` kèm câu hỏi | Chờ PO, Dev, QA trả lời |

## Việc nhỏ, không cần tạo việc

Sửa chữ vài nút, góp ý nhanh một màn, hỏi cách dùng component: hỏi trực tiếp, AI thực hiện ngay. Review một màn đang chạy: `/ux-review --shadow <link Figma hoặc ảnh>`. Kit thiếu một component: `/kit-proposal <mô tả>`.

## Dừng giữa chừng

Nói "dừng hôm nay". Hôm sau nói "làm tiếp" hoặc `/ux`. Xem mọi việc: "tới đâu rồi" hoặc `/ux-status`.

## Lỗi thường gặp

| Hiện tượng | Nói với AI |
|---|---|
| AI hiểu sai PRD | "Đọc lại PRD, tách Confirmed, Assumption, Open question, không tự suy luận" |
| AI tự mở rộng phạm vi | "Chỉ làm trong chiến lược đã đồng thuận, đề xuất thêm đưa vào Nice-to-have" |
| Thiếu state | "Kiểm lại bảy state cho từng màn" |
| UI lệch kit | "Đối chiếu kit, chỉ ra component nào lệch, thay bằng component có sẵn" |
| Prototype lệch Figma | "Cập nhật prototype theo bản Figma mới nhất" |
| AI gán sai mức của màn | "Màn này dùng component có sẵn" hoặc "màn này cần làm mới" |
