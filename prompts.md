# Khai báo dùng AI — Nguyễn Văn Hùng

Nhắc lại: không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Antigravity AI | Hỏi về quy ước định hướng mắt trái/phải trên ảnh Drive&Act xoay ngang 90° và cách kéo 13 điểm skeleton `face13` | Áp dụng quy tắc trục y lớn hơn cho mắt trái và kéo từng keypoint vào đúng vị trí giải phẫu | Có, kiểm lại bằng script `cabin_check.py` ở Checkpoint B (đạt 0 lỗi) |
| 2 | Antigravity AI | Hỏi về cách xử lý khi mắt bị gọng kính che và quy tắc bật cờ che khuất (`occluded`) | Ghi `eye = unknown` nếu không thấy mí mắt và bật cờ `occluded = 1` cho các điểm mốc bị che | Có, kiểm lại qua hàm `check_eye_flags` của script `cabin_check.py` |
| 3 | Antigravity AI | Hỏi về cách phân biệt ghế em bé (`infant_seat`) và ghế trẻ em (`child_seat`), cũng như hướng `facing` của nôi xách trong OMS | Gán đúng nhãn `infant_seat` với hướng `facing = front` cho nôi ở ảnh S03 tựa lưng vào ghế xe | Có, đối chiếu với cấu trúc nhãn của file `labels_cabin_v1.json` và rubric |
