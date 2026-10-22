---
status: chưa viết
---
# Design system: luật dùng

Khung mục lấy từ cấu trúc của `vic-design-system/SKILL.md` trong bộ gốc, bỏ toàn bộ dữ kiện VIC. Điền theo sản phẩm. Bảng chi tiết nằm ở `tokens.md` và `components.md`; file này chỉ chứa luật.

## 0. Luật không được vi phạm
<Năm đến tám luật kiểm được, mỗi luật kèm một ví dụ vi phạm điển hình. Ví dụ dạng luật: không gán mã màu rời; không dùng biến nguyên thuỷ trực tiếp; trạng thái hover, pressed của Figma không phải prop trong code; không dựng dữ liệu thành variant; focus bắt buộc có trong code.>

## 1. Mô tả chuẩn hoá trên Figma
<Bộ khoá mô tả mà mỗi component chính phải có, ví dụ PURPOSE, ANATOMY, PROPS, STATES, GAPS, CODE-MAP, USE, AVOID, A11Y, RELATED. Bộ khoá cho mô tả của biến. Đây là điều kiện để lên mức sẵn sàng 2.>

## 2. Màu
<Kiến trúc lớp biến. Chọn theo vai trò trước (nền, chữ, viền, icon), mức nhấn sau. Cặp màu chuẩn dùng nguyên cụm. Màu trạng thái và màu phân loại không trộn. Quy tắc state màu.>

## 3. Chữ
<Họ chữ, thang chữ, weight theo vai trò, bẫy cần tránh, chữ tiếng Việt có dấu.>

## 4. Khoảng cách, padding, bo góc
<Thang khoảng cách, quy tắc chọn bậc theo quan hệ, bảng padding và bo góc theo component.>

## 5. Component
<Component nên dùng, component bị bỏ, cây quyết định chọn component theo nhu cầu.>

## 6. Layout và breakpoint
<Breakpoint, lưới, chiều rộng điều hướng và vùng phụ.>

## 7. Lỗi đã biết trong thư viện
<Tên sai, property vô nghĩa, cấu trúc cần cảnh báo khi chuyển sang code.>

## 8. Checklist tự kiểm
<Danh sách kiểm trước khi trả kết quả, dùng ở E2 và R1.>
