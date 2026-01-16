# LAB 2: MANIPULATING IMAGES  
## Thông tin  
Sinh viên: Trần Đại Phát  
MSSV: 2374802010379  
Môn học: Thị giác máy tính  
GVHD: Đỗ Hữu Quân  
Năm học: 2025 - 2026  
## Mục tiêu bài học  
- Hiểu cách xử lý ảnh dưới dạng mảng Numpy và đối tượng PIL.
- Biết sao chép ảnh để tránh hiện tượng aliasing.
- Thực hành lật ảnh (flip) và cắt ảnh (crop).
- Biết cách thay đổi giá trị pixel để vẽ hình, chèn chữ và chồng ảnh.

# PILLOW LIBRARY  
## Phần 1: Cài đặt thư viện  
pip install Pillow  
## Phần 2: Các đoạn mã chính  
### Import và load thư viện  
from PIL import Image   
import numpy as np  
import matplotlib.pyplot as plt  

### Copying images  
Giả sử gán vào ảnh baboon.  
- Gán biến A bằng baboon.
<img width="81" height="20" alt="image" src="https://github.com/user-attachments/assets/89b739c7-9dd7-41ca-8fc4-8a8bdb90dad5" />

--> Minh họa aliasing, nếu thay đổi baboon thì A cũng thay đổi.  
- Kiểm tra id của A và baboon.
<img width="147" height="24" alt="image" src="https://github.com/user-attachments/assets/c1bb1d63-bcae-49a5-a7b1-7e926259c26f" />

--> Xác nhận chúng chỉ đến cùng một vị trí.  
- Sao chép baboon thành B và kiểm tra id.
<img width="129" height="40" alt="image" src="https://github.com/user-attachments/assets/e9ed90f2-a91d-48d4-8934-36a1c7fc0272" />

--> Tránh aliasing, B không bị ảnh hưởng khi thay đổi baboon.  
- Đặt tất cả pixel của mảng baboon thành 0.
<img width="128" height="21" alt="image" src="https://github.com/user-attachments/assets/bd0a1855-7e05-490c-a2fa-fe0265802058" />
--> Kiểm tra aliasing, A sẽ đen như baboon, còn B thì không.

- Hiển thị baboon đen và A cũng đen, aliasing cả 2 giống nhau.
<img width="838" height="420" alt="image" src="https://github.com/user-attachments/assets/01596565-e876-40b1-96f4-9c9e8c1501e8" />

- Hiển thị baboon đen và B ảnh gốc, copy đúng và B không thay đổi.
<img width="839" height="419" alt="image" src="https://github.com/user-attachments/assets/ad9bff20-4ec9-4f80-b51f-46666830cbe9" />  

### Flipping images  

### Cropping an image  

### Changing Specific Image Pixels  

# OPENCV LIBRARY  
## Phần 1: Cài đặt thư viện  
pip install opencv-python  
## Phần 2: Các đoạn mã chính  
### Import thư viện  
import cv2  
import numpy as np  
import matplotlib.pyplot as plt  

### Copying images  

### Flipping images  

### Cropping an image  

### Changing Specific Image Pixels  

## Hướng dẫn  
### 1. Cài đặt môi trường  
Cài python, sau đó cài các thư viện:  
Dùng tổ hợp phím: Windows + R + cmd.  
- pip install matplotlib.
- pip install opencv-python.
- pip install Pillow.  
### 2. Chạy notebook  
- Mở Jupyter Notebook trên VSCode.
- Code từng bài và chạy để xem kết quả.
- Nếu xảy ra lỗi như code sai, không có ảnh, chưa tải thư viện -> Không hiển thị kết quả.  

## Tài liệu tham khảo  
[1]  Images were taken from: https://homepages.cae.wisc.edu/~ece533/images/  
    
[2]  <a href='https://pillow.readthedocs.io/en/stable/index.html'>Pillow Docs</a>  

[3]  <a href='https://opencv.org/'>Open CV</a>  

[4] Gonzalez, Rafael C., and Richard E. Woods. "Digital image processing." (2017).  






