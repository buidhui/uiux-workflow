---
description: Chiến lược đã đồng thuận ở D3 phải đổi: phân loại, chụp bản cũ, quay lại đúng stage, đẩy lại lên repo PO
argument-hint: <intent-slug> [mô tả thay đổi hoặc đường dẫn tài liệu mới]
---
# /change-request

Dùng khi chiến lược thiết kế đã đồng thuận ở D3 phải đổi: PO đổi yêu cầu, PRD đến sau bản nháp, hoặc Designer thấy scope đã ký cần đổi. Góp ý lên thiết kế mà không đổi phạm vi (đổi vị trí, cách hiển thị, chỉnh cho khả thi) được đưa vào feedback matrix của R1, không mở CR. Không sửa tay artifact đã duyệt.

## 1. Ghi nhận
- Ghi nguyên văn thay đổi vào `inputs/change-<YYYYMMDD>.md`. Có tài liệu mới thì so với bản cũ, liệt kê điểm khác.
- Cấp mã `CR<n>` trong `decisions.md`.

## 2. Phân loại

| Loại | Dấu hiệu | Quay lại |
|---|---|---|
| Nội dung | Đổi chữ, nhãn, thứ tự hiển thị trên màn đã có trong phạm vi | D2: thêm dòng vào design-strategy, sau đó sửa UI ở R1 |
| Màn | Thêm, bỏ, tách, gộp màn; đổi modal sang page; đổi mức thiết kế của màn | D2 cho màn bị chạm, sau đó E1 nếu màn mới là L2, L3 |
| Flow | Đổi flow chính, thêm vai, thêm thao tác không hoàn tác | D1 cho phần đổi, sau đó đi tiếp như thường |

Nghi ngờ giữa hai loại thì chọn loại quay lại sớm hơn. Hỏi Designer xác nhận loại.

## 3. Thực hiện
- Chụp artifact sẽ đổi vào `archive/` với hậu tố `-pre-CR<n>`.
- Đặt stage quay lại về `[R]`, stage sau nó về `[ ]` nếu bị ảnh hưởng. UI đã dựng thì ghi rõ màn nào phải dựng lại, màn nào giữ.
- Chỉ sửa phần bị chạm, không viết lại toàn bộ.
- Đi qua gate như thường. DEC ghi rõ CR nào.
- Thay đổi chạm phần đã đẩy lên repo PO (danh sách màn, luồng, thành phần, ý kiến PRD): chạy lại D3 cho phần đổi; thay đổi nhỏ chỉ cần PO xác nhận.
