---
description: Bảng trạng thái mọi intent thiết kế, kèm kiểm tra lệch giữa state và file. Chỉ đọc, không sửa
argument-hint: [intent-slug]
---
# /ux-status

Chỉ đọc. Không sửa file nào. Phát hiện lệch thì báo, không tự sửa.

## Bảng tổng
Với mỗi `intents/*/state.md`, một dòng:

| Intent | Màn theo mức (L1, L2, L3) | Stage hiện tại | Trạng thái | Việc kế tiếp | Câu hỏi còn mở | Góp ý bắt buộc còn mở | Frame Figma |
|---|---|---|---|---|---|---|---|

Có `$ARGUMENTS` thì chỉ in intent đó, kèm bảng Stages và bảng Versions.

## Kiểm tra lệch
Chưa có script, kiểm bằng tay. Liệt kê mọi phát hiện, không dừng ở phát hiện đầu:
1. Stage `[x]` không có artifact; D2, E1, R1, H1 `[x]` không có bản chụp trong `archive/`.
2. Artifact có trên đĩa nhưng stage vẫn `[ ]`.
3. Phiên bản trong `state.md` khác frontmatter artifact.
4. Stage `[x]` không có dòng DEC cùng stage.
5. Questions file có câu chặn còn trống nhưng stage đã qua `[?]`.
6. `[?]`, `[-]` hoặc Parked quá 7 ngày không đổi: nhắc.
7. E2 xong nhưng `design-strategy.md` hoặc `ux-brief.md` có version mới hơn version đã dựng theo.
8. Màn đã duyệt ở D2 chưa được ghi vào app-map của domain.
9. `GAP` hoặc Promote candidate trong intent chưa có trong gap log của sản phẩm.
10. Màn L3 chưa có design ref mà intent đã qua D3.
13. `design-strategy.md` có version mới hơn bản đã đẩy lên repo PO (theo `alignment-log.md`); hoặc PRD trên repo PO có version mới hơn `inputs` của chiến lược.
14. D3 Parked chờ đồng thuận quá 5 ngày làm việc: nhắc Designer hỏi PO.
15. Prototype lấy từ version Figma cũ hơn bản đã qua UI Gate.
11. Frame còn ở khu vực nháp sau UI Gate.
12. R1 Parked chờ góp ý đã quá hạn: nhắc Designer quyết định đi tiếp hoặc nhắc người góp ý.

Cuối bảng: số mục mở trong gap log của sản phẩm, nhóm theo component, để người phụ trách kit thấy việc nào lặp lại nhiều nhất.

| # | Intent | Lệch | Gợi ý xử lý |
|---|---|---|---|

Không lệch thì ghi một dòng "state khớp với đĩa".
