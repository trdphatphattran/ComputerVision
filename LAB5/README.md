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
```python
kernel = np.ones((5,5))/36
```

- Tạo bộ lọc kernel
```python
kernel_filter = ImageFilter.Kernel((5,5), kernel.flatten())
```

- Áp dụng bộ lọc lên ảnh nhiễu để giảm noise
```python
image_filtered = noisy_image.filter(kernel_filter)
```

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
```python
sharpened = image.filter(kernel)
```

--> Kết quả  
<img width="831" height="413" alt="image" src="https://github.com/user-attachments/assets/0b333ef3-10b4-4aea-bf60-312a0ab7f559" />  

Hoặc ta có thể sử dụng ImageFilter.SHARPEN  
```python
sharpened = image.filter(ImageFilter.SHARPEN)
```

### 2. Edges  
Edges là những vị trí trong ảnh nơi cường độ pixel thay đổi mạnh. Gradient được dùng để đo tốc độ thay đổi này và có thể được xấp xỉ bằng phép convolution trên ảnh xám để phát hiện các cạnh trong ảnh.  
- Sử dụng ImageFilter.EDGE_ENHANCE để làm nổi bật các cạnh trong ảnh xám.
```python
img_gray = img_gray.filter(ImageFilter.EDGE_ENHANCE)
```

--> Kết quả  
<img width="431" height="416" alt="image" src="https://github.com/user-attachments/assets/6e972c0f-5610-46d8-bb9c-ef9ed6cc675b" />  

- Sử dụng ImageFilter.FIND_EDGES để phát hiện các cạnh trong ảnh.  
```python
img_gray = img_gray.filter(ImageFilter.FIND_EDGES)
```

--> Kết quả  
<img width="817" height="806" alt="image" src="https://github.com/user-attachments/assets/547596d4-8938-46c1-a2f8-bb4d097dfabe" />  


### 3. Median  
Median filter là phương pháp lọc ảnh bằng cách lấy giá trị trung vị (median) của các pixel trong vùng kernel, sau đó thay thế giá trị pixel trung tâm bằng giá trị này. Phương pháp này thường được dùng để giảm nhiễu trong ảnh.  
- Sử dụng thư viện ImageFilter.MedianFilter để giảm nhiễu trong ảnh.
```python
image = image.filter(ImageFilter.MedianFilter)
```

--> Kết quả
<img width="814" height="807" alt="image" src="https://github.com/user-attachments/assets/e47878f1-89d3-43ec-8df3-2475fce666b1" />  

## Phần 2: Với OpenCV  
### 1. Linear Filtering  
#### Filtering noise  
- Dùng hàm filter2D để lọc nhiễu
```python
image_filtered = cv2.filter2D(src=noisy_image, ddepth=-1, kernel=kernel)
```

--> Kết quả  
<img width="829" height="410" alt="image" src="https://github.com/user-attachments/assets/a963a080-88c2-46be-8f70-73335ee2de9d" />  

#### Gaussian Blur  
- Dùng hàm GaussianBlur để tiến hành lọc nhiễu với 2 độ lệch chuẩn là sigmaX và sigmaY  
```python
image_filtered = cv2.GaussianBlur(noisy_image,(5,5),sigmaX=4,sigmaY=4)
```

--> Kết quả  
<img width="827" height="408" alt="image" src="https://github.com/user-attachments/assets/7e9a3cb8-83ca-4a05-b81a-f30d3b355e7e" />  

#### Image sharpening  
- Dùng hàm filter2D để làm sắc nét ảnh.
```python
sharpened = cv2.filter2D(image, -1, kernel)
```

--> Kết quả  
<img width="826" height="413" alt="image" src="https://github.com/user-attachments/assets/043101a5-2cb7-4153-aae8-be181af10868" />

### 2. Edges  
- Dùng Sobel filter để phát hiện cạnh theo chiều ngang theo hướng X.
```python
grad_x = cv2.Sobel(src=img_gray, ddepth=ddepth, dx=1, dy=0, ksize=3)
```

--> Kết quả  
<img width="424" height="409" alt="image" src="https://github.com/user-attachments/assets/19b2500c-3e4e-43a7-92cd-7e68383b0647" />  

- Dùng Sobel filter để phát hiện cạnh theo chiều dọc theo hướng Y.
```python
grad_y = cv2.Sobel(src=img_gray, ddepth=ddepth, dx=0, dy=1, ksize=3)
```

--> Kết quả  
<img width="423" height="408" alt="image" src="https://github.com/user-attachments/assets/86788bd8-764f-4fba-b6bb-326e9f41d2bd" />  

- Chuyển các giá trị gradient về khoảng 0–255 để hiển thị được trên ảnh.
```python
abs_grad_x = cv2.convertScaleAbs(grad_x)
abs_grad_y = cv2.convertScaleAbs(grad_y)
```

- Kết hợp gradient theo X và Y để tạo ảnh phát hiện cạnh.
```python
grad = cv2.addWeighted(abs_grad_x, 0.5, abs_grad_y, 0.5, 0)
```

--> Kết quả  
<img width="812" height="811" alt="image" src="https://github.com/user-attachments/assets/c5f02ff0-6a92-4a4b-ae79-1845ed6fb6a7" />  

### 3. Median  
- Sử dụng hàm medianBlur để giảm nhiễu.
```python
filtered_image = cv2.medianBlur(image, 5)
```

--> Kết quả  
<img width="817" height="806" alt="image" src="https://github.com/user-attachments/assets/e9f741f3-4f6b-4471-94b8-50c547cc1885" />  

### 4. Threshold  
Thresholding là phương pháp phân tách ảnh dựa trên giá trị cường độ pixel. Mỗi pixel sẽ được so sánh với một ngưỡng (threshold); nếu lớn hơn hoặc nhỏ hơn ngưỡng thì sẽ được gán một giá trị khác (thường là 0 hoặc 255). Khi sử dụng THRESH_BINARY_INV, pixel trên ngưỡng sẽ thành 0 (đen) và pixel dưới hoặc bằng ngưỡng sẽ thành 255 (trắng). Nếu dùng THRESH_OTSU, OpenCV sẽ tự động chọn ngưỡng tối ưu thay vì dùng giá trị threshold do người dùng đặt.  

```python
ret, outs = cv2.threshold(src = image, thresh = 0, maxval = 255, type = cv2.THRESH_OTSU+cv2.THRESH_BINARY_INV)
```

--> Kết quả  
<img width="818" height="806" alt="image" src="https://github.com/user-attachments/assets/9f14a3df-1bce-436d-8637-db1832d01c76" />  

## Bài tập thêm  
### Feature detection and image matching  
#### 1. Thực hành xử lý ảnh trong miền tần số  
- Fast Fourier Transform (FFT) để phát hiện ảnh mờ.
- Sử dụng dft trong thư viện cv2, sau đó đưa ảnh về dạng số phức.
```python
dft = cv2.dft(img_float32, flags=cv2.DFT_COMPLEX_OUTPUT)
```
- Đưa về thang log để giảm sự chênh lệch lớn giữa các giá trị biên độ trong phổ tần số, giúp hiển thị và quan sát các tần số rõ hơn.  
```python
magnitude_spectrum = 20 * np.log(cv2.magnitude(dft_shift[:, :, 0], dft_shift[:, :, 1]))
```
--> Kết quả  
<img width="515" height="322" alt="image" src="https://github.com/user-attachments/assets/4953e68c-575d-4413-be67-f2f7f51c99d8" />  

#### 3. Sử dụng FFT Magnitude algorithm để phát hiện ảnh mờ  
<img width="449" height="77" alt="image" src="https://github.com/user-attachments/assets/60ee94b0-c2a6-46f9-a831-7906fb3f8808" />  

--> Kết quả  
<img width="673" height="674" alt="image" src="https://github.com/user-attachments/assets/e54c0b75-2709-48b6-8448-45d0cae4a674" />  

### Thực hành Harris corner detection  
- Dùng để phát hiện các góc trong ảnh.
```python
  dst = cv2.cornerHarris(gray, blockSize, ksize, k)
```
- Đánh dấu các góc phát hiện được bằng màu đỏ.
```python
  img[dst>threshold*dst.max()]=[0, 0, 255]
```
--> Kết quả  
<img width="491" height="608" alt="image" src="https://github.com/user-attachments/assets/f31cb963-cadd-4f38-adac-39b8b6b73d6b" />  

- Hoặc thử cách khác
```python
dst = cv2.cornerHarris(gray, 2, 3, 0.04)
dst = cv2.dilate(dst, None)
img[dst > 0.01 * dst.max()] = [0, 0, 255]
```

### Band-pass filtering by Difference of Gaussians  
- Phân tích tần số của ảnh trước và sau khi lọc bằng Difference of Gaussians (DoG).  
```python
filtered_image = difference_of_gaussians(wimage, 1, 12)
```
- Theo nguyên lý hoạt động:  DoG = Gaussian(sigma1) − Gaussian(sigma2).
--> Kết quả
<img width="673" height="676" alt="image" src="https://github.com/user-attachments/assets/891065fe-edcd-483c-b0f2-d934dde16bf8" />  

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
