# Visibility report

- Thư mục nhãn: `dataset/labels/train`
- 20 ảnh, 29 skeleton, trung bình 12.24 khớp có v > 0 mỗi người
- Tổng: v=2 329 | v=1 26 | v=0 138

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 22 | 0 | 7 | 0% |
| 1 | left_eye | 20 | 0 | 9 | 0% |
| 2 | right_eye | 20 | 0 | 9 | 0% |
| 3 | left_ear | 10 | 2 | 17 | 7% |
| 4 | right_ear | 14 | 1 | 14 | 3% |
| 5 | left_shoulder | 26 | 1 | 2 | 3% |
| 6 | right_shoulder | 28 | 0 | 1 | 0% |
| 7 | left_elbow | 22 | 1 | 6 | 3% |
| 8 | right_elbow | 24 | 1 | 4 | 3% |
| 9 | left_wrist | 20 | 2 | 7 | 7% |
| 10 | right_wrist | 20 | 1 | 8 | 3% |
| 11 | left_hip | 19 | 5 | 5 | 17% |
| 12 | right_hip | 23 | 2 | 4 | 7% |
| 13 | left_knee | 16 | 1 | 12 | 3% |
| 14 | right_knee | 16 | 4 | 9 | 14% |
| 15 | left_ankle | 16 | 0 | 13 | 0% |
| 16 | right_ankle | 13 | 5 | 11 | 17% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
