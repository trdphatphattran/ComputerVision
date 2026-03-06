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

#### Gaussian Blur  

#### Image sharpening  

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
