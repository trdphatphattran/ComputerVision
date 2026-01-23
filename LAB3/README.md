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
#### Toy Example  
Biểu đồ tần suất Histograms là một công cụ dùng để đếm số lần xuất hiện của các mức cường độ sáng (intensity values) trong một hình ảnh. Nó giúp chúng ta hiểu rõ hơn về phân bổ độ sáng và hỗ trợ việc xử lý, thao tác trên hình ảnh.  
Chúng ta sử dụng hàm cv2.calcHist() để tạo biểu đồ, các tham số được truyền vào như sau:  
- images: Mảng hình ảnh nguồn.
- channels: Chỉ số của kênh dùng để tính biểu đồ. Đối với ảnh xám giá trị này thường là [0].
- mask: Để xác định vùng tính toán.
- histSize: Số lượng bins để phân loại cường độ. Giá trị này là [L].
- ranges: Phạm vi của các chỉ số cường độ, thường là từ [0, L-1].
- Đối với các hình ảnh thực tế, giá trị L là 256 (0 -> 255).

Ví dụ:  
-- Vẽ biểu đồ Histograms đầu tiên  
<img width="327" height="41" alt="image" src="https://github.com/user-attachments/assets/131bc255-4dfc-4ea7-a3ec-37dd9de35206" />  

- Trục X[0, 1, 2, 3, 4, 5]: Đại diện cho các mức cường độ sáng.
- Trục Y[1, 5, 2, 0, 0, 0]: Số lượng pixel tương ứng với từng mức sáng (có 1 pixel 0, 5 pixel 1, 2 pixel 2).

<img width="539" height="416" alt="image" src="https://github.com/user-attachments/assets/10d91bff-58a1-49b0-a02c-4e6ce3657269" />  

-- Vẽ biểu đồ Histograms thứ hai  
<img width="334" height="42" alt="image" src="https://github.com/user-attachments/assets/0b55b1dc-df95-46f7-9f57-67c8febbc7eb" />  

- Giá trị 0 chuyển sang mức sáng 1 (số lượng vẫn là 1).
- Giá trị 1 chuyển sang mức sáng 3 (số lượng vẫn là 5).
- Giá trị 2 chuyển sang mức sáng 5 (số lượng vẫn là 2).

<img width="538" height="416" alt="image" src="https://github.com/user-attachments/assets/cff93811-e077-48d4-b4a5-59cef1a7b9b3" />  

#### Gray Scale Histograms  
Biểu đồ tần suất (Histogram) chủ yếu dùng cho ảnh xám, vốn rất quan trọng trong y khoa và công nghiệp. Khi xử lý ảnh màu, người ta thường tách ra thành phần độ chói (Luminance - chính là ảnh xám) để tập trung phân tích cường độ sáng.  

<img width="422" height="26" alt="image" src="https://github.com/user-attachments/assets/af46b6eb-27c8-443d-bc9e-c46391f7a6d7" />  

Đây là lệnh thực hiện việc đếm xem mỗi mức sáng xuất hiện bao nhiêu lần:  
- [goldhill]: Ảnh nguồn.
- [0]: Kênh màu.
- [256]: Số lượng bins, ở đây là 256 mức độ từ đen đến trắng.
- [0, 256]: Phạm vi cường độ sáng.

<img width="384" height="25" alt="image" src="https://github.com/user-attachments/assets/24ce96fc-53fb-4a9c-aa8a-b71106b57935" />  

Dòng này dùng để tính Probability Mass Function (PMF). Nó không chỉ đếm số lượng mà còn tính toán tỷ lệ phần trăm của mỗi mức sáng trên tổng số pixel của toàn bộ tấm ảnh.  

### 2. Intensity Transformations  
- Hình ảnh như một hàm số f(x, y), trong đó x là chỉ số hàng còn y là chỉ số cột.
- Biến đổi cường độ: Có thể tạo ra hình ảnh mới g(x, y) bằng cách áp dụng một phép biến đổi T lên ảnh cũ: g(x, y) = T(f(x, y)).
- Ánh xạ mức xám: Vì phép biến đổi này chỉ phụ thuộc vào giá trị cường độ tại một điểm duy nhất, nó còn được gọi là ánh xạ mức xám, ký hiệu là s = T(r) với r là cường độ đầu vào và s là đầu ra.
- Một phép biến đổi tuyến tính g(x, y) = 2f(x, y) + 1 sẽ nhân đôi giá trị mỗi pixel và cộng thêm 1 đơn vị.

#### Image Negatives  
- Ảnh có L mức cường độ trong khoảng [0, L-1].
- Image negative biến mỗi mức sáng thành mức tối đối nghịch của nó.
- Công thức:
Theo tọa độ ảnh:

$$  
g(x,y) = L - 1 - f(x,y)  
$$  
















