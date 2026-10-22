# Gap log

Mọi trường hợp UI kit chưa làm được điều màn hình cần. Chỉ dùng file này khi sản phẩm chưa có gap log ở nơi khác (KB mục 5); có, sau đó thì ghi vào gap log đó theo định dạng của nó. D2 ghi gap thấy được từ PRD, E1 ghi component mới Designer đã chọn, E2 và R1 ghi gap gặp khi dựng và review, `/kit-proposal` viết đề xuất. Không xoá mục; xong thì đổi trạng thái.

Trạng thái: `open` · `proposed` (đã có đề xuất) · `in kit` (đã sửa trong kit, chưa publish) · `published` · `upstream` (cần sửa design system gốc) · `wontfix`.

```
### GAP-nnn · tên ngắn
- Gặp ở:          intent · màn · node
- Component:      component của kit (và nguồn gốc nếu giới hạn nằm ở design system)
- Xử lý tạm:      màn đang làm gì
- Đề xuất:        thay đổi kit hoặc design system để bỏ xử lý tạm
- Trạng thái:     open | proposed | in kit | published | upstream | wontfix · ngày
```
