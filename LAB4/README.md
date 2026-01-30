# LAB 4: Geometric Operations and Other Mathematical Tools  
## Thông tin  
Sinh viên: Trần Đại Phát  
MSSV: 2374802010379  
Môn học: Thị giác máy tính  
GVHD: Đỗ Hữu Quân  
Năm học: 2025 - 2026  
## Mục tiêu bài học  
Bài lab này giúp chúng ta tìm hiểu về 2 kiến thức chính:  
1. Geometric Operations:
- Scaling: Phóng to hoặc thu nhỏ ảnh.
- Translation: Dịch chuyển ảnh.
- Rotation: Xoay ảnh.
2. Mathematical Operations:
- Array Operations: Xử lý trên mảng.
- Matrix Operations: Xử lý trên ma trận.

## Phần 1: Với Pillow  
### 1. Geometric Operations:  
Cho vào ảnh gốc có kích thước cụ thể như ví dụ sau:  
<img width="432" height="419" alt="image" src="https://github.com/user-attachments/assets/b8dbd764-1b50-4c3d-9e75-ac59231535ac" />  

#### Phóng to hoặc thu nhỏ ảnh  

- Giả sử tăng chiều rộng của ảnh lên 2 lần:  
<img width="162" height="21" alt="image" src="https://github.com/user-attachments/assets/f41c95dd-a73f-4cbf-8b97-64c395d2b6f1" />

--> Kết quả:  
<img width="559" height="298" alt="image" src="https://github.com/user-attachments/assets/1f2cbf4a-4422-43cf-a35c-821ed3512a98" />  

- Giả sử tăng chiều cao lên 2 lần:
<img width="165" height="19" alt="image" src="https://github.com/user-attachments/assets/8bb025c3-8ab3-4498-aede-235fa64e96b7" />

--> Kết quả:  
<img width="250" height="419" alt="image" src="https://github.com/user-attachments/assets/e8ad22df-415f-4ae7-ac94-77582c960e39" />  

- Giả sử tăng chiều dài và chiều rộng lên 2 lần:
<img width="168" height="38" alt="image" src="https://github.com/user-attachments/assets/b73bc3cb-ef4a-4b9b-878f-d836b71c1009" />

--> Kết quả:  
<img width="445" height="421" alt="image" src="https://github.com/user-attachments/assets/4ce8bc34-b52a-4dd8-9a9b-4ad09eea96f3" />  

- Giả sử giảm chiều dài và chiều rộng xuống 2 lần:  
<img width="177" height="42" alt="image" src="https://github.com/user-attachments/assets/a328c454-6d94-4cb1-99a3-1008a1069a47" />  

--> Kết quả:  
<img width="431" height="418" alt="image" src="https://github.com/user-attachments/assets/b78c0277-d390-43c1-8cf5-1cf27ee6f222" />  

- Giả sử xoay ảnh sang 45 độ:
<img width="82" height="21" alt="image" src="https://github.com/user-attachments/assets/48f46a2e-6a20-4516-a543-ccb19328c2b5" />

--> <img width="433" height="419" alt="image" src="https://github.com/user-attachments/assets/d8af4af1-c9e8-4e4a-888e-f22a194bfc29" />  

### 2. Mathematical Operations  
#### Array Operations  
- Giả sử phép cộng vô hướng vào một ma trận, mỗi ma trận trong ảnh sẽ được cộng thêm 20 đơn vị:
<img width="169" height="21" alt="image" src="https://github.com/user-attachments/assets/57a2d44b-6010-42c8-925c-f0e3ab26be60" />

--> Kết quả:  
<img width="432" height="421" alt="image" src="https://github.com/user-attachments/assets/6cb27daa-358e-4808-ade8-6033cc245985" />  

- Giả sử nhân mỗi ma trận trong ảnh thêm 10 đơn vị:
<img width="168" height="19" alt="image" src="https://github.com/user-attachments/assets/3c3ff409-4ea0-496b-9f55-855f09e6c73e" />

--> Kết quả:  
<img width="431" height="420" alt="image" src="https://github.com/user-attachments/assets/a901f6f8-e499-41c2-914f-3b3e7687264d" />  

- Giả sử chúng ta có thêm độ nhiễu vào ảnh:  
``` python
Noise = np.random.normal(0, 20, (height, width, 3)).astype(np.uint8)  
```
<img width="194" height="20" alt="image" src="https://github.com/user-attachments/assets/49413c38-86c0-4731-89ac-bc3278d235dd" />  

--> Kết quả:  
<img width="433" height="420" alt="image" src="https://github.com/user-attachments/assets/2a51490e-9867-4a92-992e-b57d2719f6dc" />  

#### Matrix Operations  
<img width="391" height="22" alt="image" src="https://github.com/user-attachments/assets/56bc5df1-096c-4724-989e-81b4acda0ead" />  

Đây là lệnh thực hiện phép Phân tách giá trị đơn lẻ (Singular Value Decomposition - SVD):  
- U: Ma trận trực giao (cột là các vector suy biến trái).  
- s: Một vector chứa các giá trị đơn lẻ (singular values) sắp xếp giảm dần. Chúng đại diện cho "tầm quan trọng" của các thành phần trong ảnh.  
- V: Ma trận trực giao (hàng là các vector suy biến phải).

<img width="839" height="421" alt="image" src="https://github.com/user-attachments/assets/05d21f55-6a26-4de3-aeee-36bfc8151f93" />  

--  

<img width="97" height="19" alt="image" src="https://github.com/user-attachments/assets/ba480d50-434c-42c1-ade9-7b5faa40edda" />  

Đây là dòng thực hiện phép nhân ma trận giữa ma trận đường chéo S và ma trận V.  Kết quả B là một ma trận trung gian đã đưa vào các trọng số từ S vào V.  

## Phần 2: Với OpenCV  
### 1. Geometric Operations:  
#### Scaling  
Có 2 kỹ thuật thường dùng là:  
- INTER_NEAREST (Nội suy lân cận gần):
  - Máy sẽ lấy đúng giá trị pixel nằm gần với vị trí mới nhất.
<img width="606" height="19" alt="image" src="https://github.com/user-attachments/assets/3a4ba7b1-b22c-4f47-b0b2-57420ceb52e7" />

--> Kết quả:  
<img width="535" height="292" alt="image" src="https://github.com/user-attachments/assets/18d75562-7b47-418a-afea-4228ba1f7891" />  

- INTER_CUBIC (Nội suy khối):
  - Máy tính sử dụng giá trị của nhiều pixel xung quanh (thường là một lưới 4x4 gồm 16 pixel để tính toán).
<img width="568" height="17" alt="image" src="https://github.com/user-attachments/assets/c91d9ab8-1586-4213-8aea-6a7131e156c9" />

--> Kết quả:  
<img width="584" height="343" alt="image" src="https://github.com/user-attachments/assets/30decc04-616e-4de5-8874-45993c9424bb" />  

#### Translation  
<img width="375" height="24" alt="image" src="https://github.com/user-attachments/assets/e3238a25-ba86-420a-a8c8-d8a642b28f00" />  

Đây là hàm được dùng để thực hiện phép biến đổi Afin cho phép dịch chuyển, xoay, ... ảnh.  

Giả sử cho đầu vào tx = 100, ty = 0, ta có ảnh được dịch chuyển theo công thức sau:  
<img width="443" height="22" alt="image" src="https://github.com/user-attachments/assets/a5dd15c7-1837-407a-9a61-79ae96172e27" />  

--> Kết quả:  
<img width="506" height="419" alt="image" src="https://github.com/user-attachments/assets/49ffafca-2926-458f-a38b-4131ae2e6954" />  

#### Rotation  
Chúng ta có thể sử dụng hàm cv2.getRotationMatrix2D:  
- center (tâm xoay): Là điểm mốc đẻ thực hiện phép xoay ảnh trên ảnh gốc.
- angle (góc xoay): Độ xoay của ảnh.
- scale (tỷ lệ): Co dãn ảnh.

Giả sử cho góc xoay theta = 45 độ:  

<img width="645" height="24" alt="image" src="https://github.com/user-attachments/assets/db36b135-64b3-40d6-92e8-e2339ea660f4" />  

--> Kết quả:  
<img width="432" height="420" alt="image" src="https://github.com/user-attachments/assets/e3b45280-abf4-4ccb-8ced-7b06a75dc2f0" />  

### 2. Mathematical Operations  
#### Array Operations  
- Giả sử phép cộng vô hướng vào một ma trận, mỗi ma trận trong ảnh sẽ được cộng thêm 20 đơn vị:  
<img width="169" height="21" alt="image" src="https://github.com/user-attachments/assets/57a2d44b-6010-42c8-925c-f0e3ab26be60" />

--> Kết quả:  
<img width="432" height="420" alt="image" src="https://github.com/user-attachments/assets/fcd79081-54ef-4a7a-b2b6-93fdb884d733" />  

- Giả sử nhân mỗi ma trận trong ảnh thêm 10 đơn vị:
<img width="168" height="19" alt="image" src="https://github.com/user-attachments/assets/3c3ff409-4ea0-496b-9f55-855f09e6c73e" />

--> Kết quả:  
<img width="431" height="420" alt="image" src="https://github.com/user-attachments/assets/a901f6f8-e499-41c2-914f-3b3e7687264d" />  

- Sử dụng nhiễu:
``` python
Noise = np.random.normal(0, 20, (rows, cols, 3)).astype(np.uint8)
```
<img width="195" height="29" alt="image" src="https://github.com/user-attachments/assets/04bd3061-18a4-470d-9862-f8c13a4fdabd" />  

--> Kết quả:  
<img width="431" height="420" alt="image" src="https://github.com/user-attachments/assets/f2863c04-f88c-49eb-abb2-f499c9bf9d8d" />  

#### Matrix Operations  
<img width="391" height="22" alt="image" src="https://github.com/user-attachments/assets/56bc5df1-096c-4724-989e-81b4acda0ead" />  

Đây là lệnh thực hiện phép Phân tách giá trị đơn lẻ (Singular Value Decomposition - SVD):  
- U: Ma trận trực giao (cột là các vector suy biến trái).  
- s: Một vector chứa các giá trị đơn lẻ (singular values) sắp xếp giảm dần. Chúng đại diện cho "tầm quan trọng" của các thành phần trong ảnh.  
- V: Ma trận trực giao (hàng là các vector suy biến phải).

<img width="839" height="421" alt="image" src="https://github.com/user-attachments/assets/05d21f55-6a26-4de3-aeee-36bfc8151f93" />  

--  

<img width="97" height="19" alt="image" src="https://github.com/user-attachments/assets/ba480d50-434c-42c1-ade9-7b5faa40edda" />  

Đây là dòng thực hiện phép nhân ma trận giữa ma trận đường chéo S và ma trận V.  Kết quả B là một ma trận trung gian đã đưa vào các trọng số từ S vào V.  

## Phần 3: Thực hành Image Filter  
- Cho ảnh gốc:
<img width="341" height="420" alt="image" src="https://github.com/user-attachments/assets/6c157b3a-d86c-4080-bce5-fe70886b0dd7" />  

### Câu 1: Sử dụng boxFilter: cv2.blur() hoặc cv2.boxFilter() để làm mờ ảnh (sử dụng nhiều thông số filter khác nhau), biểu diễn ảnh gốc và ảnh làm mờ cùng nhau để kiểm chứng.  
Cách làm:  
<img width="216" height="22" alt="image" src="https://github.com/user-attachments/assets/7d4bb4a7-8505-4402-aa59-e2535177171b" />  

--> Kết quả:  
<img width="343" height="420" alt="image" src="https://github.com/user-attachments/assets/d1e53497-9186-4ed3-b172-f064d43522fe" />  

### Câu 2: Sử dụng Gaussian Filter # Lưu ý: kích thước bộ lọc là số lẻ.  
Cách làm:  
<img width="300" height="24" alt="image" src="https://github.com/user-attachments/assets/592affab-c377-4496-a26d-974bcd9a8f88" />  

--> Kết quả:  
<img width="340" height="419" alt="image" src="https://github.com/user-attachments/assets/9107b5b6-bce6-4b45-9fdf-71b0f29a72e1" />  

### Câu 3: Sử dụng Median Filter  
Cách làm:  
<img width="249" height="23" alt="image" src="https://github.com/user-attachments/assets/b7a24279-f3ca-4c3a-b910-e0c467237437" />  

--> Kết quả:  
<img width="341" height="419" alt="image" src="https://github.com/user-attachments/assets/b2a4895e-e7d7-4822-ab46-a54fdf87303c" />  

### Câu 4: Kiểm tra lại các bộ lọc trên với hai hình ảnh pepper noise dưới đây:  
pepper_noise01.png  
<img width="255" height="253" alt="image" src="https://github.com/user-attachments/assets/02e29585-4987-4fd5-849e-6a02340c4727" />  

Cách làm:  
```python
img_pepper01 = cv2.imread('pepper_noise01.png')
img_pepper01a = cv2.blur(img_pepper01, (110,110))
img_pepper01b = cv2.GaussianBlur(img_pepper01, (11,11), 0)
img_pepper01c = cv2.medianBlur(img_pepper01, 15, 0)
```
--> Kết quả:  
<img width="495" height="421" alt="image" src="https://github.com/user-attachments/assets/6a1d4380-354c-4d74-801b-52ec989f563b" />  

pepper_noise02.png  
<img width="425" height="284" alt="image" src="https://github.com/user-attachments/assets/a4309628-b9a0-475f-b913-7334d25f910b" />  

Cách làm:  
```python
img_pepper02 = cv2.imread('pepper_noise02.png')
img_pepper02a = cv2.blur(img_pepper02, (110,110))
img_pepper02b = cv2.GaussianBlur(img_pepper02, (11,11), 0)
img_pepper02c = cv2.medianBlur(img_pepper02, 15, 0)
```

--> Kết quả:  
<img width="553" height="399" alt="image" src="https://github.com/user-attachments/assets/0b407aef-8f30-4f9a-af7f-2de5c0b11480" />  

### Câu 5: Có nhận xét gì về các kích thước filter.  
- Filter phải ma trận hoặc kích thước lẻ 3x3, 5x5, 11x11, ...  
- Kích thước phải nhỏ và vừa tránh làm quá mờ ảnh.

### Câu 6: Thực hành với Cân bằng sáng - equalizeHist, để cân bằng sáng, trước hết ta chuyển ảnh trắng đen (nếu có) sang ảnh màu.  
pepper_noise01.png  
<img width="255" height="253" alt="image" src="https://github.com/user-attachments/assets/02e29585-4987-4fd5-849e-6a02340c4727" />  

Cách làm:  
```python
blur = cv2.medianBlur(img, 5)
gray_blur = cv2.cvtColor(blur, cv2.COLOR_BGR2GRAY)
ehist = cv2.equalizeHist(gray_blur)
```

--> Kết quả:  
<img width="553" height="195" alt="image" src="https://github.com/user-attachments/assets/ed2296e3-6c87-4c4a-8323-a2d5d16b070c" />  

pepper_noise02.png  
<img width="425" height="284" alt="image" src="https://github.com/user-attachments/assets/a4309628-b9a0-475f-b913-7334d25f910b" />  

Cách làm:  
```python
blur = cv2.medianBlur(img, 5)
gray_blur = cv2.cvtColor(blur, cv2.COLOR_BGR2GRAY)
ehist = cv2.equalizeHist(gray_blur)
```
--> Kết quả:  
<img width="553" height="148" alt="image" src="https://github.com/user-attachments/assets/d9512435-f018-41a4-b144-1967c30e9460" />  

### Câu 7: Bài tập trên lớp lý thuyết: FILTER bằng các phép toán số học và logic Given two images as follow (with different sizes: 193x157 and 194x160)   
#### a. Crop two images to size 190x155  
Cách làm:  
<img width="175" height="38" alt="image" src="https://github.com/user-attachments/assets/e0748f2b-7f57-4b18-be47-8daf172e619e" />  

--> Kết quả:  
<img width="534" height="416" alt="image" src="https://github.com/user-attachments/assets/ec4c200d-8197-44b3-bbd5-3fe7e2ae1f90" />  

#### b. Transform images to negative ones.  
Cách làm:  
<img width="387" height="25" alt="image" src="https://github.com/user-attachments/assets/f006fae6-b294-414e-af3b-1621832405c2" />  

--> Kết quả:  
<img width="510" height="418" alt="image" src="https://github.com/user-attachments/assets/792adf97-9eb4-4df8-a832-460230ed3e04" />  

#### c. Process to have an image which has only the “ball” Nếu vẫn còn xuất hiện các vạch trắng, cách khắc phục như thế nào?  
Cách làm:  
<img width="378" height="25" alt="image" src="https://github.com/user-attachments/assets/7f5e1e25-1513-4b87-8e67-f6e16945e9b5" />  

--> Kết quả:  
<img width="510" height="418" alt="image" src="https://github.com/user-attachments/assets/defaec9c-fac3-4731-b2c4-51732143a69f" />  

## Bài tập thêm  
- Sử dụng lại ảnh cat.jpg
<img width="343" height="418" alt="image" src="https://github.com/user-attachments/assets/bcbc4c02-db9f-487b-b824-63234596001e" />  

### Câu 1: Sử dụng Backward, forward, central gradient để lọc ảnh.  
Cách làm:  
<img width="465" height="203" alt="image" src="https://github.com/user-attachments/assets/9893c175-124a-4ba5-9def-d1074ad31e3d" />  

--> Kết quả:  
<img width="780" height="683" alt="image" src="https://github.com/user-attachments/assets/c4675833-628f-4cc3-9fa2-783b2ce5f7fb" />  

### Câu 2: Sử dụng Finite difference filter để lọc ảnh nhiễu.  
Cách làm:  
<img width="409" height="82" alt="image" src="https://github.com/user-attachments/assets/dde182c0-2202-4a25-909b-c5e39623719c" />  

--> Kết quả:  
<img width="467" height="236" alt="image" src="https://github.com/user-attachments/assets/49f055a6-0a1d-46fe-8ee6-5c3b236c7abc" />  

### Câu 3: Sử dụng Gaussian filter để lọc ảnh.  
Cách làm: Sử dụng Gaussian 15x15.  
<img width="357" height="23" alt="image" src="https://github.com/user-attachments/assets/491a5a9b-d67f-4cc1-9170-a0fb0b8ac480" />  

--> Kết quả:  
<img width="462" height="234" alt="image" src="https://github.com/user-attachments/assets/6c7e23be-1ab8-447b-aa53-8862abc98136" />  

### Câu 4: Sử dụng Sobel detector để xác định biên của ảnh.  
Cách làm:  
- 1, 0: Đạo hàm theo trục X (ngang) là bậc 1, trục Y là bậc 0 giúp phát hiện các đường biên cứng.
- ksize = 3: Kích thước ma trận Sobel là 3x3.  
<img width="424" height="62" alt="image" src="https://github.com/user-attachments/assets/a758058e-847a-4e68-b79f-488d1f52dfe8" />  

--> Kết quả:  
<img width="462" height="233" alt="image" src="https://github.com/user-attachments/assets/31546f57-1b76-4b25-ab9c-f1871c5b555f" />  

### Câu 5: Sử dụng Canny edge detector để xác định các cạnh góc ảnh.  
Cách làm: Cho ngưỡng thấp là 50 và ngưỡng cao là 150.  
<img width="330" height="39" alt="image" src="https://github.com/user-attachments/assets/434ac0bc-ebd4-4652-94b9-b3365a5eb61c" />  

--> Kết quả:  
<img width="487" height="234" alt="image" src="https://github.com/user-attachments/assets/b97530fb-305f-4d00-933f-6d6ff8e31259" />  

### Câu 6: Sử dụng Hough transform để xác định các đường thẳng trong ảnh.  
Cách làm:  
- 1 (rho): Độ phân giải khoảng cách của tham số trong không gian Hough (tính bằng pixel).  
- np.pi/180: Độ phân giải góc của tham số trong không gian Hough.  
- threshold = 100: Số lần giao cắt tối thiểu trong không gian Hough để là một đường thẳng.
- minLineLength = 50: Độ dài tối thiểu của một đoạn thẳng.
- maxLineGap = 10: Khoảng cách tối đa giữa các đoạn thẳng để có thể nối chúng thành một đường duy nhất.  
<img width="677" height="42" alt="image" src="https://github.com/user-attachments/assets/3a54c072-0fc5-4285-93a6-52bbcb754847" />  

--> Kết quả:  
<img width="470" height="234" alt="image" src="https://github.com/user-attachments/assets/bbed6032-1bc2-4181-9e73-f0d586cac746" />  

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



















































 

















