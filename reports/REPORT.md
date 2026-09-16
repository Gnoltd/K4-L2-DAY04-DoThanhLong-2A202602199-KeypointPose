# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Do Thanh Long   Nhóm: SOLO   Ngày: 2026-09-16

> Cách dùng: copy file này thành `reports/REPORT.md`. Điền bằng số liệu do công cụ sinh ra;
> không tự ước lượng hoặc sửa số trong file JSON.

## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán | 20 |
| Số skeleton | 29 |
| v=2 / v=1 / v=0 | 329 / 26 / 133 |
| Thời gian trung bình mỗi ảnh |8-10 phút |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1. left_hip (17%)
2. right_ankle (17%)
3. right_knee (14%)

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.

Đúng một phần, nhưng vì hai lý do khác nhau. left_hip khó vì khó xác định vị trí giải phẫu: trong các ảnh người mặc quần dài ngồi trên xe máy/xe đạp (vd. train_09), hông không hề có bề mặt nào lộ ra qua quần áo nên luôn phải ước lượng theo tỷ lệ cơ thể, không có cách nào "nhìn thấy rõ hơn" dù zoom kỹ đến đâu. right_ankle/right_knee thì khó vì hay bị che bởi vật thể trong cảnh (thân xe máy, fender, khung xe - vd. train_15 chân trái bị bánh trước xe máy che) chứ không phải vì vị trí giải phẫu mơ hồ - nếu bỏ chiếc xe đi thì chân vẫn thấy rõ bình thường.

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình | 0.806 | 0.8472 |
| OKS@0.50 | 0.966 | 1.0000 |
| OKS@0.75 | 0.690 | 0.7931 |
| Lỗi `dao_trai_phai` | 1 | 0 |
| Lỗi `nham_nguoi` | 0 | 0 |
| Lỗi `xoa_khop_bi_che` | 25 | 22 |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

<!-- Mỗi dòng phải có: tên ảnh + người thứ mấy + keypoint + thao tác sửa. Không viết “đã sửa
lại một số lỗi”. -->

- train_13.txt, [Người thứ 3 + right_wrist]: sửa lỗi `dao_trai_phai` do ảnh mờ khó xác định trái/phải.

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?

<!-- Nếu không có lỗi, ghi rõ “Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh.” -->

Có 1 lỗi đảo trái/phải trước rework, ở `train_13.jpg`. Ảnh này khó: người bị mờ (motion
blur/độ phân giải thấp), khiến khó xác định chính xác bên trái/phải cơ thể khi tư thế
không rõ ràng. Đã sửa lại và lỗi này không còn xuất hiện ở lần chạy sau rework
(`dao_trai_phai` giảm từ 1 → 0).

## 3. Kiểm chéo

Bạn cùng nhóm: N/A - làm solo, không có bạn cùng nhóm để kiểm chéo nhãn.

Khớp lệch `%v=1` nhiều nhất giữa hai bảng đếm:

| Khớp | Bạn | Họ | Lệch | Nguyên nhân (guideline hay gán sai?) |
| --- | ---: | ---: | ---: | --- |
| N/A | N/A | N/A | N/A | N/A - không có bạn cùng nhóm |

Luật mới đã bổ sung vào `GUIDELINE_MINI.md` sau khi thống nhất:

<!-- Viết một rule kiểm chứng được: điều kiện nhìn thấy/căn cứ vị trí → chọn v=1 hoặc v=0.
Không chỉ ghi “cẩn thận hơn khi gán”. -->

- N/A - làm solo, không có bạn cùng nhóm để đối chiếu và thống nhất luật mới.

## 4. Model

<!-- Chép số từ outputs/eval_model.json sau Chặng 6. “Chênh” = sau fine-tune trừ baseline;
đây là quan sát trên tập test, không phải chất lượng sản phẩm. -->

| Chỉ số | yolo26n-pose gốc | Sau fine-tune | Chênh |
| --- | ---: | ---: | ---: |
| pose_mAP50 | 0.8450 | 0.8450 | +0.0000 |
| pose_mAP50-95 | 0.6853 | 0.6853 | +0.0000 |
| pose_precision | 0.9734 | 0.9746 | +0.0012 |
| pose_recall | 0.8462 | 0.8462 | +0.0000 |
| box_mAP50-95 | 0.8119 | 0.8054 | -0.0065 |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model
   điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?

   `pose_mAP50-95` không đổi: 0.6853 → 0.6853 (chênh = 0.0000). `yolo26n-pose` gốc đã
   được train trên COCO nên đã "biết" cả bộ 17 điểm lẫn phần lớn tư thế xuất hiện trong
   10 ảnh test - 20 ảnh fine-tune quá ít để đo được thay đổi ở mức OKS. Đáng chú ý hơn:
   `box_mAP50-95` lại giảm nhẹ (0.8119 → 0.8054, chênh -0.0065), cho thấy fine-tune trên
   tập nhỏ hơi làm lệch khả năng định vị hộp bao, dù độ chính xác khớp giữ nguyên.

2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm
   *khớp* dễ hơn? Vì sao?

   Chênh khoảng 0.12-0.13 (`box_mAP50-95` ~0.81 so với `pose_mAP50-95` 0.6853). Model
   tìm *người* dễ hơn tìm *khớp* rõ rệt: một hộp bao chỉ cần đúng vị trí và kích thước
   tổng thể, còn OKS của pose đòi hỏi định vị chính xác từng khớp nhỏ (cổ tay, mắt cá)
   - những điểm dễ bị che khuất hoặc mờ do chuyển động.

3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
   (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn):

   `test_03.jpg` (đua mô tô địa hình, 2 người): OKS chỉ 0.234 và 0.183 - thấp hơn hẳn
   8 ảnh test còn lại (đều >0.9). So `outputs/runs/predictions/test/test_03.jpg` với
   nhãn thật (`dataset/labels/test/test_03.txt`): các khớp model đoán dồn cụm quanh
   vùng đầu/vai thay vì trải dọc theo tư thế nghiêng người đua xe thực tế → **trượt
   hẳn**, không phải lệch nhẹ hay đảo trái/phải.

4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?

   `train_13.jpg` (OKS = 0.602, thấp nhất trong toàn bộ tập train khi so model với nhãn
   của bạn). Đáng chú ý: khi chấm với gold, `train_13.jpg` cũng nằm trong nhóm OKS thấp
   (0.7079, thấp thứ 6/29, dưới mức trung bình 0.8472) - có cơ sở để nghiêng về hướng
   đây là một ảnh khó (nhiều che khuất) khiến cả bạn lẫn model đều khó chấm đúng, chứ
   không chỉ do model kém. Cần mở ảnh này bằng `tools/visualize_pose.py` để xác nhận
   bằng mắt trước khi kết luận ai đúng.

5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
   nói gì về bức ảnh đó?

   Không hoàn toàn trùng: ảnh gán tệ nhất so với gold là `train_15.jpg` người #1
   (OKS = 0.623, tệ nhất trong 29 skeleton), còn ảnh model đoán tệ nhất so với nhãn của
   bạn là `train_13.jpg` (OKS = 0.602). Hai ảnh khác nhau nhưng đều nằm trong nhóm OKS
   thấp nhất ở cả hai bảng xếp hạng - gợi ý cả hai đều là ảnh khó thật (nhiều che khuất/
   tư thế lạ) chứ không phải một lỗi ngẫu nhiên. `train_15.jpg` người #1 chính là Ca 3
   trong `GUIDELINE_MINI.md` (chân trái bị xe máy che khuất).

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

<!-- Cấu trúc gợi ý: (1) train_XX + người thứ mấy + keypoint; (2) căn cứ thị giác như phần cơ
thể liền kề, trang phục hoặc vật che; (3) vì sao khớp còn trong khung (v=1) hay đã ra khỏi
khung (v=0). -->

`train_09.txt`, người #1 (người lái xe máy quay lưng về phía máy ảnh), khớp `right_hip`.
Bằng chứng nhìn thấy: vai trái, vai phải và hông trái đều lộ rõ trong khung, cho thấy toàn
bộ phần thân dưới - kể cả bên phải - vẫn nằm trong ảnh, chỉ là hông phải bị chính thân
người và ba lô che khuất do góc chụp từ phía sau. Tôi chọn `v=1` và đặt chấm ước lượng đối
xứng với hông trái (0.378, 0.679) qua trục dọc thân người, ra khoảng (0.448, 0.682), vì vật
cản ở đây là thân người - nằm trong khung ảnh - chứ không phải mép ảnh. Nếu để `v=0`, khớp
này sẽ bị loại thẳng khỏi phép tính OKS dù nó chắc chắn tồn tại trong ảnh, đúng loại lỗi
"xoá khớp bị che" mà rubric cảnh báo.
