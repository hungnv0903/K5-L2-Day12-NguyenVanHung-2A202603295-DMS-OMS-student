# TEAM — Ngày 12

Mã bộ ảnh: **G09** · Hình thức: nhóm

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Nguyễn Văn Hùng | 2A202603295 | có | Nguyễn Xuân Lam (2A202604051) | 35 |
| Nguyễn Xuân Lam | 2A202604051 | có | Nguyễn Văn Hùng (2A202603295) | 35 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- Ảnh `S02_rgb.png`, ghế `rear_left`: xuất hiện mô hình trẻ em ngồi trong ghế trẻ em, nhưng guideline v1.0 chỉ có `child_seat` với `occupied: no/unknown` và không có nhãn `person`/`child` cho trẻ em. Hai bạn thống nhất tạm gán `child_seat` với `occupied = unknown` và đưa vào câu hỏi leo thang của `class_list_v0.md`.

## Cá nhân

### NguyenVanHung-2A202603295
- Phần mình làm: Tự gán trọn vẹn 22 khung hình cốt lõi (16 OMS, 6 DMS), chạy script tự kiểm tra Checkpoint A/B và Final đạt 0 lỗi; thực hiện diff và phân tích 35 điểm bất đồng với bạn Nguyễn Xuân Lam.
- Điều mình học được hôm nay: Hiểu sâu sắc sự khác biệt giữa cảm biến hồng ngoại thật (NIR của Drive&Act) và ảnh hồng ngoại mô phỏng (IR-sim của SVIRO); thành thạo nguyên tắc định vị ghế theo xe và nhận thức rõ tầm quan trọng của việc đánh cờ che khuất (occluded) cho các điểm mốc mặt khi gặp đốm chói kính.
