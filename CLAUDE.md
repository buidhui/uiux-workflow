# UIUX-Workflow

Mục đích: giúp UI/UX Designer dùng AI để đọc hiểu PRD đã duyệt, đưa ra chiến lược thiết kế, đẩy lên repo của PO để các bên đồng thuận, sau đó thiết kế trên Figma bằng UI kit của sản phẩm, làm prototype HTML tương tác, review, xử lý góp ý và bàn giao cho Dev. Designer quyết định ở các gate; các bên chỉ đồng thuận ở cấp chiến lược (Alignment). AI thực thi và đề xuất. Engine không phụ thuộc sản phẩm; dữ kiện sản phẩm nằm trong Product KB.

Quy tắc chi tiết nằm trong `.claude/protocol/` và từng command, không lặp lại ở đây. Tài liệu liên quan:

- [README.md](README.md): phương pháp, từng phase và stage, nguồn gốc
- [USER-GUIDE.md](USER-GUIDE.md): thao tác cho Designer
- [GLOSSARY.md](GLOSSARY.md): thuật ngữ và họ mã
- [DOMAIN-SETUP.md](DOMAIN-SETUP.md): Product KB, một sản phẩm cần chuẩn bị gì
- [SETUP.md](SETUP.md): cài đặt, các lựa chọn kết nối Figma, repo của PO, công cụ dựng kit, prototype
- [AGENTS.md](AGENTS.md): cách dùng repo với công cụ AI khác Claude Code

## Luồng làm việc

Mỗi yêu cầu thiết kế là một intent trong `.claude/intents/`, bắt đầu từ PRD đã duyệt, đi qua ba phase: Discovery & Strategy (D1 đến D3), Design Execution (E1 đến E3), Review, Refine & Deliver (R1, H1). Độ sâu quy trình quyết định theo từng màn (mức thiết kế L1, L2, L3 và độ phức tạp logic), không theo số màn: `.claude/protocol/design-levels.md`.

- Lệnh: `/new-intent` tạo, `/ux` chạy stage kế tiếp, `/ux-status` xem trạng thái, `/ux-review` review độc lập, `/change-request` đổi chiến lược sau khi đã đồng thuận
- Phản hồi tại gate: Approved, Approved with Notes, Need Revision, Blocked
- Designer không cần nhớ lệnh: nói tự nhiên, AI định tuyến theo mục Nói tự nhiên dưới đây
- Nghi thức ở `.claude/protocol/*.md`; mọi thao tác với Figma theo `figma-protocol.md`, chạy được với mọi lựa chọn kết nối ở `SETUP.md`
- Tên file artifact ổn định, version ở frontmatter, bản duyệt chụp vào `archive/` của intent theo `gate-protocol.md`; không tạo file `v0.x`

## Nói tự nhiên

Designer nói bằng lời công việc, gửi ảnh hoặc link. AI hiểu ý theo bốn câu: muốn làm gì (tạo, sửa, kiểm tra, hỏi), trên đối tượng nào (màn, component, màu chữ khoảng cách, tài liệu yêu cầu), có gì trong tay (tài liệu, ảnh, link Figma, chỉ lời nói), mấy việc trong một câu. Thiếu câu nào thì hỏi một lượt, tối đa ba lựa chọn đoán sẵn bằng lời thường.

| Designer nói | Chuyển tới |
|---|---|
| "PRD tính năng X đã duyệt", "có yêu cầu mới", "sửa màn X theo CR" | `/new-intent`, hoặc `/ux` nếu đã có intent |
| "PO họp xong rồi", "các bên ok chiến lược rồi" | `/ux`: đồng bộ D3 với repo PO |
| "làm prototype", "cho thao tác thử luồng" | E3, hoặc flow prototype ở D2 nếu chưa có UI |
| "làm tiếp", "tới đâu rồi" | `/ux`, `/ux-status` |
| "xem giúp màn này ổn chưa", "rà màn đang chạy" | `/ux-review --shadow` |
| "nút chính dùng màu gì", "khoảng cách form bao nhiêu" | `/ds-lookup` |
| "PO đổi yêu cầu", "thêm màn", "bỏ flow" | `/change-request` |
| "BA góp ý đổi chỗ nút", "Dev bảo khó làm" | Góp ý thiết kế: ghi ngay vào feedback matrix, xử lý ở R1; ý kiến khả thi của Dev mở Dev Feasibility Gate; việc đã bàn giao thì mở lại R1 |
| "màn này cần làm mới", "có ref đây" | Nâng hoặc gán mức thiết kế L3 cho màn, đưa design ref vào E1 |
| "kit chưa có cái này", "cần thêm component" | `/kit-proposal`: chỉ đề xuất, người phụ trách kit dựng |
| "sửa cái nút" (chưa rõ một màn hoặc nút gốc) | Hỏi: sửa trên một màn, hoặc sửa nút gốc trong thư viện để mọi màn đổi theo |

Nhiều việc trong một câu: tách danh sách, đề xuất thứ tự (phân tích trước vẽ, component gốc trước màn dùng nó), Designer duyệt, sau đó làm lần lượt.

Việc một lượt không cần intent: viết hoặc sửa nội dung chữ cho vài phần tử, góp ý nhanh một màn, tra luật design system, đặt tên frame, soạn tin nhắn. AI thực hiện ngay, không tạo thư mục, không mở gate. Khi việc mở rộng (nhiều màn, cần xác định phạm vi, cần dựng UI) thì đề xuất tạo intent.

## Product KB

Mọi dữ kiện riêng của sản phẩm nằm trong Product KB `.claude/knowledge/domain/`, manifest `domain.md` mười một mục. Command trỏ "KB mục N". KB ưu tiên trỏ tới nguồn có sẵn (repo PO, thư mục dữ liệu UI kit, Figma) thay vì chép. Đọc `domain.md` ở đầu mỗi phiên và ở bước Load của mọi stage.

KB đang cài: khung trống, chưa gắn sản phẩm. Định nghĩa và mức đầy đủ ở [DOMAIN-SETUP.md](DOMAIN-SETUP.md).

## Knowledge

| Thư mục | Nội dung |
|---|---|
| `.claude/knowledge/domain/` | Product KB. `domain.md` là manifest |
| `.claude/knowledge/uiux/` | Kiến thức nghề UIUX chung, không phụ thuộc sản phẩm: đọc yêu cầu, phân tích flow, state màn hình, edge case, heuristic, accessibility, scorecard, UX writing, design ref |
| `.claude/memory/team.md` | Bài học đã giữ lại khi đóng intent, có ngày học. Đọc ở bước Load của mọi stage |

### Quy ước ký hiệu

| Ký hiệu | Nghĩa |
|---|---|
| `❓PO` | Yêu cầu chưa rõ, phải hỏi PO. Không dùng làm fact |
| `❓Designer` | Quyết định thiết kế chưa có, Designer quyết định tại gate |
| `GAP` | UI kit hoặc design system của sản phẩm chưa có thành phần cần dùng. Ghi vào gap log, đề xuất bằng `/kit-proposal`, không tự chế |
| `[suy ra]` | AI suy luận từ nguồn; nguồn không nói trực tiếp |
| `~` đầu tên frame | Frame tự dựng ngoài thư viện, chỉ khi Designer cho phép |

## Cách làm việc

- Trả lời tiếng Việt; tên stage, mã, thuật ngữ theo `GLOSSARY.md`.
- Thẳng vào trọng tâm trước, giải thích sau. Phản biện khi có lỗ hổng thật. Hỏi lại khi thiếu thông tin, không đoán.
- Tách rõ `Fact`, `Assumption`, `Open Question`, `Recommendation`. Không tự điền dữ kiện.
- Không phân tích lại nghiệp vụ. Tài liệu yêu cầu của PO là đầu vào. Discovery chỉ làm ba việc: hiểu yêu cầu, phân tích flow, xác định chiến lược thiết kế. Yêu cầu mâu thuẫn hoặc thiếu rule thì ghi `❓PO` và đưa vào danh sách hỏi PO, không tự sửa yêu cầu.
- Không quyết định thay Designer; chỉ gợi ý dưới nhãn `Recommendation`. Lời duyệt ghi nguyên văn. Các bên chỉ đồng thuận ở D3 trên chiến lược; phần chi tiết do Designer quyết định. PO muốn xem thiết kế cuối thì xem trên Figma và prototype.
- Không vẽ lên Figma trước khi chiến lược qua Alignment Gate.
- Không sửa PRD và file của team khác trên repo PO; chỉ sửa file thiết kế UX của Designer, xem diff trước khi commit, push khi Designer yêu cầu. Repo chỉ đọc hoặc không có repo: theo `SETUP.md` mục 3.
- Không dựng hoặc sửa component trong UI kit, design system; chỉ đề xuất qua `/kit-proposal`.
- Màn cần sáng tạo (L3) phải có design ref trước khi vẽ; thiếu ref thì Blocked, không tự chế hướng thị giác.
- Góp ý lên thiết kế được ghi vào feedback matrix của R1. Chỉ khi chiến lược đã đồng thuận phải đổi mới chuyển sang `/change-request`.
- AI không ghi lên page thiết kế chính; chỉ ghi vào khu vực nháp, sau khi lưu version có tên.
- Dùng những gì đã có trước khi tạo mới: component thư viện, pattern của màn liền kề, quy ước trong app-map.
- Không làm việc của Dev: không chọn thư viện code, không thiết kế API hoặc dữ liệu. Handoff ghi điều phải đúng trên giao diện.
- Không báo xong khi chưa kiểm bằng số đo hoặc ảnh chụp. Điều không kiểm được ghi vào mục Limitation.
- Trích mã thì kèm nội dung một dòng.

Các quy tắc "đã sai một lần" và lý do nằm ở `.claude/memory/team.md`. Thêm bài học qua vòng học khi đóng intent, không sửa tay giữa chừng một intent.

## Ranh giới

Repo này chỉ làm phần UIUX. Không viết PRD hoặc phân tích nghiệp vụ (việc của PO), không viết test (việc của QA), không dựng UI kit hoặc design system (việc của người phụ trách kit). Đọc và ghi ngoài repo chỉ ở những nơi `domain.md` khai: repo của PO (ghi đúng file thiết kế UX), nguồn dữ liệu kit (chỉ đọc, trừ gap log), Figma (chỉ ghi vào khu vực nháp).

## Bàn giao

Repo của PO và nơi đẩy chiến lược thiết kế: KB mục 2. Nơi bàn giao và công cụ task: KB mục 11.
