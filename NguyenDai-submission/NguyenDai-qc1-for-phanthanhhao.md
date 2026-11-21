# Phiếu QC 1 — Road v1.0

Lô được kiểm: Phan Thanh Hào (`phanthanhhao`) · Người kiểm: Nguyễn Đại  
Ngày: 21/11/2026 · Guideline: Road v1.0  
File được kiểm: `phanthanhhao-front.zip`, `phanthanhhao-fisheye.zip`; manifest `phanthanhhao-manifest.json`, revision 1.  
Số ảnh kiểm: **6 ảnh bắt buộc** (A01, A05, A06, B02, B06, B07), 0 ảnh thêm.  
Số nhãn đã kiểm: **75** = 51 shape + 24 tag. Số mục ở từng mã có thể trùng vì một nhãn được kiểm theo nhiều quy tắc.

## Tổng hợp theo mã

| Mã | Loại lỗi | Số mục kiểm | Số lỗi xác nhận | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 ảnh | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 8 vị trí trên 4 ảnh front/fisheye_front | 0; 3 cảnh báo chờ coach | nặng |
| QC1-03 position / lane thừa | sai thuộc tính / thừa | 14 lane | 3 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 14 lane | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 14 lane | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 14 lane | 1 | chính |
| QC1-07 vùng lái / crosswalk | sai phạm vi / bỏ sót / thừa | 13 polygon | 0 | chính |
| QC1-08 đèn, màu | sai phạm vi / sai thuộc tính | 8 đèn | 1 | chính (lỗi trong mẫu) |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 13 đèn/biển | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 5 biển | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 18 shape fisheye | 2 | chính |
| QC1-12 file | lỗi file | 2 ZIP + manifest | 0 | nhẹ / nặng |

## Danh sách lỗi xác nhận

| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-03 | A01 | `lane` #6 | nặng | Chồng lên `lane` #2 cùng vạch L2; xóa shape thừa. |
| 2 | QC1-06 | A01 | `lane` #2 | chính | Vạch trắng liền đơn nhưng `kind=double`; đổi thành `single`. |
| 3 | QC1-03 | A06 | `lane` #1 | nặng | Đoạn ngang trên vùng crosswalk bị gán thành vạch làn. |
| 4 | QC1-03 | A06 | `lane` #16 | nặng | Đoạn ngang trên vùng crosswalk bị gán thành vạch làn. |
| 5 | QC1-08 | B02 | `traffic_light` #7 | chính | Box bao mặt người và nền ngoài vỏ đèn; cần thu sát vỏ. |
| 6 | QC1-11 | B06 | `crosswalk` #2 | chính | Polygon tràn lên thân xe phía dưới trái. |
| 7 | QC1-11 | B07 | `drivable` #5 | chính | Polygon tràn lên thân xe phía dưới trái. |

ID shape là thứ tự 0-based của các shape trong thẻ `<image>` thuộc XML export, không tính bốn tag. Ảnh phủ nhãn và giải thích chi tiết được lưu trong hồ sơ kiểm chéo nội bộ; danh sách lỗi và quyết định nằm đầy đủ trong phiếu này.

## Ca mơ hồ / cần coach

| Ảnh | Câu hỏi cho lead | Lời đáp |
| --- | --- | --- |
| A05 | Ảnh không thấy vạch sơn hai bên làn; có xác nhận miễn QC1-02 thiếu L1/R1 không? | Chưa có. |
| A06 | Có vạch R1 nhìn thấy ở giao lộ này hay không, hay lint QC1-02 được miễn? | Chưa có. |

## Kiểm file và manifest

Hai ZIP đều mở được bằng `road_check lint`, mỗi ZIP chỉ chứa `annotations.xml`, không chứa ảnh. SHA-256 và số byte khớp manifest revision 1. File front có 16 ảnh, file fisheye có 12 ảnh; không trùng tên ảnh; mỗi ảnh có đủ bốn tag. Manifest ghi 4 cảnh báo nặng, 5 chính, 14 nhẹ cho **toàn bộ 28 ảnh**; đó là cảnh báo lint, không phải số lỗi đã xác nhận trong mẫu này.

## Quyết định

**Lỗi nặng đã xác nhận: 3. Lỗi chính đã xác nhận: 4 / 75 nhãn = 5,33 %. Lỗi nhẹ: 0. Ca chờ lead: 2 ảnh (3 vị trí L1/R1).**  
**Quyết định: Rework.** Chỉ một lỗi nặng đã đủ để trả sửa theo thang QC 1; mẫu này có ba. Tỉ lệ lỗi chính cũng vượt 5 %. Các cảnh báo QC1-02 cần coach xác nhận nhưng không làm thay đổi quyết định Rework hiện tại. Sau khi sửa trên CVAT, cần export lại, tăng revision và kiểm lại mẫu.
