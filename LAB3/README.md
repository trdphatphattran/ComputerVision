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

Theo hàm biến đổi cường độ:  

$$  
s = L - 1 - r  
$$  

Với ảnh 8-bit:  

$$  
g(x, y) = 255 - f(x, y)  
$$  

và  

$$  
s = 255 - r  
$$  

--Ví dụ code chính:  
<img width="552" height="62" alt="image" src="https://github.com/user-attachments/assets/08384937-9c22-4e5b-bde8-13be36831147" />  

- -1 * img + 255 <=> 255 - img (negative).

#### Brightness and contrast adjustments  
- Ảnh gốc là f(x, y), ảnh sau biến đổi là g(x, y):

$$  
g(x,y) = \alpha f(x,y) + \beta  
$$  

- Để tăng độ sáng (brightness):  

$$  
\alpha = 1,\quad \beta = 100  
$$  

--Ví dụ code làm tăng độ sáng:  
<img width="484" height="63" alt="image" src="https://github.com/user-attachments/assets/a4c918f6-de5d-442f-9e0f-624fbaf0012f" />  

<img width="840" height="419" alt="image" src="https://github.com/user-attachments/assets/e347cbf1-c679-4192-92be-2f7ecd81f6d8" />  

--Ví dụ code là tăng độ tương phản:  
<img width="490" height="59" alt="image" src="https://github.com/user-attachments/assets/13673962-c384-4db8-b447-94dc302bb9c5" />  

<img width="839" height="419" alt="image" src="https://github.com/user-attachments/assets/2e8cf553-7ad0-4448-a4c1-318f170205fb" />  

#### Histogram Equalization  
- Giúp tăng độ tương phản của ảnh bằng cách mở rộng dải mức xám và làm phẳng histogram.
- Chỉ cần dùng hàm: cv2.equalizeHist().

--Ví dụ code sử dụng:  
<img width="385" height="37" alt="image" src="https://github.com/user-attachments/assets/5f09b374-4e89-4b7f-8ae2-18526c8a8cdf" />  

<img width="839" height="420" alt="image" src="https://github.com/user-attachments/assets/128402a7-61da-4fa6-8d5d-63a6f454939f" />  

### 3. Thresholding and Simple Segmentation  
Thresholding là kỹ thuật dùng trong image segmentation nhằm tách đối tượng ra khỏi ảnh.  
Nguyên lý:  
- Chọn 1 ngưỡng (threshold).
- Với mỗi pixel (i, j): gán 1 hoặc 255 (nếu pixel > ngưỡng), ngược lại gán 0.

--Ví dụ code chính:  
<img width="481" height="222" alt="image" src="https://github.com/user-attachments/assets/077913c1-3ada-41a2-9c86-45997868cc61" />  

- So sánh từng pixel với ngưỡng. Gán max_value và min_value.

--Ví dụ minh họa:  
<img width="687" height="83" alt="image" src="https://github.com/user-attachments/assets/cefa1c95-2f2d-4eab-bce5-a3a7abb16d8e" />  

<img width="835" height="422" alt="image" src="https://github.com/user-attachments/assets/d0b65cce-7001-4da2-85d8-44f46bcefcfb" />  

--Ngoài ra, còn một số thư viện khác như:  
- cv2.THRESH_BINARY
- cv2.THRESH_TRUNC
- cv2.THRESH_OTSU


# GIỚI THIỆU VỀ UBER DATASET  
## Phần 1: Chuẩn bị file dữ liệu  
uber-raw-data-jul14.csv  
## Phần 2: Các code chính  
### 1. Load dữ liệu với pandas  
<img width="405" height="541" alt="image" src="https://github.com/user-attachments/assets/81264c85-6de2-45eb-94e2-f9e5fe4d0f4e" />  

### 2. Xử lý dữ liệu thời gian  
- Chuyển dữ liệu sang datetime.
<img width="463" height="23" alt="image" src="https://github.com/user-attachments/assets/25ba59ec-4762-447f-97d0-4aad6e76c3cf" />

- Đếm số chuyến xe trong từng giờ.
<img width="518" height="339" alt="image" src="https://github.com/user-attachments/assets/b554c72f-6958-49d5-b247-2c1c6c2318bb" />

### 3. Theo ngày giờ trong tuần  
<img width="335" height="57" alt="image" src="https://github.com/user-attachments/assets/ca105ffe-ae6b-4301-8241-c041efba07ea" />  

- Lấy feature Hour và Week Day.

<img width="514" height="21" alt="image" src="https://github.com/user-attachments/assets/3592ef6d-927a-40ae-82dd-b7d4c20cc82f" />  

- Trung bình số chuyến cho mỗi giờ trong tuần.

<img width="559" height="596" alt="image" src="https://github.com/user-attachments/assets/d4b61474-2c10-4e06-b026-bcf81483f2a5" />  

- Chuyển sang dạng bảng để phân tích hoặc vẽ heatmap.

### 4. Tính khoảng cách địa lý  
- Ví dụ cho tọa độ Việt Nam và Trung Quốc như sau:
<img width="675" height="55" alt="image" src="https://github.com/user-attachments/assets/9ffe659b-7042-456e-9bd7-5b0957066757" />

- Tính khoảng cách Uber đi đến 2 điểm đó:
<img width="556" height="349" alt="image" src="https://github.com/user-attachments/assets/211c7bc5-627d-466a-8495-88725488c51c" />

### 5. Vẽ bản đồ Trường Đại học Văn Lang CS3  
- Sử dụng Google Maps, ta thấy VLU CS3 có tọa độ là (10.827620, 106.700011).
- Code chính để vẽ:
<img width="632" height="185" alt="image" src="https://github.com/user-attachments/assets/fcbe24e0-dde7-413c-aaa0-33a7b673549d" />

<img width="1221" height="733" alt="image" src="https://github.com/user-attachments/assets/72afd4cd-7af0-4364-a6a3-63b8f43ff48b" />  

# LAB01: LÀM QUEN VỚI ẢNH SỐ TRONG COMPUTER VISION  
## Câu 1: Cài đặt thư viện  
pip install opencv-python  
## Câu 2. Kiểm tra xem OpenCV đọc ảnh thế nào và hiển thị chiều của ảnh  
- Đọc chiều của ảnh bằng shape() và hiển thị ảnh bằng imshow().  
<img width="492" height="103" alt="image" src="https://github.com/user-attachments/assets/22a034e4-3192-40f8-af72-625cd231f7e7" />  

- Kết quả:
<img width="556" height="320" alt="image" src="https://github.com/user-attachments/assets/db039e0b-86ce-4740-9b5b-a77f10add10f" />

## Câu 3: Show hình ảnh ra cho trực quan, sử dụng plt.imshow. Có nhận xét gì về bức ảnh? Có cách nào để hiển thị đúng hay không?  
### Cách 1: Đảo chiều matrix  
<img width="312" height="84" alt="image" src="https://github.com/user-attachments/assets/f94a853d-ba23-4b0f-960a-dfa084f29100" />  

- Kết quả:
<img width="380" height="126" alt="image" src="https://github.com/user-attachments/assets/c1de4a41-af23-4812-9644-8183b232b56c" />

### Cách 2: Convert các chế độ màu  
<img width="429" height="28" alt="image" src="https://github.com/user-attachments/assets/c70a2f08-3f7b-46be-877b-1e7de10a730b" />  

- Kết quả:
<img width="558" height="166" alt="image" src="https://github.com/user-attachments/assets/8958c29d-179c-4055-911e-162daf62cd0d" />

## Câu 4: Phóng to ảnh  
- Sử dụng cv2.resize và tăng kích thước lên 1000x1000.
<img width="364" height="25" alt="image" src="https://github.com/user-attachments/assets/ddd3ba5c-b5fc-4a41-b540-abf13376f81c" />

- Kết quả:
<img width="428" height="422" alt="image" src="https://github.com/user-attachments/assets/61450d9d-e6d0-4294-8299-cd7f4a9ac5a8" />

## Câu 5: Cắt ảnh  
- Giả sử, cắt ảnh theo các thông số sau:
<img width="353" height="120" alt="image" src="https://github.com/user-attachments/assets/0ad7945a-1abe-448d-8ff2-36919194bdf8" />

- Kết quả:
<img width="503" height="421" alt="image" src="https://github.com/user-attachments/assets/7323be78-af77-47b2-bbae-a5b4041a23b6" />

## Câu 6: Ghép dọc và ghép ngang 2 ảnh  
### Ghép dọc:  
<img width="584" height="62" alt="image" src="https://github.com/user-attachments/assets/bd0f13be-a43f-4edf-8bc3-14d6dd9d976f" />  

- Kết quả:
<img width="260" height="423" alt="image" src="https://github.com/user-attachments/assets/cec2b7db-3c96-49b2-9074-a1e3382d0341" />

### Ghép ngang:  
<img width="584" height="62" alt="image" src="https://github.com/user-attachments/assets/4cf34904-564d-4025-b786-e35102780c3f" />  

- Kết quả:
<img width="555" height="281" alt="image" src="https://github.com/user-attachments/assets/ae9cd85d-2270-423d-baf0-92413eb44d50" />  

## HƯỚNG DẪN  
### 1. Cài đặt thư viện quan trọng  
pip install numpy  
pip install pandas  
pip install folium  
### 2. Chạy notebook  
- Mở Jupyter Notebook trên VSCode.
- Code từng bài và chạy để xem kết quả.
- Nếu xảy ra lỗi như code sai, không có ảnh, chưa tải thư viện -> Không hiển thị kết quả.

## TÀI LIỆU THAM KHẢO  
[1]  Images were taken from: https://homepages.cae.wisc.edu/~ece533/images/  
[2]  <a href='https://pillow.readthedocs.io/en/stable/index.html'>Pillow Docs</a>  
[3]  <a href='https://opencv.org/'>Open CV</a>  
[4] Gonzalez, Rafael C., and Richard E. Woods. "Digital image processing." (2017).  
[5 ] Jian, Wushuai, Xueyan Sun, and Shuqian Luo. "Computer-aided diagnosis of breast microcalcifications based on dual-tree complex wavelet transform." Biomedical engineering online 11.1 (2012): 1-12.  


















































