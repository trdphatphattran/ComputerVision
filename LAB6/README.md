# LAB 6: Keypoint Detection  
## Thông tin  
Sinh viên: Trần Đại Phát  
MSSV: 2374802010379  
Môn học: Thị giác máy tính  
GVHD: Đỗ Hữu Quân  
Năm học: 2025 - 2026  

## Phần 1: Lý thuyết  


## Phần 2: Bài tập  
### Bài 1: Khai báo thư viện và ảnh đầu vào  
```python
import numpy as np
import cv2
import matplotlib.pyplot as Phat

img = cv2.imread('image.png')
Phat.imshow(img[:,:,::-1])
```
--> Kết quả:  


### Bài 2: Sử dụng Harris Corner Detection tìm các keypoint trong ảnh  

### Bài 3: Sử dụng Band-pass filtering by Difference of Gaussians  

### Bài 4: Kiểm tra ảnh qua Automatic Scale Selection  

### Bài 5: Kiểm tra ảnh qua Scale Invariant Detection  

### Bài 6: Kiểm tra ảnh qua Scale-space blob detector  

### Bài 7: Thực hành với Bag-of-words detection  

### Bài 8: Ghép ảnh Image Panoramas  

### Bài 9: Ghép ảnh Automatic mosaicing  

### Bài 10: Sử dụng Wide base-line stereo  

### Bài 11: CBIR (content-based image retrieval)  

### Bài 12: Bag-of-word with SIFT + Histogram  

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
[5] Jian, Wushuai, Xueyan Sun, and Shuqian Luo. "Computer-aided diagnosis of breast microcalcifications based on dual-tree complex wavelet transform." Biomedical engineering online 11.1 (2012): 1-12.  
[6] https://docs.opencv.org/3.4/dc/d0d/tutorial_py_features_harris.html

