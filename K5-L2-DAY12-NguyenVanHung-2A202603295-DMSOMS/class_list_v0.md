# Danh sách lớp v0 — Nguyễn Văn Hùng · G09

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `face` | toạ độ box [x1, y1, x2, y2] | Xác định vùng đầu/mặt tài xế, làm vùng quan tâm (ROI) để cắt ảnh đưa vào các mạng con ước lượng tư thế đầu (head pose) và theo dõi mắt | Có, hiển thị rõ viền khuôn mặt |
| 2 | `eye_state` | open / closed / unknown | Tính toán chỉ số PERCLOS (tỷ lệ thời gian mí mắt nhắm) để phát hiện tài xế ngủ gật (Drowsiness detection) và đưa ra cảnh báo âm thanh/rung vô lăng | Có, trừ trường hợp bị đốm phản xạ đèn LED trên tròng kính che khuất |
| 3 | `gaze_zone` | road, mirror_l, mirror_r, mirror_c, cluster, center, lap, other | Giám sát vùng nhìn của mắt và hướng quay đầu để phát hiện xao nhãng (Distraction detection) khi tài xế nhìn lệch khỏi mặt đường quá 2–3 giây | Có (kết hợp hướng nhìn con ngươi và hướng mặt) |
| 4 | `hand_on_wheel` | yes / no / unknown | Giám sát trạng thái giữ vô lăng khi xe chạy chế độ hỗ trợ lái (ADAS Level 2), kích hoạt cảnh báo rảnh tay (Hands-off warning) buộc tài xế đặt tay lại vô lăng | Có, NIR bắt nét tốt hình dáng bàn tay và ngón tay |
| 5 | `phone` (phone_state) | held / mounted / lap | Phát hiện hành vi sử dụng điện thoại khi đang lái xe (áp tai hoặc nhìn màn hình), cảnh báo vi phạm an toàn giao thông | Có nếu thấy cạnh/viền máy phản xạ hoặc màn hình phát sáng |
| 6 | `face13` (skeleton 13 keypoints) | 13 toạ độ điểm + cờ occluded/outside | Tính toán tỉ số khung mắt EAR (Eye Aspect Ratio) đo viền mí mắt mở và MAR (Mouth Aspect Ratio) đo độ mở miệng để phát hiện ngáp | Có, cần bật cờ che khuất (occluded) khi bị phản xạ kính hoặc góc nghiêng |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` (occupant_presence) | theo vị trí ghế: rear_left, rear_middle, rear_right | Nhận diện có người ngồi trên ghế sau để kích hoạt hệ thống nhắc thắt dây an toàn (Seatbelt Reminder - SBR) và định tuyến điều hòa | Có, nhận biết theo dáng người |
| 2 | `seatbelt` | worn_correct / worn_incorrect / not_worn / unknown | Kiểm tra hành khách thắt dây đúng chuẩn hay không, phát hiện hành vi luồn dây sau lưng để đối phó chốt cảnh báo | Có, nhưng trên nền áo tối màu sẽ khó phân biệt hơn ảnh màu RGB |
| 3 | `child_seat` | theo ghế; occupied: no / unknown | Nhận diện ghế trẻ em lắp trên xe để điều chỉnh lực bung túi khí phù hợp và kích hoạt tính năng kiểm tra ghế sau trước khi khóa cửa | Có (nhận diện theo khung nhựa và đệm ghế ngồi) |
| 4 | `infant_seat` | theo ghế; facing: rear / front | Phát hiện nôi xách em bé sơ sinh để cảnh báo vô hiệu hóa túi khí (nếu đặt ghế trước) hoặc cảnh báo chống bỏ quên trẻ nhỏ (Child Presence Detection - CPD) | Có (hình dáng nôi cong hình quả trứng đặc trưng) |
| 5 | `object` | theo ghế; type: bag / box / cup / other | Phát hiện đồ vật giá trị (balo, laptop, túi xách) bị bỏ quên trên xe khi tắt máy, gửi thông báo cảnh báo qua ứng dụng điện thoại của chủ xe | Có (theo hình khối của vật) |
| 6 | `camera_blocked` | yes / no | Tự chẩn đoán tình trạng camera OMS trong khoang lái bị hành lý che lấp hoặc ống kính bị bám bẩn để thông báo bảo trì cảm biến | Có (toàn bộ khung hình bị mất chi tiết hoặc tối sầm) |

## 2 câu hỏi leo thang

Câu hỏi bạn muốn hỏi người viết guideline (hoặc khách hàng) vì guideline v1.0 chưa trả lời. Mỗi câu kèm **tên khung** làm ví dụ.

1. **Câu hỏi:** Trong ảnh có mô hình trẻ em ngồi trong ghế trẻ em, hệ thống OMS cần phân biệt ghế trẻ em có người (`child_seat_occupied`) và ghế trẻ em trống (`child_seat_empty`) như thế nào khi Guideline v1.0 chỉ cho phép `child_seat` có thuộc tính `occupied = no/unknown` và không cho phép vẽ `person` cho trẻ em?
   - **Khung ví dụ:** `S02_rgb.png` và `S02_ir.png` (ghế bên phải ảnh: `rear_left` của xe).
   - **Bạn tạm gán thế nào và vì sao:** Tạm gán box `child_seat` với thuộc tính `occupied = unknown` và không vẽ box `person` cho trẻ em, theo đúng quy định mục 3 của GUIDE ("Bộ ảnh không có trẻ em ngồi. Thấy hình giống trẻ em thì báo coach, không gán") để đảm bảo tuân thủ schema và không bị xung đột nhãn.

2. **Câu hỏi:** Khi đồ vật (ví dụ balo, đồ chơi) được đặt trực tiếp bên trong nôi em bé (`infant_seat`), guideline v1.0 chỉ quy định vẽ 2 box đè nhau cho `child_seat` + `object`, chưa nêu rõ quy tắc cho `infant_seat`. Trong trường hợp này có vẽ thêm box `object` không và thuộc tính `facing` của nôi có thay đổi theo chiều quay thực tế trong xe không?
   - **Khung ví dụ:** `S03_rgb.png` và `S03_ir.png` (ghế `rear_left`).
   - **Bạn tạm gán thế nào và vì sao:** Tạm thời chỉ gán 1 box `infant_seat` bao quanh nôi với `facing = front` vì nôi quay mặt về trước xe, không vẽ thêm box đè bên trong để tránh làm model nhầm lẫn giữa nôi sơ sinh có đồ vật và nôi có em bé.
