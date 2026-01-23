# LAB 3: Histogram and Intensity Transformations  
## Thông tin  
Sinh viên: Trần Đại Phát  
MSSV: 2374802010379  
Môn học: Thị giác máy tính  
GVHD: Đỗ Hữu Quân  
Năm học: 2025 - 2026  
## Mục tiêu bài học  
Bài này tập trung vào các phép biến đổi ảnh (Pixel Transforms) - là những thao tác được thực hiện trên từng pixel một. Các nội dung cụ thể bao gồm:  
- Histograms: Áp dụng để hiển thị cường độ sáng của hình ảnh, từ đó giúp tối ưu hóa các đặc tính của ảnh.
- Intensity Transformations: Áp dụng để cải thiện độ tương phản và độ sáng, giúp các đối tượng trong ảnh trở nên dễ quan sát hơn.
- Thresholding: Sử dụng ở phần cuối của bài lab để phân tách các đối tượng trong ảnh ra khỏi nền ảnh.

## Phần 1: Cài đặt thư viện  
%pip install matplotlib opencv-contrib-python (cài opencv và matplotlib).  

## Phần 2: Lý thuyết và ví dụ  
### 1. Histograms  
Biểu đồ tần suất Histograms là một công cụ dùng để đếm số lần xuất hiện của các mức cường độ sáng (intensity values) trong một hình ảnh. Nó giúp chúng ta hiểu rõ hơn về phân bổ độ sáng và hỗ trợ việc xử lý, thao tác trên hình ảnh.  
Chúng ta sử dụng hàm cv2.calcHist() để tạo biểu đồ, các tham số được truyền vào như sau:  
- images: Mảng hình ảnh nguồn.
- channels: Chỉ số của kênh dùng để tính biểu đồ. Đối với ảnh xám giá trị này thường là [0].
- mask: Để xác định vùng tính toán.
- histSize: Số lượng bins để phân loại cường độ. Giá trị này là [L].
- ranges: Phạm vi của các chỉ số cường độ, thường là từ [0, L-1].
- Đối với các hình ảnh thực tế, giá trị L là 256 (0 -> 255).

