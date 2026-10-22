---
status: chưa viết
---
# Accessibility

Dùng ở E2 (tự kiểm) và R1 (trục Accessibility). Nền: WCAG 2.2 mức AA.

## Nội dung dự kiến
- Tương phản: chữ thường từ 4.5:1, chữ lớn và thành phần không phải chữ từ 3:1; tính từ giá trị thật của biến, không ước lượng từ ảnh
- Vùng chạm: mức AA là 24 x 24 px (WCAG 2.2, tiêu chí 2.5.8). 44 x 44 px là mức AAA (tiêu chí 2.5.5) và là khuyến nghị của nền tảng di động; domain chọn ngưỡng nào thì ghi ở `design-system.md`
- Focus nhìn thấy được ở mọi phần tử tương tác
- Nút chỉ có icon có nhãn cho trình đọc màn hình; icon trang trí ẩn khỏi trình đọc
- Trạng thái và lỗi có chữ đi kèm, không chỉ dựa vào màu
- Chữ tiếng Việt có dấu: chiều cao dòng đủ để không cắt dấu

## Nguồn để chuyển
- `vic-design-final-review/references/review.md` trục 6
- `vic-design-generate/references/qa-screen.md` S7

## Sửa khi chuyển
- Bộ gốc ghi "touch target 44, WCAG 2.5.5" như ngưỡng bắt buộc trong khi nền là mức AA. Sửa như mục Vùng chạm ở trên
