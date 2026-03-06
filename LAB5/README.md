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

### 3. Median  

## Phần 2: Với OpenCV  
### 1. Linear Filtering  
#### Filtering noise  

#### Gaussian Blur  

#### Image sharpening  

### 2. Edges  

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
