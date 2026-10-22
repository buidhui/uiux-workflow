# Screen states

Định nghĩa duy nhất về state cấp màn cho mọi stage. D2 khai, E1 mô tả, E2 dựng, R1 kiểm, H1 bàn giao theo cùng bảng này. Bảy state trùng với danh sách team đang dùng trong hướng dẫn cũ.

## State cấp màn

| State | Khi nào | Bắt buộc khai cho |
|---|---|---|
| Default | Dữ liệu điển hình, đầy đủ. Dùng dữ liệu mẫu thực tế, danh sách đủ dài để thấy nhịp | Mọi màn |
| Empty | Chưa có dữ liệu ở lần dùng đầu; tìm hoặc lọc không ra; đã xoá toàn bộ. Ba trường hợp có thể cần ba nội dung khác nhau | Màn có danh sách hoặc vùng dữ liệu |
| Loading | Đang tải lần đầu; đang tải thêm; đang xử lý một thao tác | Màn gọi dữ liệu hoặc có thao tác chờ |
| Success | Phản hồi sau thao tác thành công: thông báo, chuyển màn, cập nhật ngay trên màn | Màn có thao tác ghi |
| Error | Lỗi tải; lỗi một phần (một vùng tải được, một vùng lỗi); không tìm thấy; lỗi khi lưu; lỗi nhập liệu | Màn gọi dữ liệu, có thao tác ghi, hoặc có form |
| Disabled | Màn hoặc vùng bị khoá do trạng thái của dữ liệu hoặc quy trình, không do quyền: đơn đã duyệt không sửa được, đợt đã đóng, đang chờ xử lý | Màn có dữ liệu đổi trạng thái |
| Permission | Vai không có quyền: ẩn phần tử, chỉ xem, hoặc chặn cả màn kèm giải thích | Màn hoặc phần tử có phân quyền |

Phân biệt Disabled và Permission: cùng một người, đổi trạng thái dữ liệu mà màn mở lại được là Disabled; đổi vai mới mở được là Permission.

Quy tắc khai:
- Mỗi màn khai đủ bảy cột. Mỗi ô là một trong ba: có, không kèm lý do, hoặc `GAP` (design system chưa có cách thể hiện).
- "Không" mà không có lý do là chưa xong.
- Một state có nhiều trường hợp thì liệt kê từng trường hợp.
- Mỗi state có làm thì là một frame riêng khi dựng, cùng hàng với frame Default, cùng tiền tố tên.

## State cấp phần tử

Hover, pressed, focus, disabled, selected, invalid của từng phần tử tương tác theo design system của domain, không khai ở bảng cấp màn. Focus phải nhìn thấy được ở mọi phần tử tương tác, kể cả khi thư viện Figma chưa có variant focus.

## Vì sao có file này

Bộ skill VIC định nghĩa state ở bốn nơi, lệch nhau (năm đến tám state). Hướng dẫn cũ của team dùng bảy state: default, empty, loading, success, error, disabled, permission. File này lấy đúng bảy state đó, viết rõ điều kiện từng state, và tách Disabled (do trạng thái dữ liệu) khỏi Permission (do vai).
