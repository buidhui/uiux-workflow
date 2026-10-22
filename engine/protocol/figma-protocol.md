# Figma Protocol

Luật thao tác Figma cho mọi stage ghi vào Figma (E1 khi vẽ wireframe, E2, E3 khi nối prototype, R1 khi sửa theo góp ý, H1 khi ghi chú bàn giao) và mọi bước đọc số liệu (E3, R1, `/ux-review`). Luồng không tạo hoặc sửa component trong UI kit; phần kit thiếu chuyển sang `/kit-proposal`. Không phụ thuộc design system cụ thể; dữ kiện của design system nằm ở Product KB mục 5, 6.

## 0. Công cụ kết nối

Engine không gắn với một công cụ Figma. `USER-GUIDE.md` mục A3 mô tả bốn lựa chọn: A connector Figma của claude.ai, B Figma Dev Mode MCP trên máy, C figma-console MCP với plugin Desktop Bridge, D không kết nối. Lựa chọn đang dùng trên máy và kết quả kiểm khả năng ghi ở `.uiux/setup.md` (do `/setup` ghi, không đưa lên git).

Trước việc đầu tiên cần Figma trong một phiên: kiểm công cụ nào đang kết nối, việc cần làm đòi khả năng nào (đọc, chụp ảnh, ghi), và đối chiếu bảng khả năng ở `USER-GUIDE.md` mục A3. Công cụ hiện có không đủ thì dùng cách thay thế ở bảng "Lựa chọn nào cho stage nào" và báo Designer một dòng. Không giả định một khả năng chưa được kiểm; khả năng ghi "Kiểm khi cài" thì thử một lần trên khu vực nháp, ghi kết quả vào `.uiux/setup.md`.

Tài liệu này gọi thao tác theo tên chung: "đọc design context", "chụp ảnh frame", "chạy lệnh ghi qua Plugin API", "tìm component trong thư viện". Mỗi lựa chọn có tên công cụ riêng cho cùng thao tác.

## 1. Mức sẵn sàng design system

| Mức | Điều kiện | Được làm |
|---|---|---|
| 0 | Chưa có design system viết ra; quy ước nằm trong code hoặc trong đầu người | Đọc Figma để review. Không dựng màn |
| 1 | Product KB có luật design system và danh mục component của kit đã duyệt (trỏ tới nguồn hoặc viết trong KB); thư viện Figma chưa có biến kèm mô tả, hoặc AI không đọc được thư viện | E2 ở chế độ frame thường: dựng theo spec trong Product KB, đặt tên node theo chức năng để sau đổi sang instance; ghi Limitation "không liên kết thư viện" |
| 2 | Thư viện Figma có biến và component kèm mô tả chuẩn hoá theo bộ khoá ở `design-system.md` mục 1, AI đọc được qua MCP | E2 chỉ dùng instance của UI kit |

Mức hiện tại ghi ở KB mục 5. Command kiểm mức này ở bước Load, không tự nâng mức.

## 2. Trước khi ghi
- File đích ghi trong `intent.md` hoặc `domain.md`. Không ghi vào file nào khác.
- Mỗi script ghi bắt đầu bằng guard: tên file đang mở khác file đích thì dừng, không ghi.
- Đọc trước, ghi sau. Thông tin component, biến, text style lấy từ Figma thật và từ mô tả trên Figma; bảng trong Product KB chỉ là chỉ mục. Hai bên lệch thì tin Figma, dừng và báo lệch.
- Kiểm phần việc chưa hoàn tất: frame có đánh dấu `generated-by: uiux-workflow` so với `build-report.md`; lệch nghĩa là Designer đã sửa tay, đọc lại trước khi đụng.

## 3. Chỗ ghi an toàn
- AI không ghi lên page thiết kế chính. Mọi lần ghi vào page hoặc section nháp tên theo KB mục 6 (mặc định `AI Draft / <intent>`), hoặc vào branch của file khi gói Figma có branching. Designer chuyển frame sang page chính sau UI Gate. Ghi chú bàn giao ở H1 là ngoại lệ: được ghi cạnh frame đã ở page chính, không sửa frame.
- Trước đợt ghi đầu tiên của intent và trước mỗi đợt sửa lớn: lưu một version có tên trong lịch sử file (`figma.saveVersionHistoryAsync`, tên `uiux-workflow <intent> <stage> trước khi ghi`). Sau mỗi vòng sửa theo góp ý ở R1: lưu version có mô tả là các dòng feedback đã xử lý, làm change log trên Figma. Không lưu được qua MCP thì nhắc Designer tự lưu, chờ xác nhận, sau đó mới ghi.
- Sửa màn đang chạy theo CR: nhân bản frame gốc sang khu vực nháp, sau đó sửa bản nhân, không sửa trực tiếp frame gốc.

## 4. Ưu tiên thành phần có sẵn
- Mọi phần tử trên màn là instance từ thư viện của domain. Icon là instance icon của thư viện. Không vẽ lại, không detach, kể cả để đổi màu.
- Component có vùng chứa nội dung (slot) thì đổ nội dung vào đó, không tự dựng khung.
- Không dùng component mà Product KB ghi là bỏ không dùng nữa.
- Đọc khoảng trống (`GAPS`) trong mô tả component trước khi chọn variant. Không giả định variant không tồn tại.

## 5. Khi thư viện thiếu
1. Tìm: công cụ tìm component trong thư viện với nhiều từ khoá đồng nghĩa, mỗi lần một từ; đi qua instance của màn liền kề (component lồng trong instance phải duyệt đệ quy `children`); design system gốc và thư viện khác ghi trong KB mục 5.
2. Vẫn thiếu: dừng. Báo Designer thiếu gì, đã tìm ở đâu, hai lựa chọn: cấp quyền hoặc thư viện để lấy component thật, hoặc cho phép dựng frame thường.
3. Chỉ khi được phép mới dựng frame thường, tên bắt đầu bằng `~`, đặt tên theo chức năng, ruột ghép từ instance thư viện. Ghi vào build-report mục Promote candidates và vào gap log của sản phẩm (KB mục 5); muốn đưa vào kit thì `/kit-proposal`.
4. Không tạo `COMPONENT` hoặc `COMPONENT_SET`. Luật này áp cả cho khung app, sidebar, header, dòng bảng. Cần component mới thì `/kit-proposal`.

## 6. Khi ghi
- Gán biến ngay lúc tạo node, không tạo giá trị thô, sau đó gán sau. Không mã màu rời, không biến nguyên thuỷ (primitive) khi domain có lớp biến ngữ nghĩa.
- Chữ đi qua text style của domain, không đặt font rời.
- Khoảng cách theo thang của domain; giá trị lẻ thì lấy bậc gần nhất, không giữ số thô tạm thời.
- State màu dùng trọn bộ cùng một mức nhấn; không có biến cho một state thì không đổi màu ở state đó.
- Mode (breakpoint, màu sáng tối) đặt rõ trên frame theo scope. Domain chưa có mode được yêu cầu thì ghi `GAP`, hỏi Designer.
- Mỗi batch tối đa 50 node. Ghi node ID sau mỗi batch. Timeout thì kiểm phần đã chạy, chỉ chạy phần thiếu; lặp lại thì giảm nửa batch.
- Không xoá, không đè node có sẵn. Sửa nhầm thì làm thao tác ngược và báo.
- Đánh dấu frame do AI dựng: pluginData `generated-by: uiux-workflow`, intent, stage, ngày.

## 7. Kiểm và báo
- Kiểm bằng số đo và ảnh chụp từng section, đối chiếu ngược về `design-strategy.md`.
- Cùng một lỗi sửa hỏng hai lần thì dừng, báo Designer. Không thử cách thứ ba.
- Không báo xong dựa trên số lệnh đã gửi; chỉ dựa trên kết quả đã kiểm.
- Không nói "đã chạy thử prototype"; MCP ghi được tương tác nhưng không chạy thử được.
- Báo cáo tách rõ phần nào là instance thư viện, phần nào là frame tự dựng, kèm lý do.

## 8. Lỗi kết nối
Kết nối MCP lỗi: dừng, kiểm trạng thái thật, báo việc đã làm và chưa làm, sau đó mới làm tiếp. Cách khắc phục theo từng lựa chọn ở `USER-GUIDE.md` mục A3; chạy `/setup` để kiểm lại kết nối. Không khắc phục được thì chuyển sang cách thay thế của stage và ghi vào Limitation.
