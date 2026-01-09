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
<img width="279" height="39" alt="image" src="https://github.com/user-attachments/assets/46e5f68c-92aa-4f0d-a6f5-49543d5ebbb9" />  
### Lượng tử hóa  
image_gray.quantize(256 // 2**n)  
<img width="226" height="39" alt="image" src="https://github.com/user-attachments/assets/2ab69e1f-51ed-43bd-8520-7f05f8970ebb" />  
--> Hiểu cách giảm độ phân giải ảnh  
### Tách kênh màu  
red, green, blue = baboon.split()  
<img width="247" height="21" alt="image" src="https://github.com/user-attachments/assets/8c6d9f68-99c5-4957-9e99-7233912bc40f" />  
--> Làm việc với các kênh RGB.  
### Chuyển PIL --> NumPy Array  
array = np.asarray(image)  
<img width="186" height="37" alt="image" src="https://github.com/user-attachments/assets/743df8a6-1f2f-4f4e-8333-72efcc2c148f" />  
array = np.array(image)  
<img width="172" height="22" alt="image" src="https://github.com/user-attachments/assets/4e95b728-eda9-42c4-b25d-ebcf2f801f6e" />  
### Lấy thông tin NumPy Array  
array.shape, array.min(), array.max()  
--> Hiểu cấu trúc mảng.  
### Slicing ảnh  
array[0:rows, :, :] (cắt ngang)  
<img width="215" height="58" alt="image" src="https://github.com/user-attachments/assets/41d26bb6-b2b3-4055-ac62-721bc8399464" />  
array[:, 0:columns, :] (cắt dọc)  
<img width="243" height="55" alt="image" src="https://github.com/user-attachments/assets/fd536f81-07a6-41bb-b476-48d623e81658" />  
### Làm việc với kênh màu  
baboon_red = baboon_array.copy()  
baboon_red[:, :, 1] = 0 (xóa G)  
baboon_red[:, :, 2] = 0  (xóa B)  


# OPENCV LIBRARY  
## Phần 1: Cài đặt thư viện  
pip install opencv-python  
## Phần 2: Các đoạn mã chính  
### Import thư viện  
import cv2  
import numpy as np  
import matplotlib.pyplot as plt  
### Kiểm tra kiểu dữ liệu  
type(image)  
image.shape  
<img width="87" height="20" alt="image" src="https://github.com/user-attachments/assets/b177d7a2-373d-42e0-ab12-262480cea585" />  
image.max()  
<img width="83" height="22" alt="image" src="https://github.com/user-attachments/assets/b29b4a3e-b88b-48fa-8457-7e098270481d" />  
image.min()  
<img width="84" height="22" alt="image" src="https://github.com/user-attachments/assets/cc1429ba-20be-422f-bac2-123bf4ad3557" />  
--> Hiểu cấu trúc dữ liệu NumPy Array.  
### Chuyển đổi định dạng màu  
new_image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)  
<img width="357" height="20" alt="image" src="https://github.com/user-attachments/assets/0fe75c5d-801e-4696-85ba-255db4493fdd" />  
--> OpenCV dùng BGR, phải chuyển sang RGB để hiển thị đúng màu.  
### Chuyển sang Grayscale  
image_gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)  
<img width="380" height="22" alt="image" src="https://github.com/user-attachments/assets/18ddb9dc-18be-4db8-bfaf-eb64f68886d7" />  
### Tách các kênh màu  
blue, green, red = baboon[:, :, 0], baboon[:, :, 1], baboon[:, :, 2]  
<img width="499" height="24" alt="image" src="https://github.com/user-attachments/assets/373d27ed-be04-4992-8eca-9245598f6220" />  
--> Làm việc trực tiếp với NumPy Slicing.  
### Slicing ảnh  
new_image[0:rows, :, :] (cắt ngang)  
<img width="248" height="57" alt="image" src="https://github.com/user-attachments/assets/bc728e8e-dc09-4a10-b740-a5ec197bded8" />  
new_image[:, 0:columns, :] (cắt dọc)  
<img width="268" height="56" alt="image" src="https://github.com/user-attachments/assets/1a798d9f-8708-4ef1-8590-014e5fa217b6" />  
--> Trích xuất phần ảnh  
### Làm việc với kênh màu  
baboon_red = baboon.copy()  
baboon_red[:, :, 0] = 0 (xóa B)  
baboon_red[:, :, 1] = 0 (xóa G)  



