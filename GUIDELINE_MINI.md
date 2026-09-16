# Mini guideline - nhóm: SOLO |  người gán: Do Thanh Long  |  ngày: 2026-09-16

> Điền file này **trong lúc** gán nhãn, không phải sau khi xong. Mỗi lần bạn dừng lại
> hơn 10 giây để phân vân, đó là một dòng phải ghi vào đây.

## 1. Luật bắt buộc (đã thống nhất cả lớp - không sửa)

- Bộ 17 điểm COCO, đúng tên, đúng thứ tự. Lấy từ file `.SVG` chung.
- Mọi người trong ảnh đều có **đủ 17 điểm**. Điểm không dùng được thì gắn cờ, không xoá.
- Trái/phải tính theo **cơ thể người**, không theo bức ảnh.
- Bị che, còn trong khung -> `v = 1`, **vẫn đặt chấm** ở vị trí ước lượng.
- Ra ngoài mép ảnh -> `v = 0`, **không** đặt chấm.
- Không dùng `Hidden` (`h`) - nó không được lưu vào file.

## 2. Luật của nhóm bạn (phải điền)

| Tình huống | Luật nhóm bạn chọn | Vì sao |
| --- | --- | --- |
| Hông của người mặc quần áo dài | Luôn ước lượng theo tỷ lệ giải phẫu (điểm giữa đường nối vai và gối, lệch theo hướng vặn thân), gán `v=1`, không bao giờ `v=0` | Hông gần như không bao giờ lộ ra qua quần áo - GUIDE.md gọi đây là "ước lượng giải phẫu" bắt buộc; để `v=0` sẽ xoá thẳng khớp khỏi OKS dù người còn nguyên trong ảnh |
| Tai bị tóc hoặc mũ bảo hiểm che một phần | Còn thấy một phần vành tai → `v=2` tại điểm thấy được; bị che kín hoàn toàn bởi vỏ mũ cứng → `v=1`, đặt chấm ước lượng ngang tầm mắt, lùi vào trong so với viền mũ | Ví dụ thật trong bộ ảnh: `train_02` người #1 (mũ bảo hiểm xe đạp full-shell) và `train_15` người #1 (mũ bảo hiểm cụp kính) - vỏ mũ rộng hơn đầu thật nên không suy ra vị trí tai từ viền mũ như suy từ tóc, nhưng đầu vẫn "còn trong khung" |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) | Chỉ khớp thực sự vượt ra ngoài biên ảnh mới `v=0`/không chấm; nếu người dừng đúng mép ảnh, mọi khớp từ đầu gối trở xuống → `v=0` | Phân biệt với các ca bị vật khác che (ba lô, xe máy) trong `train_09`/`train_15` - ở đó vẫn phải `v=1`. Nhầm hai trường hợp này chính là lỗi số 3 của slide 46 |
| Cổ tay nằm sau tay lái / sau thân mình | `v=1`, ước lượng theo phương cẳng tay (kéo dài đoạn vai→khuỷu tay thêm một đoạn bằng chính nó theo hướng cầm lái) | Ca thật: `train_09` người #1 - ba lô và tư thế quay lưng che khuất cổ tay phải, nhưng cẳng tay vẫn nằm trong khung, chỉ là góc chụp từ sau che mất bàn tay |
| Hai người chồng lên nhau | Gán trọn 17 điểm của một người xong mới chuyển người kế tiếp; dùng hướng vai + màu trang phục để phân định khớp thuộc về ai trước khi đặt chấm | Cách duy nhất tránh lỗi "nhầm người" theo luật bắt buộc #3 của GUIDE.md; sửa lại sau khi đã đặt cả hai bộ khung dễ nhầm điểm giữa hai người tư thế gần giống nhau |
| Người nhỏ đến mức nào thì không gán nữa | Không đặt ngưỡng bỏ qua trong bộ 20 ảnh này | GUIDE.md nói rõ bộ ảnh đã được chọn để mọi người đủ lớn để gán đủ 17 điểm; gặp ca khó nhìn thì ghi vào mục 3 làm ca mơ hồ, không tự ý bỏ qua để tránh lệch `%v=1` khi so nhóm |

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `train_09`, người thứ `1`, khớp `right_elbow, right_wrist, right_knee, right_ankle` (nửa phải cơ thể)

- Mơ hồ ở chỗ nào: Người ngồi trên xe máy quay hẳn lưng về phía máy ảnh, đeo ba lô to; toàn bộ nửa phải cơ thể bị chính thân người và ba lô che kín, không còn đường viền quần áo hay chi nào lộ ra để bám vào khi ước lượng toạ độ.
- Bạn quyết thế nào: Lấy đối xứng gương qua trục dọc thân người từ nửa trái đang thấy rõ (vai trái→khuỷu trái→cổ tay trái, hông trái→gối trái→mắt cá trái), dịch sang phải đúng bằng khoảng cách vai trái-vai phải; gán `v=1` cho các khớp suy luận được theo cách này thay vì để `v=0`.
- Vì sao: Luật bắt buộc mục 1 nói rõ "bị che, còn trong khung → v=1, vẫn đặt chấm" - thân người và ba lô là vật cản nằm trong khung ảnh, không phải mép ảnh.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu để cả cụm này là `v=0`, model học rằng "người quay lưng thì không có tay/chân phải" - sai cấu trúc cơ thể chỉ vì góc chụp, và mất luôn phần đóng góp OKS của các khớp đó ở mọi ảnh chụp từ sau.

### Ca 2 - ảnh `train_02`, người thứ `1`, khớp `left_eye, right_eye, left_ear, right_ear`

- Mơ hồ ở chỗ nào: Người đi xe đạp đội mũ bảo hiểm cứng full-shell; đầu nằm gọn trong mũ, không có phần tóc hay da đầu lộ ra để suy đoán vị trí mắt/tai như với người đội mũ vải hoặc để tóc che một phần.
- Bạn quyết thế nào: Gán `v=1`, đặt chấm ước lượng theo tỷ lệ đầu người bình thường (mắt ngang ~40% chiều cao mũ tính từ đáy, tai hai bên ngang mắt) - dựa vào vị trí đầu thật, không đặt chấm lên vỏ mũ.
- Vì sao: Vỏ mũ chỉ là vật che chắn bên ngoài trong khung ảnh; đầu người vẫn "còn trong khung" đúng nghĩa Occluded, không phải "ra ngoài khung".
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu để `v=0`, model học rằng "đội mũ bảo hiểm thì không có mắt/tai" - sai nghiêm trọng vì mũ bảo hiểm rất phổ biến trong domain xe cộ của bộ dữ liệu này, khiến model mất khả năng định vị đầu ở đúng nhóm ảnh quan trọng nhất.

### Ca 3 - ảnh `train_15`, người thứ `1`, khớp `left_hip, left_knee, left_ankle`

- Mơ hồ ở chỗ nào: Người đứng cạnh xe máy ở cây xăng, đội mũ bảo hiểm cụp kính nhìn xuống; chân trái bị đúng bánh trước và fender xe máy che từ hông trở xuống, trong khi chân phải lộ hẳn ra ngoài xe.
- Bạn quyết thế nào: Gán `v=1`, ước lượng chân trái bằng cách giữ khoảng cách hông-gối-mắt cá tương tự chân phải (đang thấy rõ) nhưng dịch vào sát đường viền bánh xe/fender, vì người đứng thẳng hai chân song song.
- Vì sao: Xe máy là vật cản nằm trong khung ảnh chứ không phải biên ảnh; luật bắt buộc yêu cầu ước lượng theo giải phẫu thay vì xoá khớp chỉ vì góc chụp che khuất một bên cơ thể.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu để `v=0`, model học rằng đứng cạnh xe máy nghĩa là "chỉ có một chân" - lỗi hệ thống sẽ lặp lại ở mọi ảnh có phương tiện che một phần thân dưới, đúng loại lỗi rubric gọi là xoá khớp bị che.

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: `N/A` (bạn `N/A%` / họ `N/A%`)
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**: N/A - làm solo, không có bạn cùng nhóm để so visibility report.
- Luật mới bổ sung vào mục 2 sau khi thống nhất: N/A
