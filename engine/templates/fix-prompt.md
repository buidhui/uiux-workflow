---
intent: <slug>
artifact: fix-prompt
source: design-review version <n>
date: <YYYY-MM-DD>
---
# Fix prompt: <tên màn> · <tên section>

Prompt tự chứa: dùng được ở bất kỳ AI hoặc hội thoại nào có quyền sửa file Figma này. Không tham chiếu tới cuộc trao đổi nào khác.

## Bối cảnh
- File: <tên file, key> · Section hoặc frame: <node> · Breakpoint: <> · Mode: <>
- Design system: <tên>. Luật tóm tắt đủ để sửa đúng: <màu dùng biến nào cho vai trò nào, text style, thang khoảng cách, bo góc, icon, điều cấm>
- Yêu cầu gốc liên quan: "<trích scope đúng phần liên quan>"

## Việc cần sửa
### Fix 1 [CRITICAL] <tên ngắn>
- Vị trí: node <id> (<mô tả để người đọc tìm được>)
- Hiện trạng: <số đo, tên biến đang dùng, giá trị>
- Yêu cầu: <đích: tên biến hoặc text style kèm giá trị thật>
- Không được: <đổi phần khác, dùng mã màu rời, detach...>
- Nghiệm thu: <đo lại như thế nào, đạt khi nào>

## Ràng buộc chung
- Chỉ sửa node liệt kê
- Mọi giá trị qua biến hoặc text style của design system
- Giữ instance, đổi variant qua property, không tạo component mới
- Sửa xong: chụp ảnh và liệt kê node đã đổi

## Nghiệm thu tổng
- [ ] Fix 1 ...
