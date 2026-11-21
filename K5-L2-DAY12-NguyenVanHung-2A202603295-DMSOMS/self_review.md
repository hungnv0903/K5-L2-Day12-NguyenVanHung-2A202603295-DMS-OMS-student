# Tự đánh giá — Nguyễn Văn Hùng · G09

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S02_rgb.png | person (ghế trái ảnh) | `seat_flip` | Thuộc tính seat ban đầu để sót mặc định là driver, cần sửa về rear_right | Đã sửa |
| S04_rgb.png | person (ghế phải ảnh) | `seat_flip` | Box person ban đầu bị để mặc định seat=driver, đã đổi sang rear_left | Đã sửa |
| D01.png | face13 (mắt trái) | `ok` | Khóe mắt và mí mắt đã đặt đúng chiều y lớn hơn mắt phải trên ảnh xoay 90° | Đã kiểm tra |
| D06.png | face13 (left_eye_*) | `flag` | eye_left chọn unknown nhưng thiếu cờ che khuất occluded, đã bật occluded=1 | Đã sửa |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

- **Lỗi:** Quên đổi thuộc tính vị trí ghế (`seat`) sau khi vẽ box `person` trên nhóm ảnh SVIRO, dẫn đến giá trị bị lưu mặc định là `driver`.
- **Vì sao mình mắc:** CVAT luôn tự động gán giá trị đầu tiên trong danh sách (`driver`) cho mọi box mới tạo; khi tập trung căn chỉnh khung viền khít mép thì dễ bỏ sót kiểm tra tab DETAILS.
- **Lần sau tránh bằng cách:** Tạo thói quen ngay sau khi vẽ xong hình hộp là chuyển mắt sang tab DETAILS bên phải để kiểm tra và chọn ngay đúng vị trí ghế theo xe (`rear_left` / `rear_middle` / `rear_right`).

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó:

- Tại ảnh `S02_rgb.png` và `S04_rgb.png`, bạn Nguyễn Xuân Lam gán `seatbelt = not_worn` trong khi tôi gán `unknown`. Sau khi đối chiếu lại guideline và phóng to quan sát, người lớn trong ảnh mặc áo màu sáng và thấy rõ hoàn toàn không có dải dây an toàn vắt chéo qua vai/ngực. Bộ dữ liệu SVIRO cũng khẳng định không có nhân vật nào thắt dây an toàn. Tôi học được rằng khi đã nhìn thấy rõ phần thân người không có dây thì nên gán dứt khoát `not_worn` thay vì lạm dụng `unknown`.
