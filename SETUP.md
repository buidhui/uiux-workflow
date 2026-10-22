# Cài đặt và kết nối

Tài liệu này dành cho Designer nhận bàn giao quy trình. Mỗi phần nêu các cách làm được hỗ trợ; Designer chọn cách phù hợp với máy, tài khoản và quyền của mình. Quy trình chạy được với mọi lựa chọn dưới đây. Lựa chọn nào thiếu khả năng thì bước tương ứng chuyển sang cách làm thay thế, ghi ở bảng "Lựa chọn nào cho stage nào" (mục 2).

## 1. Công cụ AI

| Cách | Khi nào dùng | Cách chạy quy trình |
|---|---|---|
| Claude Code trong VS Code, JetBrains, ứng dụng desktop hoặc terminal | Cách chính, được hỗ trợ đầy đủ | Mở thư mục repo. Lệnh `/ux`, `/new-intent` và các lệnh khác có sẵn |
| Công cụ AI khác đọc được repo (ví dụ Codex, Cursor) | Team đang dùng công cụ đó | Công cụ đọc `AGENTS.md`. Lệnh là file Markdown trong `.claude/commands/`; yêu cầu AI đọc file lệnh, sau đó làm theo, ví dụ "đọc `.claude/commands/ux.md` và làm theo" |

Với công cụ khác Claude Code, agent review độc lập (`.claude/agents/ux-lead.md`) có thể không chạy được như một agent riêng. Khi đó mở một phiên mới, đưa đúng các file mà `review-protocol.md` liệt kê và yêu cầu đóng vai UX Lead theo file agent; phiên review không được thấy hội thoại thiết kế.

## 2. Kết nối Figma

Có bốn lựa chọn. Một máy có thể cài nhiều lựa chọn cùng lúc; ghi lựa chọn đang dùng vào Product KB mục 6.

### Lựa chọn A: Connector Figma của claude.ai

Kết nối từ tài khoản claude.ai, dùng được trong Claude Code khi đăng nhập cùng tài khoản.

1. Vào claude.ai, mục Settings, Connectors, chọn Figma, đăng nhập Figma.
2. Mở Claude Code, gõ `/mcp`, kiểm tra Figma có trong danh sách.
3. Tài khoản Figma cần quyền sửa file đích nếu muốn AI ghi vào Figma.

### Lựa chọn B: Figma Dev Mode MCP server trên máy

Server chạy cùng ứng dụng Figma desktop, chỉ đọc.

1. Mở Figma desktop, vào Preferences, bật Dev Mode MCP Server.
2. Thêm vào Claude Code: `claude mcp add --transport http figma-desktop http://127.0.0.1:3845/mcp`. Địa chỉ theo tài liệu của Figma tại thời điểm viết; kiểm tra lại trong tài liệu của Figma nếu kết nối thất bại.
3. Figma desktop phải đang mở khi AI làm việc. Lỗi kết nối bị từ chối (connection refused) thường do Figma chưa mở hoặc server chưa bật.

### Lựa chọn C: figma-console MCP và plugin Desktop Bridge

Đọc và ghi qua plugin chạy trong Figma desktop. Bộ skill dựng kit của UpBase dùng cách này.

1. Tạo personal access token trong Figma, mục Settings, Security, quyền đọc file và thư viện.
2. Thêm vào Claude Code: `claude mcp add figma-console --scope user --env FIGMA_ACCESS_TOKEN=<token> -- npx -y figma-console-mcp@latest`.
3. Trong Figma desktop, mở file cần làm, chạy Plugins, Development, Figma Desktop Bridge. Giữ cửa sổ plugin mở trong lúc AI làm việc.
4. Token hết hạn không báo lỗi; tìm kiếm qua REST trả về rỗng. Gặp kết quả rỗng bất thường thì kiểm tra token trước.

### Lựa chọn D: Không kết nối

Designer gửi ảnh chụp màn hình hoặc ảnh xuất từ Figma, và link frame để ghi vào tài liệu. AI đọc ảnh. Mọi việc ghi vào Figma do Designer làm.

### Khả năng của từng lựa chọn

| Việc | A. Connector claude.ai | B. Dev Mode MCP | C. figma-console | D. Không kết nối |
|---|---|---|---|---|
| Đọc cấu trúc frame, design context | Có | Có | Có | Không, chỉ đọc ảnh |
| Chụp ảnh frame | Có | Có | Có | Designer gửi ảnh |
| Đọc biến, token | Có | Có | Có | Không |
| Tìm component trong thư viện | Có | Hạn chế | Có, qua plugin | Không |
| Dựng instance, sửa frame | Có, qua lệnh chạy Plugin API | Không | Có | Không |
| Lưu version có tên | Kiểm khi cài | Không | Kiểm khi cài | Designer lưu |
| Ghi annotation, note | Kiểm khi cài | Không | Có | Designer ghi |
| Vẽ sơ đồ trên FigJam | Có | Không | Hạn chế | Không |
| Cần Figma desktop mở | Không | Có | Có | Không |
| Cần token | Không | Không | Có | Không |

"Kiểm khi cài" nghĩa là khả năng phụ thuộc phiên bản công cụ. Lần chạy đầu, AI thử và ghi kết quả vào Product KB mục 6.

### Lựa chọn nào cho stage nào

| Stage | Cần | Lựa chọn đủ | Khi không đủ |
|---|---|---|---|
| D2 | Đọc màn liền kề | A, B, C | D: Designer gửi ảnh màn liền kề |
| E1 vẽ wireframe trên Figma (tuỳ chọn) | Ghi | A, C | Wireframe dạng khối văn bản trong `ux-brief.md` |
| E2 AI dựng UI | Ghi, tìm component | A, C | Designer dựng; AI tự kiểm bằng cách đọc (A, B, C) hoặc qua ảnh (D) |
| E3 prototype | Đọc design context | A, B, C | D: dựng từ chiến lược, UX Brief và ảnh; độ giống thấp hơn, ghi trong `prototype-report.md` |
| R1 review | Đọc, chụp ảnh, đọc biến | A, B, C | D: review qua ảnh; mọi nhận xét ghi nhãn Visual judgment, các trục cần số đo ghi N/A |
| H1 ghi chú bàn giao | Ghi | A, C | Designer ghi theo nội dung AI soạn |

### Agent review và công cụ Figma

Agent `ux-lead` chỉ được đọc Figma. Danh sách công cụ của agent nằm ở dòng `tools` của `.claude/agents/ux-lead.md`, đã có tên công cụ đọc của lựa chọn A, B (tên server `figma-desktop`) và C. Khi cài server với tên khác, thêm tên công cụ chụp ảnh và đọc của server đó vào dòng `tools`, theo dạng `mcp__<tên server>__<tên công cụ>`; xem tên bằng lệnh `/mcp`.

## 3. Repo của PO

| Cách | Khi nào | D3 và H1 làm gì |
|---|---|---|
| Repo git, Designer có quyền push | Team PO dùng PO-Workflow hoặc repo tài liệu | AI sửa file thiết kế UX trong intent của PO, Designer xem diff, AI commit, push khi Designer yêu cầu |
| Repo git, Designer chỉ có quyền đọc | Quy ước của PO không cho Designer push | AI soạn nội dung file; Designer gửi PO, hoặc mở pull request nếu quy ước cho phép |
| Không có repo; PRD trên Lark, Confluence, Google Docs | Team PO chưa dùng repo | AI xuất file thiết kế UX ở `discovery/alignment/`; Designer đưa lên nơi PO dùng; xác nhận của PO dán nguyên văn vào `decisions.md` |

Chọn cách trong Product KB mục 2.

## 4. Git cho repo này

| Cách | Ghi chú |
|---|---|
| Dùng git trong terminal hoặc trong VS Code | Cách chính |
| Không dùng git | Quy trình vẫn chạy; mất lịch sử thay đổi và không chia sẻ được với Designer khác. Nên sao lưu thư mục `.claude/intents/` định kỳ |
| Nhờ AI commit | AI chỉ commit và push khi Designer yêu cầu |

## 5. UI kit và công cụ dựng kit

| Tình huống | Cách làm |
|---|---|
| Sản phẩm có UI kit trên Figma và hướng dẫn dùng kit | Khai trong Product KB mục 5; AI dùng kit ở D2, E2 |
| Có UI kit nhưng chưa có hướng dẫn dùng | AI đọc thư viện trên Figma (A, C); hướng dẫn dùng kit được viết dần theo việc |
| Chưa có UI kit | Mức sẵn sàng 0; Designer dựng UI; mọi màn có phần chưa có trong app được xếp tối thiểu L2 |
| Có công cụ dựng kit (ví dụ một bộ skill dựng kit) | Khai trong Product KB mục 5; `/kit-proposal` chuyển đề xuất cho công cụ đó ở bước đề xuất |
| Không có công cụ dựng kit | `/kit-proposal` ghi đề xuất vào gap log; người phụ trách kit đọc và xử lý |

## 6. Prototype

| Tình huống | Cách làm |
|---|---|
| Biết thư viện component của frontend | Prototype dùng thư viện đó qua CDN, giống sản phẩm thật nhất |
| Không biết, hoặc thư viện không tải được trong một file HTML | Prototype dùng HTML và CSS theo token của Product KB |
| Cần chia sẻ cho người không có repo | Gửi file `index.html`; người nhận mở bằng trình duyệt, không cần cài đặt. Nếu môi trường có công cụ đăng trang (ví dụ artifact của claude.ai), có thể đăng thành link riêng tư |
| Muốn trình bày trong Figma | Nối điều hướng giữa frame (lựa chọn A hoặc C); không có thì Designer nối tay |

## 7. Kiểm tra sau khi cài

1. Mở repo bằng công cụ AI, gõ `/` (Claude Code) và thấy `/ux`.
2. Hỏi AI "đọc giúp frame <link>" để kiểm kết nối Figma; với lựa chọn D, gửi một ảnh.
3. Hỏi AI "liệt kê intent trong repo của PO" để kiểm đường dẫn ở Product KB mục 2.
4. Ghi lựa chọn đã dùng và kết quả kiểm vào Product KB mục 6.
