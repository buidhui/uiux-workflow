# Design Levels

Độ sâu của quy trình quyết định theo từng màn, không theo số màn. Hai màn cùng một intent có thể đi hai đường khác nhau: màn form ghép từ component có sẵn đi nhanh, màn cần sáng tạo phải có design ref và hướng thị giác trước khi vẽ.

## Trục 1: Mức thiết kế

| Mức | Nhận diện | Ví dụ | Đầu vào bắt buộc thêm | UI do ai dựng |
|---|---|---|---|---|
| L1 Có sẵn | Mọi component và pattern đã có trong design system hoặc trong app. Màn ghép từ form, bảng, danh sách, chi tiết, modal quen thuộc | Thêm trường vào form, màn danh sách quản trị theo mẫu có sẵn, thêm cột, đổi nhãn | Không | AI dựng khi design system từ mức 1; Designer dựng tay vẫn được |
| L2 Mở rộng | Phần lớn có sẵn, nhưng thiếu component hoặc pattern. Giữ nguyên ngôn ngữ thị giác của sản phẩm | Bộ lọc dạng mới, card cho loại dữ liệu chưa có, stepper, lịch, biểu đồ chưa có trong thư viện | Pattern cũ gần nhất; đề xuất component mới dựa trên style hiện có để Designer chọn | AI dựng phần có sẵn; phần mới dựng sau khi Designer chọn đề xuất, dưới dạng frame tự dựng |
| L3 Sáng tạo | Cần hướng thị giác hoặc trải nghiệm mới, cần gây ấn tượng hoặc tạo khác biệt | Landing, onboarding, dashboard tổng quan, gamification, màn rỗng lần đầu có minh hoạ, màn cho người dùng cuối B2C | Design ref bắt buộc: Designer gửi, hoặc AI nghiên cứu, sau đó Designer chọn. Không có ref thì Blocked | Designer dẫn; AI làm phương án khám phá theo reference lock khi Designer yêu cầu |

## Trục 2: Độ phức tạp logic

| Mức | Nhận diện |
|---|---|
| Thường | Một vai, hoặc các vai thấy giống nhau; ít state đặc biệt; không rule rẽ nhánh; không thao tác không hoàn tác |
| Phức tạp | Một trong số: nhiều vai với quyền khác nhau; state phụ thuộc trạng thái dữ liệu (chờ duyệt, đã khoá); rule rẽ nhánh; thao tác không hoàn tác hoặc hàng loạt; nhiều trường, dữ liệu lớn |

## Độ sâu theo từng màn

| | Logic thường | Logic phức tạp |
|---|---|---|
| L1 | Rà trường hợp biên rút gọn. UX Brief nén vào chiến lược thiết kế. AI dựng UI. Tự kiểm S1 đến S9. Review độc lập khi Designer muốn | Rà trường hợp biên đầy đủ. UX Brief nén, có đặc tả hành vi cho điểm phức tạp. Review độc lập bắt buộc |
| L2 | Rà rút gọn. UX Brief có wireframe và đề xuất component mới. Review độc lập bắt buộc | Rà đầy đủ. UX Brief đầy đủ có wireframe, đề xuất component, đặc tả hành vi. Review độc lập bắt buộc |
| L3 | Rà rút gọn. Design ref, chọn hướng thị giác (reference lock), wireframe. Designer dựng UI. Review độc lập bắt buộc | Như ô bên trái, cộng rà đầy đủ và đặc tả hành vi |

Rà rút gọn: chỉ các nhóm áp dụng cho màn đó, cộng corner checklist của domain. Rà đầy đủ: năm câu cấp flow và năm nhóm cấp màn theo `engine/knowledge/edge-case-sweep.md`.

## Cách gán mức
- D1 ước tính để báo Designer đường đi ở Context checkpoint. D2 xác định mức từng màn, kèm lý do, Designer duyệt ở Strategy Gate.
- Nghi ngờ giữa hai mức thì chọn mức cao hơn.
- Mức được nâng giữa chừng khi phát hiện thiếu component (L1 lên L2) hoặc Designer muốn làm mới hướng thị giác (lên L3). Nâng mức thì ghi DEC, thêm bước còn thiếu của màn đó; không chạy lại các màn khác.
- Mức thiết kế phụ thuộc design system của domain: cùng một màn có thể là L2 hôm nay và L1 sau khi thư viện có component đó. Đọc hướng dẫn dùng kit và gap log của sản phẩm (KB mục 5) trước khi gán.

## Gán mức khi domain mức 0
`components.md` còn trống thì đối chiếu với app đang chạy thay cho thư viện: app-map, màn trong file Figma của module, ảnh màn trong `assets/screens/`. Màn ghép được từ pattern đã thấy ở ít nhất một màn khác của app là L1; có phần chưa thấy ở đâu là L2. Ghi rõ đối chiếu với màn nào làm lý do. Mức 0 không làm L3 khó hơn: L3 là chuyện cần hướng thị giác mới, không phụ thuộc thư viện.

## Đường đi ở cấp intent

| Tình huống | Stage và gate |
|---|---|
| CR trên màn có sẵn, mọi màn L1, logic thường | D1 chạy liền D2 · Strategy Gate · D3 Alignment (thường chỉ cần PO xác nhận) · E1 nén · E2 · E3 khi Designer yêu cầu · UI Gate · Delivery Gate. Bốn gate |
| Mọi màn L1, có flow mới hoặc màn logic phức tạp | Context checkpoint · Strategy Gate · Alignment Gate · E1 nén · E2 · E3 · UI Gate · Delivery Gate. Năm gate |
| Có ít nhất một màn L2 hoặc L3 | Context checkpoint · Strategy Gate · Alignment Gate · UX Brief Gate · E2 · E3 · UI Gate · Delivery Gate. Sáu gate |

Alignment Gate chờ các bên bên ngoài, thường là điểm dài nhất về thời gian; Designer làm việc khác trong lúc chờ. Dev Feasibility Gate chỉ mở khi Dev có ý kiến về khả năng làm. Các điểm dừng giữa phase của E2 khi AI dựng màn lớn không tính.
