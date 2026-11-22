# Phiếu QC 1 — Road v1.0 (TỰ KIỂM)

Lô được kiểm (học viên): Nguyễn Thái Dương (tự kiểm)   Người kiểm: Trần Như Thái  
Ngày: 22/11/2026   Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): nguyenthaiduong-front.zip, nguyenthaiduong-fisheye.zip, revision 1  
Số ảnh kiểm: 20 (A01–A12, B01–B08), không có ảnh thêm   Số nhãn đã kiểm (shape + tag): 332 (252 shape + 80 tag)

## Tổng hợp theo mã
"Số mục kiểm" tính theo số nhãn thuộc nhóm đó trong manifest (đếm từng nhãn lane, drivable, đèn, biển…).

| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 20 | 2 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 40 | 5 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 50 | 8 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 50 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 50 | 5 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 50 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 97 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 46 | 3 | nhẹ |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 105 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 59 | 4 | nhẹ |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 76 | 8 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

QC1-06, QC1-07, QC1-09 ghi 0 lỗi vì `lint` không kiểm các mục này (chỉ GT mới kiểm được), **không phải** vì đã xác nhận đúng.

## Danh sách lỗi (mỗi lỗi một dòng)
Mô tả lấy nguyên từ cảnh báo của lint.

| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-05 | A01 | lane | chính | 2 polyline cùng position L2: vạch đứt có bị tách không? |
| 2 | QC1-04 | A03 | lane#11@(668,390) | chính | điểm đầu cao hơn điểm cuối: có vẽ từ xa về gần không? |
| 3 | QC1-08 | A04 | traffic_light#9@(603,275) | nhẹ | box thấp hơn 8 px: không bắt buộc |
| 4 | QC1-02 | A05 | lane | nặng | chưa có L1 (bỏ qua nếu thật sự không thấy vạch) |
| 5 | QC1-02 | A05 | lane | nặng | chưa có R1 (bỏ qua nếu thật sự không thấy vạch) |
| 6 | QC1-02 | A06 | lane | nặng | chưa có R1 (bỏ qua nếu thật sự không thấy vạch) |
| 7 | QC1-02 | A07 | lane | nặng | chưa có L1 (bỏ qua nếu thật sự không thấy vạch) |
| 8 | QC1-08 | A07 | traffic_light#0@(703,244) | nhẹ | box thấp hơn 8 px: không bắt buộc |
| 9 | QC1-08 | A07 | traffic_light#12@(640,228) | nhẹ | box thấp hơn 8 px: không bắt buộc |
| 10 | QC1-05 | A08 | lane | chính | 2 polyline cùng position L2: vạch đứt có bị tách không? |
| 11 | QC1-02 | A09 | lane | nặng | chưa có R1 (bỏ qua nếu thật sự không thấy vạch) |
| 12 | QC1-10 | A10 | traffic_sign#1@(488,235) | nhẹ | box thấp hơn 8 px: không bắt buộc |
| 13 | QC1-10 | A10 | traffic_sign#2@(537,236) | nhẹ | box thấp hơn 8 px: không bắt buộc |
| 14 | QC1-10 | A10 | traffic_sign#19@(422,192) | nhẹ | box thấp hơn 8 px: không bắt buộc |
| 15 | QC1-05 | A12 | lane | chính | 2 polyline cùng position L1: vạch đứt có bị tách không? |
| 16 | QC1-11 | B02 | road_curb#6@(758,383) | chính | chỉ 2 điểm: trên fisheye hãy đặt điểm theo cung |
| 17 | QC1-11 | B02 | road_curb#7@(532,386) | chính | chỉ 2 điểm: trên fisheye hãy đặt điểm theo cung |
| 18 | QC1-11 | B02 | traffic_light#9@(113,116) | chính | gợi ý edge_zone = bật (tâm box ngoài 80 % bán kính; tự kiểm lại) |
| 19 | QC1-11 | B02 | traffic_light#10@(1078,75) | chính | gợi ý edge_zone = bật (tâm box ngoài 80 % bán kính; tự kiểm lại) |
| 20 | QC1-11 | B03 | traffic_sign#6@(1131,362) | chính | gợi ý edge_zone = bật (tâm box ngoài 80 % bán kính; tự kiểm lại) |
| 21 | QC1-10 | B03 | traffic_sign#9@(795,269) | nhẹ | box thấp hơn 8 px: không bắt buộc |
| 22 | QC1-01 | B04 | tag | nặng | camera: camera = fisheye_front, tên file gợi ý fisheye_rear |
| 23 | QC1-11 | B04 | traffic_sign#4@(1065,171) | chính | gợi ý edge_zone = bật (tâm box ngoài 80 % bán kính; tự kiểm lại) |
| 24 | QC1-03 | B05 | lane#5@(1123,446) | nặng | camera hai bên: lane phải có position = other |
| 25 | QC1-11 | B05 | traffic_light#3@(1061,14) | chính | gợi ý edge_zone = bật (tâm box ngoài 80 % bán kính; tự kiểm lại) |
| 26 | QC1-11 | B05 | traffic_light#4@(1072,16) | chính | gợi ý edge_zone = bật (tâm box ngoài 80 % bán kính; tự kiểm lại) |
| 27 | QC1-03 | B06 | lane#0@(993,264) | nặng | camera hai bên: lane phải có position = other |
| 28 | QC1-03 | B06 | lane#5@(927,500) | nặng | camera hai bên: lane phải có position = other |
| 29 | QC1-01 | B07 | tag | nặng | camera: camera = fisheye_left, tên file gợi ý fisheye_right |
| 30 | QC1-03 | B07 | lane#0@(672,125) | nặng | camera hai bên: lane phải có position = other |
| 31 | QC1-03 | B07 | lane#4@(81,758) | nặng | camera hai bên: lane phải có position = other |
| 32 | QC1-03 | B07 | lane#5@(958,273) | nặng | camera hai bên: lane phải có position = other |
| 33 | QC1-03 | B07 | lane#6@(74,712) | nặng | camera hai bên: lane phải có position = other |
| 34 | QC1-05 | B07 | lane | chính | 2 polyline cùng position L2: vạch đứt có bị tách không? |
| 35 | QC1-05 | B07 | lane | chính | 2 polyline cùng position L1: vạch đứt có bị tách không? |
| 36 | QC1-03 | B08 | lane#0@(210,628) | nặng | camera hai bên: lane phải có position = other |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Ảnh không có vạch kẻ nhìn thấy (đường có xe đỗ hai bên); không vẽ L1/R1 có được miễn QC1-02 không? | chưa có |
| A06, A07, A09 | Một bên đường là lề, không thấy vạch; không vẽ R1 (A06, A09) hoặc L1 (A07) có được miễn không? | chưa có |
| B04, B07 | Tag camera đang ghi `fisheye_front` (B04, tên `_RV`) và `fisheye_left` (B07, tên `_MVR`); tôi chưa sửa | chưa có |

## Quyết định
Lỗi nặng: 15   Lỗi chính: 14 / 332 nhãn = 4,2 %   Lỗi nhẹ: 7   Ca chờ lead: 3  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): còn lỗi nặng (QC1-01 ×2, QC1-02 ×5, QC1-03 ×8) nên quyết định là Rework, dù tỉ lệ lỗi chính dưới 5 %. 

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
