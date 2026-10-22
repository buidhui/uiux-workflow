---
description: Dựng Product KB cho một sản phẩm theo mười một mục của DOMAIN-SETUP.md; ưu tiên trỏ tới nguồn có sẵn
argument-hint: <tên sản phẩm>
---
# /new-domain

Dựng Product KB. Phần cần người quyết định vẫn là người làm; lệnh này hỏi đúng câu, kiểm đường dẫn, ghi đúng vị trí. Đọc `DOMAIN-SETUP.md` trước khi chạy.

## 0. Kiểm an toàn
- `.claude/intents/` còn intent nào thì dừng: sản phẩm mới dựng ở repo mới.
- `domain.md` đã điền thì hỏi Designer có muốn dựng lại không. Xác nhận xong mới ghi đè.

## 1. Hỏi theo mức Tối thiểu trước, một lượt
Mục 1, 2, 5 (file kit, mức sẵn sàng), 6, 11 theo bảng ở `DOMAIN-SETUP.md` mục 2. Với mỗi mục, hỏi "đã có ở đâu chưa" trước "nội dung là gì".

## 2. Kiểm nguồn
- Repo của PO: pull được không, tìm một intent mẫu, tìm template file thiết kế UX.
- File Figma và UI kit: đọc được không bằng công cụ MCP đã khai.
- Thư mục dữ liệu kit (nếu có): có hướng dẫn dùng kit, gap log không.
Đường dẫn không mở được thì ghi `❓Designer`, không tự điền.

## 3. Ghi
- `domain.md`: mười một mục, đường dẫn trước, nội dung ngắn sau.
- Đánh giá mức sẵn sàng design system theo `.claude/protocol/figma-protocol.md` mục 1; không ghi mức cao hơn bằng chứng.
- File trong KB chỉ tạo cho nội dung chưa có nguồn: `gap-log.md`, `content-guide.md`, `corner-checklist.md`, `frontend-stack.md`, `app-map/`, `assets/`.
- `.claude/memory/team.md` về bản trống, thêm dòng ngày khởi tạo.

## 4. Mức Hiệu quả
Hỏi tiếp mục 3, 4, 5 đầy đủ, 7, 8, 9 nếu Designer muốn làm ngay; không thì ghi là sẽ dày dần theo việc.

## 5. Kết thúc
Trình: mục đã đủ theo từng mức, đường dẫn còn `❓Designer`, việc kế tiếp. Tự kiểm theo checklist ở `DOMAIN-SETUP.md` mục 7.
