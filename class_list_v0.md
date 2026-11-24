# Danh sách lớp v0 — Nguyễn Quốc Việt · G10

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `face` / `face13` | bbox + 13 điểm mốc | Theo dõi vị trí đầu, hướng nhìn (yaw/pitch) và làm cơ sở phát hiện mất tập trung | Có |
| 2 | `eye_left` / `eye_right` | `open` / `closed` / `unknown` | Phát hiện buồn ngủ, nhắm mắt lâu (PERCLOS) | Có, trừ khi kính phản xạ LED |
| 3 | `glasses` | `none` / `clear` / `sunglasses` / `unknown` | Đánh giá độ tin cậy của nhận diện mắt (kính râm hoặc phản xạ làm giảm độ chính xác) | Có (kính râm/phản xạ thấy rõ) |
| 4 | `gaze_zone` | `road` / `mirror` / `center_stack` / `phone` / `unknown` | Xác định tài xế có đang nhìn đường hay liếc sang màn hình/điện thoại | Có (dựa theo hướng đầu và mắt) |
| 5 | `hand` (`on_wheel`) | `yes` / `no` / `unknown` | Giám sát trạng thái cầm vô lăng để cảnh báo khi xe yêu cầu tài xế nắm tay lái | Có |
| 6 | `phone` | bbox | Phát hiện hành vi cầm/sử dụng điện thoại gây mất tập trung khi lái xe | Có (khi thấy rõ vật thể) |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` | bbox + `seat` | Đếm số hành khách và xác định vị trí ngồi để điều chỉnh túi khí/điều hòa | Có |
| 2 | `child_seat` | bbox + `seat` | Nhận biết ghế trẻ em để cảnh báo quên trẻ hoặc vô hiệu hóa túi khí phù hợp | Có (hình dạng) |
| 3 | `infant_seat` | bbox + `seat` | Phân biệt nôi trẻ sơ sinh (thường quay ngược) để tắt túi khí ghế trước/cảnh báo bỏ quên | Có (hình dạng) |
| 4 | `seatbelt` | `worn` / `not_worn` / `unknown` | Cảnh báo hành khách chưa thắt dây an toàn | Hạn chế (khó thấy trên áo tối) |
| 5 | `object` | bbox | Phát hiện vật thể bỏ quên trên ghế sau (túi xách, đồ vật) hoặc vật cản trên ghế | Có |
| 6 | `frame_meta` (`light`) | `day` / `night` / `unknown` | Phân loại điều kiện ánh sáng của khung hình để đánh giá hiệu năng model theo môi trường | Không áp dụng trực tiếp (tag cấp ảnh) |

## 2 câu hỏi leo thang

1. Câu hỏi: Khi ảnh SVIRO là ảnh dựng tổng hợp (synthetic), thuộc tính `light` của `frame_meta` nên bắt buộc gán `unknown` hay gán theo độ sáng trực quan của ảnh RGB?
   Khung ví dụ: `S01_rgb.png`, `S01_ir.png`
   Bạn tạm gán thế nào và vì sao: Tạm giữ nhất quán theo cặp RGB/IR và ghi chú giải thích ở `check_final.txt` vì `cabin_check.py` chỉ phát cảnh báo `[WARN]` chứ không báo lỗi.
2. Câu hỏi: Trên ảnh IR thật khi tròng kính có đốm phản xạ LED che một phần mắt nhưng vẫn thấy mí mắt hơi khép, ngưỡng nào thì được gán `closed` thay vì `unknown`?
   Khung ví dụ: `D03.png`
   Bạn tạm gán thế nào và vì sao: Tạm gán `unknown` theo nguyên tắc an toàn của guideline: không đoán khi mắt bị che bởi phản xạ LED.
