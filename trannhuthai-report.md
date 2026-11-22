# Báo cáo cá nhân — Ngày 11
Họ tên: Trần Như Thái   Mã học viên: 2A202603184  
Phiên bản CVAT (Help → About): 2.81.0
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 22/11/2026 10:57 Số lần nộp lại sau Rework: 0

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | lane/road_curb: polyline; crosswalk/drivable: polygon; traffic_light/traffic_sign: rectangle. `lint` không báo label lạ (QC1-12) |
| Thuộc tính và giá trị | Đúng | `lint` không báo thuộc tính hay giá trị sai tên |
| 4 tag ảnh | Đúng | camera, timeofday, weather, source; cả 20 ảnh đủ bốn tag |
Cách kết thúc polyline trên bản CVAT này:  phím N
Cách đặt tag ảnh trên bản CVAT này: mỗi tag là một label kiểu Tag có một thuộc tính select `value` (ví dụ `camera` với `value = fisheye_left`); trong XML là `<tag label="camera"><attribute name="value">…</attribute></tag>`.

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 35 | 25 | 5 | 25 | 38 | 48 |
| front-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 15 | 22 | 11 | 9 | 8 | 11 |
| fisheye-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

(Số liệu lấy từ `trannhuthai-manifest.json`, `shapes_by_label`.)

## 3. Bảng ca khó
Các dòng dưới đây dựa trên ảnh chụp màn hình và cảnh báo `lint`. Bạn đọc và sửa phần "Lý do" nếu khác suy nghĩ thật của bạn.

| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| B04 | drivable | Có gán vùng lái hay không, vì camera sau chụp đoạn đường xe vừa đi qua | Gán `drivable` (direct) | Guideline định nghĩa drivable là "phần mặt đường xe đi được nếu đường trống", tính theo mặt đường trong ảnh; bảng kế hoạch B04 yêu cầu drivable |
| B04 | drivable / crosswalk | Vùng lái có gồm vạch ngựa vằn không, vì hai polygon chồng lên nhau | Polygon drivable bao cả vùng vạch ngựa vằn | Vạch ngựa vằn nằm trên mặt đường xe đi được; ghi riêng thêm crosswalk |
| A05 | lane | Vẽ lane hay bỏ qua | Không vẽ L1/R1 | Ảnh có xe đỗ hai bên, không thấy vạch kẻ trên mặt đường (xem ảnh chụp A05); đã ghi vào phiếu QC 1 để hỏi coach |
| A06, A09 | lane | Có vẽ R1 không | Không vẽ R1 | Bên phải chỉ có lề đường, không thấy vạch; cần coach xác nhận |
| A07 | lane | Có vẽ L1 không | Không vẽ L1 | Bên trái là dải phân cách bê tông, không thấy vạch; cần coach xác nhận |
| A01, A08, A12, B07 | lane | Hai polyline cùng `position` là một vạch đứt bị tách hay hai vạch khác nhau | Giữ nguyên | Lint cảnh báo QC1-05; tôi chưa kiểm lại từng ảnh |

## 4. Phiếu QC 1 nhận được

| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-01 tag camera (nặng) | 2 | Đồng ý: B04 (`_RV`) ghi `fisheye_front`, B07 (`_MVR`) ghi `fisheye_left`, sai so với hậu tố tên ảnh | Chưa |
| QC1-02 thiếu L1/R1 (nặng) | 5 | Một phần: A05, A06, A07, A09 có thể không thấy vạch; chờ coach xác nhận để được miễn | Chưa |
| QC1-03 position ở camera hai bên (nặng) | 8 | Đồng ý: lane ở B05–B08 phải có `position = other` | Chưa |
| QC1-04 chiều vẽ (chính) | 1 | Cần kiểm lại: A03 lane#11, điểm đầu cao hơn điểm cuối | Chưa |
| QC1-05 vạch đứt bị tách (chính) | 5 | Cần kiểm lại: A01, A08, A12, B07 (×2) có hai polyline cùng `position` | Chưa |
| QC1-08 đèn, box thấp hơn 8 px (nhẹ) | 3 | Không bắt buộc theo guideline | Chưa |
| QC1-10 biển, box thấp hơn 8 px (nhẹ) | 4 | Không bắt buộc theo guideline | Chưa |
| QC1-11 fisheye (chính) | 8 | Cần kiểm lại: 2 road_curb chỉ có 2 điểm ở B02; 6 gợi ý bật `edge_zone` | Chưa |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| trannhuthai-front.zip | Có (`lint` đọc được 12 ảnh) | A01: 10/10 | A02: 8/8 | Có, 12/12 ảnh |
| trannhuthai-fisheye.zip | Có (`lint` đọc được 8 ảnh) | B01: 8/8 | B02: 13/13 | Có, 8/8 ảnh; B04 và B07 sai giá trị, xem mục 7 |

Manifest: `contains_images = false` cho cả hai zip.  
Kết quả `lint` lần nộp này: 36 cảnh báo, gồm 15 nặng, 14 chính, 7 nhẹ.

## 6. Ảnh chụp màn hình
1. Tab Labels của project: ![Labels](screenshots/01-labels.png)
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển), ở đây là A08: ![A08](screenshots/02-front-A08.png)
3. Một ảnh fisheye đã gán, polyline cong: ![B07](screenshots/03-fisheye-B07-curve.png) (B07, camera phải; polyline `road_curb` đi theo cung). Ảnh B04: ![B04](screenshots/04-fisheye-B04.png)
4. Một đoạn XML có `<polyline label="lane">` (từ `trannhuthai-front.zip`, ảnh A01):
```xml
<polyline label="lane" source="manual" occluded="0" points="1280.00,709.64;907.91,617.45;672.31,559.14;576.12,535.94;512.29,521.84;463.24,510.39" z_order="0">
  <attribute name="position">L2</attribute>
  <attribute name="style">solid</attribute>
  <attribute name="color">white</attribute>
  <attribute name="kind">single</attribute>
</polyline>
```
Điểm đầu có y = 709,64 (gần xe) và điểm cuối có y = 463,24 (xa xe), nên polyline vẽ từ gần ra xa.

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:

Theo `lint` trên bài nộp, số cảnh báo theo mã là: QC1-03 (8), QC1-11 (8), QC1-02 (5), QC1-05 (5), QC1-01 (2), QC1-04 (1), QC1-08 và QC1-10 nhẹ (7). Lỗi nặng nhiều nhất là **QC1-03**: ở bốn ảnh camera trái/phải (B05–B08) có 8 polyline lane chưa đặt `position = other`, vì CVAT tự điền giá trị đầu danh sách. Cách tránh ở Ngày 20: đặt giá trị mặc định đúng cho thuộc tính ngay khi vẽ, và chạy `lint` sau mỗi nhóm ảnh thay vì chờ đến cuối. Hai ảnh B04 và B07 bị đặt sai tag camera (QC1-01); cách tránh là đối chiếu hậu tố tên ảnh (FV, RV, MVL, MVR) với tag ngay khi đặt tag.

Nhãn của bạn đi vào model ở đâu? Chọn một lỗi và nói nó làm model học sai thế nào:

Lấy lỗi QC1-03. Ở camera trái/phải, vạch ngoài đời nằm ngang tầm nhìn, nên khái niệm "làn bên trái/bên phải của xe" (L1, R1) không áp dụng. Nếu nhãn ghi L1/R1 ở những ảnh này, model học làn có vị trí ngữ nghĩa từ góc nhìn bên hông, nên có thể gán sai vai trò làn khi suy luận ở camera bên và làm nhiễu việc học vị trí làn ở camera trước và sau. Lỗi QC1-01 (sai tag camera) làm model gộp nhầm ảnh của hai camera khác nhau vào cùng một nhóm. 
## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
Không.
