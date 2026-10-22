# Checklist: E2 UI Design

## Trước khi dựng
- [ ] **[BLOCK]** `design-strategy.md` đã duyệt; `ux-brief.md` đã duyệt khi E1 chạy; version ghi vào build-report
- [ ] **[BLOCK]** AI chỉ dựng màn được giao cho AI và khi mức sẵn sàng design system từ 1
- [ ] **[BLOCK]** Đã lưu version có tên trước khi ghi; chỉ ghi vào khu vực nháp; CR sửa trên bản nhân bản
- [ ] Phase plan đã được duyệt khi màn lớn

## Tự kiểm, mỗi section và toàn màn
- [ ] **[BLOCK]** S1 Độ phủ: 100% dòng scope, hoặc GAP có lý do
- [ ] **[BLOCK]** S2 Biến: 0 mã màu rời, 0 biến nguyên thuỷ gán thẳng; khoảng cách thuộc thang; bo góc đúng bảng của domain
- [ ] **[BLOCK]** S3 Instance: 0 vẽ tay, 0 detach, 0 component bị bỏ, 0 component tự tạo khi chưa được phép
- [ ] S4 Chữ: text style của domain; 0 chữ mẫu, 0 tiếng Anh sót; chữ có dấu không bị cắt
- [ ] S5 Icon: đúng nguồn thư viện, đúng nấc kích thước, khoá tỉ lệ
- [ ] S6 Mode và breakpoint đặt rõ, khớp scope
- [ ] S7 Accessibility cơ học: tương phản chữ từ 4.5:1, thành phần không phải chữ từ 3:1; vùng chạm theo `accessibility.md`; nút chỉ có icon có nhãn
- [ ] S8 Bố cục: chiều rộng trong dải breakpoint, lưới đúng, không tràn, không đè
- [ ] S9 Nhất quán với màn liền kề; màn L3 bám reference lock

## Báo cáo
- [ ] **[BLOCK]** Tách rõ instance thư viện và frame tự dựng, kèm lý do
- [ ] Designer dựng tay: link frame đã ghi, tự kiểm đã chạy bằng cách đọc Figma
- [ ] GAP và Promote candidate mới đã vào gap log của sản phẩm; phần cần bổ sung vào kit đã qua `/kit-proposal`
