---
status: chưa viết
---
# Scorecard của Design Review

Dùng ở R1 và `/ux-review`. Khung dưới đây lấy từ bộ gốc, chưa hiệu chỉnh. Hiệu chỉnh sau đợt chạy thử bằng cách cho agent và Designer chấm độc lập cùng một bộ màn, sau đó so điểm.

## Khung đề xuất

| Trục | Trọng số | Ghi chú |
|---|---|---|
| Requirement fit | 25 | N/A khi không có scope để đối chiếu |
| Flow và IA | 15 | |
| Heuristic | 15 | |
| Visual hierarchy | 10 | Nhận xét bằng mắt |
| Consistency với design system | 15 | N/A khi domain mức 0 |
| Accessibility | 15 | |
| Responsive và nội dung | 5 | |

- Mỗi trục bắt đầu từ trọng số đầy đủ, trừ theo finding của trục: Critical, Major, Minor. Mức trừ cụ thể chờ hiệu chỉnh
- Trục N/A: loại khỏi mẫu số, quy đổi lại thang 100
- Luật trần: còn Critical chưa sửa thì không qua PASS; Requirement fit dưới một nửa trọng số thì không qua NEEDS REWORK
- Verdict: PASS, CONDITIONAL PASS, NEEDS REWORK, FAIL; ngưỡng chờ hiệu chỉnh
- GAP của design system không trừ điểm Designer

## Nguồn để chuyển
- `vic-design-final-review/references/scorecard.md` mục 1 đến 3, 5

## Sửa khi chuyển
- Bộ gốc trừ cố định 60%, 25%, 8% trọng số cho mỗi finding, không chia theo số màn: màn lớn bị trừ nặng hơn, mười ba finding Minor đủ đưa một trục về 0. Cần chuẩn hoá theo số màn hoặc đặt sàn cho từng mức
