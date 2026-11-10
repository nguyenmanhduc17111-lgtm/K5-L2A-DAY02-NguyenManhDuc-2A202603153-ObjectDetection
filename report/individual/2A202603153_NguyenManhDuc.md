# Báo cáo cá nhân — Ngày 2 Object Detection



## 1. Thông tin học viên

- Họ tên:Nguyễn Mạnh Đức
- MSSV:2A202603153
- Email:26ai.ducnm13@vinuni.edu.vn
- Lớp:L2A
- Link repo bài làm:https://github.com/nguyenmanhduc17111-lgtm/K5-L2-Day02-ObjectDetection
- Link Colab đã chạy:https://colab.research.google.com/drive/1LweQs_oFdbfaBv-R_jKM4RQkbG-_eb1_#scrollTo=N52-qdiPCmJZ

## 2. Schema và mini guideline

[Mini guideline của tôi](../../GUIDELINE_MINI.md)
drive_002.jpg có nhiều xe che nhau, mỗi xe nhận diện được có một box riêng.
drive_011.jpg có xe bị cắt ở mép ảnh, box dừng ở rìa ảnh.
drive_019.jpg có hai xe che nhau, dùng hai box cho hai vật thể.
drive_017.jpg chưa chốt vì ảnh mờ, điền quyết định thực tế nếu đã xử lý.
## 3. Annotation và self-QC

- Số file nhãn train:50
- Kết quả checker và lỗi đã xử lý:đạt cấu trúc 50/50 file, chuyển ID lớp từ bản export CVAT và thống nhất ánh xạ với cấu hình cuối
- Danh sách ít nhất 10 ảnh đã rà bằng mắt:drive_001.jpg, drive_002.jpg, drive_003.jpg, drive_004.jpg, drive_005.jpg, drive_006.jpg, drive_007.jpg, drive_008.jpg, drive_009.jpg, drive_010.jpg, drive_011.jpg, drive_017.jpg, drive_019.jpg
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa:phát hiện nhiều box quá rộng, kéo lại các cạnh box cho sát phần xe. Với các xe bị che nhau, điều chỉnh box cho từng xe 
- Commit khóa nhãn ban đầu: 09dd480

## 4. Gold QC và rework

| Chỉ số | Trước sửa | Sau sửa nếu có |
|---|---:|---:|
| TP |459 |620 |
| FP |495 |151 |
| FN |194 |33 |
| Precision |0.4811 |0.8042 |
| Recall |0.7029 |0.9495 |
| F1 |0.5713 |0.8708 |
| mean_iou_of_matches |0.8323 |0.9436 |
| passed |false |true |

[Kết quả đánh giá annotation](../../outputs/annotation_evaluation.json)


## 5. Kết quả YOLO

- Môi trường: Google Colab, GPU device= T4.
- Model: YOLO26n, checkpoint khởi tạo yolo26n.pt.
- Epochs: 50.
- Kích thước ảnh: 640.
- Batch: -1.
- Seed: 20260909.
- Best checkpoint: /content/Day2-Lab/outputs/yolo26_runs/vehicle_annotation/weights/best.pt.
[10 ảnh dự đoán](assets/eval_predictions/visuals/)
[Log và biểu đồ](assets/yolo26_runs/)
| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision |0.4155 |
| Recall |0.6199 |
| mAP50 |0.5808 |
| mAP50–95 |0.4103 |



Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?
- Lớp bus recall thấp nhất, ảnh drive_052.jpg minh họa
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
- Model tìm được vật thể nhưng vị trí/kích thước box chưa đủ chính xác ở ngưỡng IoU cao.
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?
- drive_052.jpg có chiếc xe buýt lớn được dự đoán thành car; cần đối chiếu thêm phân bố lớp và nhãn train trước khi kết luận nguyên nhân.
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?
- Không dùng 10 ảnh eval để train vì model cần được đánh giá trên dữ liệu không trực tiếp dùng để cập nhật trọng số. Nếu đưa các ảnh này vào train, kết quả đánh giá có thể cao hơn thực tế do model đã học từ chúng.
- validation để theo dõi model trong quá trình huấn luyện và chọn checkpoint tốt nhất (best.pt).

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
|Thứ tự lớp CVAT khác cấu hình | |Kiểm tra tên lớp, chuyển ID |Checker đạt 50/50 |
|Colab lỗi kết nối runtime |Báo “Không gán được phần phụ trợ” và Failed to unassign endpoint |Thử đổi CPU/T4 và kết nối lại |Sau đó kết nối được và chạy notebook |
|Tải kết quả |Tải ZIP báo Failed to fetch |Dùng files.download() trong cell|Tải được ZIP về máy |

## 7. Tự đánh giá theo rubric


- Model vẫn bỏ sót hoặc nhầm lớp ở một số vật thể. Ví dụ, trong drive_052.jpg, chiếc xe buýt lớn ở giữa ảnh được dự đoán thành car, cần kiểm tra lại phân bố lpws và tính nhất quán để giải thích rõ hơn lỗi này


## 8. Công cụ AI và tài liệu tham khảo

- Codex/ChatGPT được sử dụng để hỗ trợ tạo nhãn nháp, hướng dẫn xử lỹ lôi Colab, hỗ trợ làm báo cáo.
- Google Colab và Ultralytics YOLO được sử dụng để huấn luyện, đánh giá và tạo ảnh prediction.
