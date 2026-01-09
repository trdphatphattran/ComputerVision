# LAB 1: PILLOW LIBRARY AND OPENCV LIBRARY  
## Thông tin  
Sinh viên: Trần Đại Phát  
MSSV: 2374802010379  
Môn học: Thị giác máy tính
GVHD: Đỗ Hữu Quân  
Năm học: 2025 - 2026  
## Mục tiêu bài học  
Các tác vụ chính: Xử lý và thị giác máy tính bao gồm nhiều công việc như hiển thị, cắt, lật, xoay, phân đoạn, phân loại, phục hồi, nhận dạng và tạo ảnh. Ngoài ra, việc làm việc trên đám mây đòi hỏi các kỹ năng lưu trữ, truyền tải và thu thập hình ảnh qua internet.

Lý do chọn Python: Python là công cụ tuyệt vời nhờ sở hữu hệ thống thư viện phong phú về xử lý ảnh, thị giác máy tính, trí tuệ nhân tạo, cũng như các thư viện hỗ trợ làm việc với dữ liệu trên internet và đám mây.

Mục tiêu bài học: Hình ảnh kỹ thuật số thực chất là các tệp tin trên máy tính. Trong bài thực hành này, bạn sẽ tìm hiểu bản chất của các tệp tin đó và học cách thao tác với chúng thông qua thư viện Pillow (PIL) và OpenCV của Python.  
# PILLOW LIBRARY  
## Phần 1: Cài đặt thư viện  
pip install Pillow  
## Phần 2: Các đoạn mã chính  
### Import và load thư viện  
from PIL import Image   
import numpy as np  
import matplotlib.pyplot as plt  
### Lấy thông tin ảnh  
print(image.size) (width, height)  
<img width="128" height="19" alt="image" src="https://github.com/user-attachments/assets/c8a7de26-0d94-4579-8a70-bbb9f5b5f608" />  
print(image.mode) (RGB)  
<img width="130" height="23" alt="image" src="https://github.com/user-attachments/assets/05e0633c-3148-4323-a167-b4987029f19b" />  
--> Hiểu cấu trúc dữ liệu ảnh.  
### Chuyển sang Grayscale  
from PIL import ImageOps  
image_gray = ImageOps.grayscale(image)  
### Lượng tử hóa  
image_gray.quantize(256 // 2**n)  
--> Hiểu cách giảm độ phân giải ảnh  
### Tách kênh màu  
red, green, blue = baboon.split()  
--> Làm việc với các kênh RGB.  
### Chuyển PIL --> NumPy Array  
array = np.asarray(image)  
array = np.array(image)  
### Lấy thông tin NumPy Array  
array.shape, array.min(), array.max()  
--> Hiểu cấu trúc mảng.  
### Slicing ảnh  
array[0:rows, :, :] (cắt ngang)  
array[:, 0:columns, :] (cắt dọc)  
### Làm việc với kênh màu  
baboon_red = baboon_array.copy()  
baboon_red[:, :, 1] = 0 (xóa G)  
baboon_red[:, :, 2] = 0  (xóa B)  


