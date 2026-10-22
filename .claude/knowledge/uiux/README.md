# Knowledge pack nghề UIUX

Kiến thức chung cho vai UI/UX Designer, không phụ thuộc sản phẩm. Khác với `../domain/`, là Product KB của sản phẩm đang cài. Command của stage ghi file nào cần đọc.

Bộ gốc để chuyển nội dung: thư mục `claude-skills-uiux-vic` (xem README mục Nguồn gốc); phần heuristic, accessibility, interaction pattern có thể lấy thêm từ kiến thức Design Agent của AWS AI-DLC (`core/knowledge/aidlc-design-agent/`, MIT-0). Khi chuyển, gỡ mọi dữ kiện của VIC (tên biến, node, file key, tên sản phẩm), chỉ giữ phương pháp. Kiểm sau khi chuyển: thư mục này không còn tên biến, file key hoặc tên sản phẩm của bộ gốc.

| File | Nội dung | Stage đọc | Tình trạng |
|---|---|---|---|
| `screen-states.md` | Bảy state cấp màn, quy tắc khai | D2, E1, E2, R1, H1 | Đã viết |
| `requirement-reading.md` | Phân loại câu trong tài liệu yêu cầu, chuẩn câu yêu cầu, từ yêu cầu ra user task, đọc wireframe của PO | D1 | Chưa viết |
| `flow-analysis.md` | Phân rã flow tới đúng độ sâu, định vị màn vào cấu trúc app, gán mức thiết kế | D2 | Chưa viết |
| `edge-case-sweep.md` | Năm câu cấp flow, năm nhóm cấp màn, rà rút gọn và đầy đủ, mức ưu tiên, đặc tả hành vi | D2 | Chưa viết |
| `heuristics.md` | Mười heuristic, cognitive walkthrough, phân cấp thị giác | R1 | Chưa viết |
| `accessibility.md` | Tương phản, vùng chạm, focus, nhãn, màu không là tín hiệu duy nhất | E2, R1 | Chưa viết |
| `scorecard.md` | Bảy trục, trọng số, mức trừ, luật trần, verdict | R1 | Chưa viết |

Nguồn bổ sung: hướng dẫn cũ của team `User Guide_UI-UX- Workflow w AI.md` (Step 1 đến 9, prompt mẫu, lỗi thường gặp), dùng cho `requirement-reading.md`, `ux-writing-vi.md` và USER-GUIDE.
| `ux-writing-vi.md` | Nguyên tắc chữ trên giao diện tiếng Việt, câu mẫu chung | D2, E1, E2 | Chưa viết |
| `prototyping.md` | Flow prototype và prototype HTML: chuẩn chung, bảng điều khiển, dữ liệu mẫu | D2, E3 | Đã viết |
| `reference-research.md` | Design ref cho màn L3: phân tích ref, nghiên cứu khi chưa có, chống trung bình hoá, reference lock | E1 | Chưa viết |
