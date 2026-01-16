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
#### Giả sử gán vào ảnh baboon.  
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
#### Giả sử gán vào ảnh cat.png.  
<img width="833" height="521" alt="image" src="https://github.com/user-attachments/assets/6b9bff49-c391-4089-9146-9879cfe8b606" />  

- Sử dụng "flip" để đảo hình ảnh từ trên xuống.
<img width="226" height="23" alt="image" src="https://github.com/user-attachments/assets/5e1478ac-9e0b-4d77-a0a9-b32903ab3983" />

--> Kết quả:  
<img width="448" height="289" alt="image" src="https://github.com/user-attachments/assets/ecc2377d-b436-44b2-b78b-b655c23cf212" />  

- Sử dụng "mirror" để lật ảnh sang ngang (trái qua phải).
<img width="255" height="22" alt="image" src="https://github.com/user-attachments/assets/ddd82a2a-ca92-4317-bd3c-c86ae591ba3f" />

--> Kết quả:  
<img width="445" height="286" alt="image" src="https://github.com/user-attachments/assets/c37b8efd-19f4-4951-b0b2-705b1fec8f1f" />  

- Sử dụng "transpose" để lật ảnh theo chiều dọc.
<img width="208" height="20" alt="image" src="https://github.com/user-attachments/assets/2fc6d159-9034-4435-9f83-ce924bf3995c" />

--> Kết quả:  
<img width="555" height="352" alt="image" src="https://github.com/user-attachments/assets/5fba393f-ed0c-48f9-a43e-3fe6d3467541" />  

- Một số cách khác:  
<img width="363" height="130" alt="image" src="https://github.com/user-attachments/assets/08d03692-79a8-422a-bd87-e000cc10fd36" />

--> Kết quả:  
<img width="827" height="579" alt="image" src="https://github.com/user-attachments/assets/70d724e9-b432-4a94-9e97-28cff70ac995" />  

<img width="825" height="644" alt="image" src="https://github.com/user-attachments/assets/ae5cb083-26b8-411a-b536-bb51dea85013" />  

<img width="825" height="281" alt="image" src="https://github.com/user-attachments/assets/3c883898-9a87-43ee-b77f-1223844f63b1" />  

<img width="826" height="643" alt="image" src="https://github.com/user-attachments/assets/2fa75014-916d-4fa8-a6f4-baaeedd0689f" />  

<img width="826" height="642" alt="image" src="https://github.com/user-attachments/assets/e5ea395b-75f2-4585-a713-cf6fd328b331" />  

<img width="825" height="643" alt="image" src="https://github.com/user-attachments/assets/372ff6aa-dd8e-437c-8095-a04a51c28974" />  

### Cropping an image  
#### Giả sử vẫn truyền vào cat.png  
- Cắt ảnh theo hàng dọc từ 150 đến 400, minh họa crop được bằng slicing trên numpy array.  
<img width="255" height="57" alt="image" src="https://github.com/user-attachments/assets/d8c86cc5-3c2e-4415-bc89-5749d444ad9c" />

--> Kết quả:  
<img width="440" height="93" alt="image" src="https://github.com/user-attachments/assets/dada685e-506a-4c5a-9d7e-58995fe60a62" />  

- Cắt ảnh theo cột từ 150 đến 400, minh họa crop ngang để thu hẹp vùng.  
<img width="318" height="59" alt="image" src="https://github.com/user-attachments/assets/e3def3a8-07f6-4b59-9d60-8622d546b3a0" />  

--> Kết quả:  
<img width="440" height="125" alt="image" src="https://github.com/user-attachments/assets/61756bdf-80d1-437d-9fb3-54f0c8fde582" />  

- Cắt ảnh với các tọa độ left, upper, right, lower.
<img width="380" height="39" alt="image" src="https://github.com/user-attachments/assets/92d7c39f-831c-4e58-bb2c-1f4985fff644" />

--> Kết quả:  
<img width="444" height="435" alt="image" src="https://github.com/user-attachments/assets/78815757-1679-40b2-a1e5-93e61d084996" />  

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






