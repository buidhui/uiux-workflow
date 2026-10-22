---
description: Stage D1 Context Overview. Hiểu bối cảnh, mục tiêu tính năng, người dùng, phạm vi ban đầu trước khi phân tích flow. Gọi qua /ux
argument-hint: <intent-slug>
---
# D1 Context Overview

| | |
|---|---|
| Stage | D1 Context Overview |
| Slug | context-overview |
| Phase | discovery |
| Execution | always, chạy ngay sau `/new-intent`. CR trên màn có sẵn mà mọi màn L1, logic thường: chạy liền với D2, không dừng riêng |
| Produces | `discovery/context-overview/context-overview.md` · `context-overview-questions.md` |
| Consumes | `inputs/*` và tài liệu trỏ tới trong `intent.md` (bắt buộc) · wireframe của PO, ảnh màn cũ, link Jira (tuỳ) · app-map của module liên quan |
| Requires | none |
| Áp dụng | Cả intent |
| Reviewer | none |
| Archive | no |
| Template | `engine/templates/context-overview.md` |
| Checklist | `engine/verification/context-overview.md` |
| Knowledge | `engine/knowledge/requirement-reading.md` · KB mục 1, 2, 3 |

Chạy theo `engine/protocol/stage-protocol.md`. Tương ứng Step 1 trong tài liệu hướng dẫn cũ của team.

## Mục đích
Designer và AI hiểu cùng một bối cảnh: tính năng giải quyết vấn đề gì, cho ai, vai nào làm gì trên giao diện, module và màn nào bị chạm, điều gì đã rõ, điều gì chưa rõ. Chưa thiết kế UI, không phân tích lại nghiệp vụ.

## Load
- Đọc toàn bộ tài liệu. Xác định loại và mức hoàn thiện: PRD đã duyệt, user stories, CR notes, mô tả miệng, danh sách finding Designer chọn sửa.
- Tài liệu từ repo của PO: đọc PRD đã duyệt và artifact liên quan theo KB mục 2; nghiệp vụ tra KB của PO theo KB mục 3, chỉ đọc. Giữ nguyên mã của PO.
- Wireframe của PO: đọc như ý định của PO; bản thiết kế do Designer làm. Tách phần đã quyết định (có màn này, có trường này) và phần vẽ tạm (bố cục, cách hiển thị).
- Ảnh màn cũ, ảnh khoanh vùng: xác định màn nào trên app.
- App-map của module liên quan.

## Ask
Chỉ hỏi những điểm ảnh hưởng tới thiết kế: vai và quyền hiển thị khi tài liệu không nói; yêu cầu không đo được; tham chiếu viết tắt; nền tảng, breakpoint. Điểm nghiệp vụ chưa rõ ghi `OQ-NN` với `❓PO` vào mục Câu hỏi cho BA, PO.

## Generate
`context-overview.md` theo template: tóm tắt mục tiêu tính năng; người dùng và vai; business context ở mức đủ để thiết kế; yêu cầu chạm giao diện thành user task `UT-NN`; wireframe của PO đã quyết định và để ngỏ; module, màn có thể bị ảnh hưởng; ước tính sơ bộ mức thiết kế (`design-levels.md`), xác định ở D2; Confirmed, Assumption, Open question; câu hỏi cho BA, PO kèm tin nhắn dán thẳng; nguồn đã đọc.

## Đường đi
Ước tính mức thiết kế và độ phức tạp từng màn theo `design-levels.md`, chọn đường đi theo bảng "Đường đi ở cấp intent", ghi vào `state.md`: bảng màn và mức, stage nén hoặc bỏ qua ghi `[S]` kèm lý do. Có màn có vẻ L3 mà chưa có design ref: nhắc Designer chuẩn bị vào `inputs/refs/`.

## Gate
Context checkpoint. Trình: số user task, số vai, module bị chạm, câu hỏi BA, PO (chặn và không chặn), và đường đi bằng lời thường, ví dụ "4 màn: 3 màn form có sẵn component, 1 màn dashboard cần sáng tạo, cần design ref; 5 lần duyệt". Approved thì ghi `DEC1`: đường đi và lý do, nguyên văn Designer. Stage kế: D2.

CR trên màn có sẵn, mọi màn L1, logic thường: không mở gate này; nói một dòng đường đi, sau đó chạy D2, xác nhận đường đi ở Strategy Gate.
