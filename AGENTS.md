# AGENTS.md

Hướng dẫn cho công cụ AI khác Claude Code (ví dụ Codex, Cursor) khi làm việc trong repo này.

1. Đọc `CLAUDE.md` trước mọi việc. Mọi quy tắc trong đó áp dụng cho mọi công cụ.
2. Lệnh của quy trình là file Markdown trong `.claude/commands/`. Khi người dùng gọi một lệnh, ví dụ `/ux` hoặc "làm bước kế tiếp", đọc file lệnh tương ứng (`.claude/commands/ux.md`) và làm theo từng bước.
3. Nghi thức chung nằm ở `.claude/protocol/`. Template ở `.claude/templates/`, checklist ở `.claude/verification/`, kiến thức ở `.claude/knowledge/`.
4. Review độc lập: không tự review thiết kế do chính phiên này làm ra. Đề nghị người dùng mở phiên mới, đưa các file theo `.claude/protocol/review-protocol.md` và yêu cầu phiên đó đóng vai theo `.claude/agents/ux-lead.md`.
5. Hộp chọn câu hỏi (AskUserQuestion) có thể không có trong công cụ này. Khi đó trình câu hỏi dạng danh sách đánh chữ cái và chờ người dùng trả lời.
6. Kết nối Figma và các lựa chọn thay thế: `SETUP.md`.
