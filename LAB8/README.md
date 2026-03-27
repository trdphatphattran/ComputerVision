# LAB 8: NHẬN DIỆN ĐỐI TƯỢNG TRONG VIDEO (VIDEO DETECTION)  
## Thông tin  
Sinh viên: Trần Đại Phát  
MSSV: 2374802010379  
Môn học: Thị giác máy tính  
GVHD: Đỗ Hữu Quân  
Năm học: 2025 - 2026  

## Phần 1: Lý thuyết  
Nhận diện đối tượng trong video (Video Detection) là quá trình giúp máy tính hiểu và xác định nội dung trong video, ví dụ như:  
- Video có người, chó, xe, ...
- Nhận ra khuôn mặt, vật thể, hoặc chữ viết, ...

## Phần 2: Bài tập  

### Sử dụng đường dẫn sau đây để lưu về video dài khoảng 12 đến 20 giây:
https://pixabay.com/vi/videos/search/l%e1%bb%85%20h%e1%bb%99i/  

### Sau đó, theo link github này và tải về thư mục retinanet_resnet50_fpn_coco-eeacb38b.pth:  
https://github.com/OlafenwaMoses/ImageAI/releases  

### Code chính:  
```python
detector = VideoObjectDetection()
detector.setModelTypeAsRetinaNet()
detector.setModelPath(os.path.join(execution_path, "retinanet_resnet50_fpn_coco-eeacb38b.pth"))
detector.loadModel()
```
- Chọn loại máy quét: Dùng thuật toán RetinaNet.  
- Nạp dữ liệu: Chỉ đường dẫn đến file chứa những gì đã học.  
- Kích hoạt: Nạp toàn bộ cấu hình đó vào hệ thống để sẵn sàng bắt đầu quét video.

```python
video_path = detector.detectObjectsFromVideo(input_file_path=os.path.join(execution_path, "video_predicted.mp4"), 
                                             output_file_path=os.path.join(execution_path, "video_predicted"), 
                                             frames_per_second=5, log_progress=True)
print(video_path)
```
- Đọc video gốc: Lấy file video_predicted.mp4 để phân tích.  
- Quét vật thể: Tìm người, xe, đồ vật... trong video với tốc độ 5 khung hình/giây.  
- Xuất video mới: Tạo ra một video kết quả (có vẽ sẵn các ô vuông bao quanh vật thể) và in ra đường dẫn file đó sau khi xong.

--> Kết quả:  

<img width="1512" height="982" alt="image" src="https://github.com/user-attachments/assets/f54abb7d-aa62-40e3-859c-44521bf0cdca" />  

## HƯỚNG DẪN  
### 1. Cài đặt thư viện quan trọng  
!pip install imageai  
### 2. Chạy notebook  
- Mở Jupyter Notebook trên VSCode hoặc dùng Colab.  
- Code từng bài và chạy để xem kết quả.
- Nếu xảy ra lỗi như code sai, không có ảnh, chưa tải thư viện -> Không hiển thị kết quả.

## Tài liệu tham khảo  
[1] https://imageai.readthedocs.io/en/latest/video/index.html  
[2] https://github.com/OlafenwaMoses/ImageAI  


