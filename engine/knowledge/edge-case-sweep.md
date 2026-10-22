---
status: chưa viết
---
# Rà edge case

Dùng ở D2, bước rà trường hợp biên.

## Nội dung dự kiến
- Năm câu cấp flow: huỷ giữa chừng, phụ thuộc chưa sẵn sàng, lặp thao tác, dữ liệu đổi giữa các bước, phiên hết hạn
- Năm nhóm cấp màn: nhập liệu, quyền, hệ thống và mạng, giới hạn dữ liệu, thao tác không hoàn tác; câu hỏi cụ thể cho từng nhóm
- Tiêu chí thao tác không hoàn tác: không thu hồi được, không chỉ là mất dữ liệu
- Mức Must, Should, Optional và cách xếp
- Đặc tả hành vi bốn phần: khởi động, luật, phản hồi, lặp hoặc chế độ
- Cách thể hiện hành động bị chặn theo quyền: ẩn, vô hiệu kèm giải thích, chỉ xem; tiêu chí chọn

## Nguồn để chuyển
- `vic-screen-discovery/references/edgecase.md`
- `uiux-edgecase-permission-detector/SKILL.md` các bước 1 đến 8

## Sửa khi chuyển
- Bỏ con số "mất 60% case" của bộ gốc: không có nguồn
- Bỏ tên component VIC trong phần xác nhận xoá; thay bằng "hộp thoại xác nhận chặn luồng" và trỏ về design system của domain
