# LAB 5: Spatial Operations in Image Processing  
## Thông tin  
Sinh viên: Trần Đại Phát  
MSSV: 2374802010379  
Môn học: Thị giác máy tính  
GVHD: Đỗ Hữu Quân  
Năm học: 2025 - 2026  
## Mục tiêu bài học  
Mục tiêu của bài này là tìm hiểu các phép toán không gian (spatial operations) trong xử lý ảnh, sử dụng các pixel lân cận để xác định giá trị của pixel hiện tại. Các kỹ thuật như lọc nhiễu, làm mờ Gaussian, làm sắc nét, phát hiện cạnh và lọc trung vị được áp dụng để cải thiện chất lượng ảnh và hỗ trợ các bước quan trọng trong thị giác máy tính và trí tuệ nhân tạo.  

## Phần 1: Với Pillow  
### 1. Linear Filtering  
Filtering là kỹ thuật cải thiện chất lượng ảnh, ví dụ như loại bỏ nhiễu hoặc làm sắc nét ảnh bị mờ. Phương pháp phổ biến để thực hiện filtering là convolution, sử dụng một kernel để nhân với vùng ảnh tương ứng rồi dịch chuyển trên toàn bộ ảnh. Các kernel khác nhau sẽ thực hiện những nhiệm vụ khác nhau và phương pháp này cũng được sử dụng rộng rãi trong các thuật toán AI.  
#### Filtering noise  
Import ImageFilter từ thư viện PIL.  
- Tạo kernel để làm mượt ảnh
<img width="198" height="20" alt="image" src="https://github.com/user-attachments/assets/13a41ee7-ad76-43b4-9173-9bf777833d24" />

- Tạo bộ lọc kernel
<img width="433" height="23" alt="image" src="https://github.com/user-attachments/assets/b88ad5c1-8a28-4f66-99bb-d520e19c0895" />

- Áp dụng bộ lọc lên ảnh nhiễu để giảm noise
<img width="367" height="25" alt="image" src="https://github.com/user-attachments/assets/22fb35b8-7caa-4bd8-8c0a-30b8cc9068b3" />

--> Kết quả:  
<img width="835" height="416" alt="image" src="https://github.com/user-attachments/assets/a3e6dbd6-0299-4fa9-8829-802a9e5fbd53" />  

#### Gaussian Blur  
Gaussian Blur được thực hiện bằng cách sử dụng hàm filter() trên ảnh cùng với bộ lọc có sẵn ImageFilter.GaussianBlur. Bộ lọc này làm mờ ảnh bằng cách làm mượt các pixel lân cận để giảm nhiễu và chi tiết nhỏ.  

```python
image_filtered = noisy_image.filter(ImageFilter.GaussianBlur)  
```
--> Kết quả  
<img width="831" height="410" alt="image" src="https://github.com/user-attachments/assets/1c7f0443-888c-403d-8251-56e59bb21d99" />  

#### Image sharpening  
Image Sharpening là kỹ thuật làm sắc nét ảnh bằng cách làm mượt ảnh và tính toán sự thay đổi giữa các pixel (đạo hàm). Quá trình này thường được thực hiện bằng cách áp dụng một kernel để làm nổi bật các chi tiết và cạnh trong ảnh.  
```python
kernel = np.array([[-1,-1,-1], 
                   [-1, 9,-1],
                   [-1,-1,-1]])
kernel = ImageFilter.Kernel((3,3), kernel.flatten())
```
- Tạo sharpening kernel để làm nổi bật chi tiết và tạo bộ lọc từ kernel.

- Áp dụng bộ lọc sharpening lên ảnh
<img width="237" height="20" alt="image" src="https://github.com/user-attachments/assets/b2ff918a-0c75-49cd-a67f-a2172ca5479a" />

--> Kết quả  
<img width="831" height="413" alt="image" src="https://github.com/user-attachments/assets/0b333ef3-10b4-4aea-bf60-312a0ab7f559" />  

Hoặc ta có thể sử dụng ImageFilter.SHARPEN  
<img width="334" height="20" alt="image" src="https://github.com/user-attachments/assets/36f19fb5-c505-4589-9184-ba692bf5d0da" />  

### 2. Edges  
Edges là những vị trí trong ảnh nơi cường độ pixel thay đổi mạnh. Gradient được dùng để đo tốc độ thay đổi này và có thể được xấp xỉ bằng phép convolution trên ảnh xám để phát hiện các cạnh trong ảnh.  
- Sử dụng ImageFilter.EDGE_ENHANCE để làm nổi bật các cạnh trong ảnh xám.
<img width="381" height="19" alt="image" src="https://github.com/user-attachments/assets/ad373fd1-229b-4975-b851-7ef2c28da505" />

--> Kết quả  
<img width="431" height="416" alt="image" src="https://github.com/user-attachments/assets/6e972c0f-5610-46d8-bb9c-ef9ed6cc675b" />  

- Sử dụng ImageFilter.FIND_EDGES để phát hiện các cạnh trong ảnh.  
<img width="368" height="21" alt="image" src="https://github.com/user-attachments/assets/f9a6bca5-7f8e-4240-8813-cf0a10e94591" />  

--> Kết quả  
<img width="817" height="806" alt="image" src="https://github.com/user-attachments/assets/547596d4-8938-46c1-a2f8-bb4d097dfabe" />  


### 3. Median  
Median filter là phương pháp lọc ảnh bằng cách lấy giá trị trung vị (median) của các pixel trong vùng kernel, sau đó thay thế giá trị pixel trung tâm bằng giá trị này. Phương pháp này thường được dùng để giảm nhiễu trong ảnh.  
- Sử dụng thư viện ImageFilter.MedianFilter để giảm nhiễu trong ảnh.
<img width="342" height="21" alt="image" src="https://github.com/user-attachments/assets/33e46720-ce30-4cbe-9ee8-75057d428e51" />

--> Kết quả
<img width="814" height="807" alt="image" src="https://github.com/user-attachments/assets/e47878f1-89d3-43ec-8df3-2475fce666b1" />  

## Phần 2: Với OpenCV  
### 1. Linear Filtering  
#### Filtering noise  
- Dùng hàm filter2D để lọc nhiễu
<img width="499" height="22" alt="image" src="https://github.com/user-attachments/assets/9c5270ee-2905-4458-9bad-aea5e53c6cc3" />

--> Kết quả  
<img width="829" height="410" alt="image" src="https://github.com/user-attachments/assets/a963a080-88c2-46be-8f70-73335ee2de9d" />  

#### Gaussian Blur  
- Dùng hàm GaussianBlur để tiến hành lọc nhiễu với 2 độ lệch chuẩn là sigmaX và sigmaY  
<img width="514" height="21" alt="image" src="https://github.com/user-attachments/assets/b15ee84b-0497-4658-ac00-eba1615a8031" />

--> Kết quả  
<img width="827" height="408" alt="image" src="https://github.com/user-attachments/assets/7e9a3cb8-83ca-4a05-b81a-f30d3b355e7e" />  

#### Image sharpening  
- Dùng hàm filter2D để làm sắc nét ảnh.
<img width="321" height="19" alt="image" src="https://github.com/user-attachments/assets/2a18ea35-5ceb-4dd5-ba78-d5464b4a3c4a" />

--> Kết quả  
<img width="826" height="413" alt="image" src="https://github.com/user-attachments/assets/043101a5-2cb7-4153-aae8-be181af10868" />

### 2. Edges  
- Dùng Sobel filter để phát hiện cạnh theo chiều ngang theo hướng X.
<img width="501" height="19" alt="image" src="https://github.com/user-attachments/assets/bc24eb20-7474-45bb-ae34-9b53492b729d" />

--> Kết quả  
<img width="424" height="409" alt="image" src="https://github.com/user-attachments/assets/19b2500c-3e4e-43a7-92cd-7e68383b0647" />  

- Dùng Sobel filter để phát hiện cạnh theo chiều dọc theo hướng Y.
<img width="503" height="21" alt="image" src="https://github.com/user-attachments/assets/623b8647-ee27-4ce7-94e8-acfafb19e12c" />

--> Kết quả  
<img width="423" height="408" alt="image" src="https://github.com/user-attachments/assets/86788bd8-764f-4fba-b6bb-326e9f41d2bd" />  

### 3. Median  

### 4. Threshold  

## HƯỚNG DẪN  
### 1. Cài đặt thư viện quan trọng  
pip install numpy  
pip install pandas  
pip install folium  
pip install opencv-python.  
pip install Pillow.  
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
