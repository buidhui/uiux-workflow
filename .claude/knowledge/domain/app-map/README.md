# App-map

Mỗi module của sản phẩm một file `<module>.md`. App-map dày dần theo intent: sau Alignment Gate, màn mới được ghi với trạng thái "đã đồng thuận chiến lược" kèm mức thiết kế; sau UI Gate, cập nhật node ở page chính; sau Delivery Gate, "đã bàn giao".

Khung một file:

```markdown
---
module: <tên module>
figma: <file, page>
updated: <YYYY-MM-DD>
---
# <Tên module>

## Màn
| SCR | Tên | Node hoặc link | Vị trí | State có sẵn | Trạng thái | Intent gần nhất |
|---|---|---|---|---|---|---|

## Flow
| FLOW | Tên | Màn theo thứ tự |
|---|---|---|

## Pattern đang dùng
- <ví dụ: danh sách dùng bảng có header dính, hành động hàng loạt ở góc phải>

## Component thường dùng
| Component | Variant thường gặp | Ở đâu |
|---|---|---|

## Quy ước riêng
```
