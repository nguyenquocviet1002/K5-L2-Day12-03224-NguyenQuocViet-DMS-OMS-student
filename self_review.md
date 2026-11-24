# Tự đánh giá — Nguyễn Quốc Việt · G10

## 1. Tự rà soát 4 cảnh

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| `S01_rgb.png` | `child_seat` | `seat_flip` | `cabin_check.py` cảnh báo `seat=driver` trên ảnh SVIRO (camera chỉ nhìn hàng ghế sau) | Ghi nhận (giải thích ở `check_final.txt`) |
| `S03_ir.png` | `person` | `seat_flip` | Cảnh báo `seat=driver` trên ảnh SVIRO hàng ghế sau | Ghi nhận (giải thích ở `check_final.txt`) |
| `D01.png` | `face` | `ok` | Giữ `eye_left=unknown` khi không thấy rõ, không đoán | Không cần sửa |
| `D02.png` | `face` | `ok` | Thấy rõ không đeo kính (`glasses=none`), các điểm `face13` đúng phía trái/phải theo người lái | Không cần sửa |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Gán nhầm `seat=driver` cho một số đối tượng trên ảnh SVIRO (`S01_rgb`, `S03_ir/rgb`, `S07_ir/rgb`) và để `light` khác `unknown` trên ảnh dựng SVIRO.

Vì sao mình mắc: Chưa kiểm tra kỹ góc nhìn của camera OMS (chỉ nhìn hàng ghế sau) trước khi chọn thuộc tính `seat`, và quen tay đánh giá độ sáng theo mắt thường trên ảnh dựng.

Lần sau tránh bằng cách: Luôn xác định vị trí camera (DMS vs OMS hàng ghế sau) trước khi gán `seat`, và chạy `cabin_check.py` ngay sau mỗi checkpoint để sửa sớm.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai (hoặc cần lưu ý nhất): Ở `S03_ir.png` (`seatbelt`: mình gán `unknown`, peer gán `not_worn`). Mình học được rằng trên ảnh IR vùng áo tối rất dễ gây nhầm lẫn nếu đoán `not_worn`; khi không thấy rõ dây an toàn thì giữ `unknown` theo đúng guideline để tránh tạo nhãn sai cho model.
