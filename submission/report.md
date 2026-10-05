# Báo cáo bonus — Lab 2D Perception

## 4C — Val gốc và val lật gương

| Model | Pose mAP50-95 — val gốc | Pose mAP50-95 — val lật gương |
|---|---|---|
| flip_idx giải phẫu | 0.457 | 0.439 |
| flip_idx đồng nhất | 0.417 | 0.298 |

Trên val gốc cùng hướng quay, Pose mAP50-95 của model giải phẫu/đồng nhất là 0.457/0.417; trên val lật gương là 0.439/0.298. Metric trên val gốc đã che lỗi vì train và val chỉ có hổ quay phải; val lật gương mới kiểm tra khả năng giữ đúng nhãn giải phẫu khi hướng quay đổi.

## Bài tập về nhà — ONNX CPU latency

| Cấu hình | preprocess (ms) | inference (ms) | postprocess (ms) | số box |
|---|---|---|---|---|
| ONNX CPU one-to-many + NMS, conf 0.25 | 7.490 | 99.110 | 1.580 | 5 |
| ONNX CPU one-to-many + NMS, conf 0.001 | 5.480 | 80.910 | 2.280 | 186 |
| ONNX CPU one-to-one NMS-free, conf 0.25 | 4.690 | 69.050 | 0.410 | 5 |
| ONNX CPU one-to-one NMS-free, conf 0.001 | 4.690 | 68.890 | 0.440 | 177 |

Kết quả đo đủ one-to-many + NMS và one-to-one NMS-free ở conf 0.25/0.001. Conf thấp giữ nhiều candidate hơn nên postprocess NMS chịu chi phí lớn hơn; head one-to-one tránh bước khử trùng lặp, phù hợp hơn với backend CPU/NPU.

Link notebook đã chạy: [< URL FILE NOTEBOOK TRÊN REPO GITHUB PUBLIC SAU KHI PUSH>](https://github.com/TrKhuyn/Track04-Day18-2D-perception-detection-segmentation-keypoints/blob/main/lab_2d_perception_student.ipynb)
