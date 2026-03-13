# LAB 6: Keypoint Detection  
## Thông tin  
Sinh viên: Trần Đại Phát  
MSSV: 2374802010379  
Môn học: Thị giác máy tính  
GVHD: Đỗ Hữu Quân  
Năm học: 2025 - 2026  

## Phần 1: Lý thuyết  
### 1. Keypoint Detection là gì?  
- Keypoint Detection (Phát hiện điểm đặc trưng) là quá trình xác định các điểm "quan trọng" hoặc "thú vị" trong một bức ảnh. Những điểm này mang thông tin đặc biệt giúp máy tính có thể nhận diện, theo dõi hoặc khớp nối các bức ảnh với nhau.

### 2. Các đặc trưng  
- Một Keypoint là một vị trí $(x, y)$ trong ảnh mà tại đó có sự thay đổi rõ rệt về cường độ sáng theo nhiều hướng.
  - Đặc điểm: Một điểm được coi là keypoint tốt nếu nó độc nhất và dễ nhận diện lại khi ảnh bị xoay, thay đổi ánh sáng hoặc thay đổi góc chụp.
  - Ví dụ: Các góc (corners), các đốm (blobs) hoặc các điểm giao nhau giữa các cạnh thường là những keypoint lý tưởng. Các vùng phẳng (flat) hoặc đường thẳng (edges) thường không được chọn làm keypoint vì chúng dễ gây nhầm lẫn.
 
### 3. Các tính chất  
- Để một thuật toán phát hiện điểm đặc trưng hoạt động hiệu quả, nó cần đảm bảo các tính chất sau:  
  - Tính bất biến (Invariance): Nếu ảnh bị xoay (rotation) hoặc thay đổi độ sáng (illumination), thuật toán vẫn phải tìm ra đúng điểm đó.  
  - Tính độc lập quy mô (Scale Invariance): Dù vật thể ở xa (nhỏ) hay ở gần (to), điểm đặc trưng vẫn phải được phát hiện chính xác.  
  - Tính lặp lại (Repeatability): Nếu chụp hai bức ảnh của cùng một cảnh, thuật toán phải tìm thấy cùng một tập hợp các điểm đặc trưng trên cả hai ảnh.  

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
<img width="547" height="296" alt="Image" src="https://github.com/user-attachments/assets/b46af11e-47e1-47a0-946a-efa1152dbd2a" />  

### Bài 2: Sử dụng Harris Corner Detection tìm các keypoint trong ảnh  
```python
dst = cv2.cornerHarris(gray, 2, 3, 0.04)
dst = cv2.dilate(dst, None)
img[dst > 0.01 * dst.max()] = [0, 0, 255]
```
Nguyên lý hoạt động của code:  

<img width="234" height="40" alt="Image" src="https://github.com/user-attachments/assets/01a37324-1b62-4f01-ab2d-716fe0b25380" />  

- Nếu R lớn: Đó là góc.
- Nếu R < 0: Đó là cạnh.
- Nếu |R| nhỏ: Đó là phẳng.

--> Kết quả:  
<img width="550" height="297" alt="Image" src="https://github.com/user-attachments/assets/e5f5ca78-4c74-42dc-90e4-8b8b6605105c" />  

### Bài 3: Sử dụng Band-pass filtering by Difference of Gaussians  
```python
blur1 = cv2.GaussianBlur(gray, (5, 5), sigmaX=1.0)
blur2 = cv2.GaussianBlur(gray, (5, 5), sigmaX=2.0)
dog = blur1 - blur2
```
Toán tử DoG xấp xỉ toán tử LoG, giúp phát hiện sự thay đổi cường độ sáng:  

<img width="330" height="41" alt="Image" src="https://github.com/user-attachments/assets/dd787306-9c54-449b-a6fb-9d4611bf4836" />  

--> Kết quả:  
<img width="551" height="294" alt="Image" src="https://github.com/user-attachments/assets/b0ff9f01-c720-4a2d-95cc-ed65bf951d45" />  

### Bài 4: Kiểm tra ảnh qua Automatic Scale Selection  
```python
blur = cv2.GaussianBlur(gray_float, (ksize, ksize), sigma)
log_normalized = cv2.Laplacian(blur, cv2.CV_32F) * (sigma**2)
```
Nếu sigma càng lớn, ảnh càng mờ, đồng nghĩa với việc các chi tiết nhỏ bị loại bỏ, chỉ còn lại các vùng lớn.  
--> Kết quả:  

<img width="550" height="291" alt="Image" src="https://github.com/user-attachments/assets/9c3942a4-aa35-47ab-a089-f92e479bb9a4" />  

### Bài 5: Kiểm tra ảnh qua Scale Invariant Detection  
```python
dst = cv2.cornerHarris(gray_float, blockSize=int(2*sigma), ksize=3, k=0.04)
dst = cv2.dilate(dst, None)
```
Nếu vật thể to, alpha lớn -> blocksize lớn -> máy tính sẽ quét trên diện rộng -> nhận diện được các góc lớn mà không bị nhiễu bởi các chi tiết nhỏ.  
--> Kết quả:  

<img width="546" height="294" alt="Image" src="https://github.com/user-attachments/assets/70e16ce7-4f76-4135-bbbf-a1b0255baa08" />  

### Bài 6: Kiểm tra ảnh qua Scale-space blob detector  
```python
log = cv2.Laplacian(blur, cv2.CV_32F) * (sigma**2)
scale_space.append(np.abs(log))
&
  if val > threshold and val == np.max(scale_space[i-1:i+2, y-1:y+2, x-1:x+2]):
    radius = int(sigmas[i] * np.sqrt(2))
    cv2.circle(result_img, (x, y), radius, (0, 255, 255), 1)
```
Tạo ra một ảnh Laplacian ở nhiều mức độ mờ khác nhau.  
--> Kết quả:  

<img width="547" height="296" alt="Image" src="https://github.com/user-attachments/assets/872034d2-ba4f-4307-b690-fbaaab4f7fa5" />  

### Bài 7: Thực hành với Bag-of-words detection  
```python
k = 20
kmeans = KMeans(n_clusters=k, n_init=10, random_state=0)
kmeans.fit(descriptors)
```
Vì có quá nhiều mảnh ghép (hàng ngàn cái), máy tính không thể nhớ hết được. Nó dùng thuật toán K-Means để nhóm những mảnh ghép trông giống nhau lại thành một nhóm. Ở đây k = 20 nghĩa là ta ép máy tính phải tạo ra đúng 20 nhóm mẫu. Mỗi nhóm đại diện cho một loại chi tiết tiêu biểu.  
--> Kết quả:  

<img width="548" height="412" alt="Image" src="https://github.com/user-attachments/assets/07a0aae9-d6ac-4f20-8248-58335c35c015" />  

### Bài 8: Ghép ảnh Image Panoramas  
```python
bf = cv2.BFMatcher()
matches = bf.knnMatch(des1, des2, k=2)

good_matches = []
for m, n in matches:
    if m.distance < 0.75 * n.distance:
        good_matches.append(m)
&
H, mask = cv2.findHomography(dst_pts, src_pts, cv2.RANSAC, 5.0)
```
Để dán hai bức ảnh lại với nhau, máy tính cần biết chúng khớp nhau ở đâu. Nó lấy các mảnh ghép từ ảnh trái đối chiếu với ảnh phải. Chỉ những cặp nào cực kỳ giống nhau mới được giữ lại.  
--> Kết quả:  

<img width="551" height="224" alt="Image" src="https://github.com/user-attachments/assets/bb7d5868-906a-435f-932d-ae7d4d70cedc" />  

### Bài 9: Ghép ảnh Automatic mosaicing  
```python
stitcher = cv2.Stitcher_create(cv2.Stitcher_PANORAMA)
status, result = stitcher.stitch(images)
```
Chúng ta chỉ cần đưa vào tập hợp các ảnh, sau đó máy tính tự so khớp từng điểm ảnh lại với nhau và nó tự ghép lại thành một ảnh hoàn chỉnh.  
--> Kết quả:  

<img width="551" height="269" alt="Image" src="https://github.com/user-attachments/assets/09064915-79ef-4024-8409-cd8ac2fa78c6" />  

### Bài 10: Sử dụng Wide base-line stereo  
```python
sift = cv2.SIFT_create()
kp1, des1 = sift.detectAndCompute(gray1, None)
kp2, des2 = sift.detectAndCompute(gray2, None)
&
FLANN_INDEX_KDTREE = 1
index_params = dict(algorithm=FLANN_INDEX_KDTREE, trees=5)
search_params = dict(checks=50)
flann = cv2.FlannBasedMatcher(index_params, search_params)
matches = flann.knnMatch(des1, des2, k=2)
&
  F, mask = cv2.findFundamentalMat(pts1, pts2, cv2.FM_RANSAC, 3.0, 0.99)
```
Sử dụng SIFT để phát hiện ra các keypoints detection ổn định nhất, đây là bước quan trọng nhất cho Wide Baseline Stereo. Sau đó chúng ta dùng FLANN để tìm feature tương ứng giữa 2 ảnh.  
--> Kết quả:  

<img width="1212" height="467" alt="Image" src="https://github.com/user-attachments/assets/87d4fbcc-db38-4bdd-baf1-b58362016b08" />  

### Bài 11: CBIR (content-based image retrieval)  
```python
    hist1 = cv2.calcHist([hsv_img1], [0, 1], None, [50, 60], [0, 180, 0, 256])
    hist2 = cv2.calcHist([hsv_img2], [0, 1], None, [50, 60], [0, 180, 0, 256])
&
    similarity = cv2.compareHist(hist1, hist2, cv2.HISTCMP_CORREL)
```
CBIR được thể hiện qua việc so sánh đặc trưng màu sắc giữa hai bức ảnh để tính toán độ tương đồng, bằng cách phân tích chính dữ liệu pixel bên trong ảnh.  
--> Kết quả:  

<img width="790" height="297" alt="Image" src="https://github.com/user-attachments/assets/fb93f051-49f3-49e0-ac0d-6a0394b6eac5" />  

### Bài 12: Bag-of-word with SIFT + Histogram  
```python
def build_histogram(descriptors, kmeans, k):
    labels = kmeans.predict(descriptors)
    hist, _ = np.histogram(labels, bins=range(k + 1))
    return hist.astype(float) / np.sum(hist)
```
Đầu vào của hàm này chính là các mô tả SIFT. SIFT cung cấp các nội dung (như góc cạnh, ...) thay vì chỉ là màu sắc đơn thuần. Mỗi điểm SIFT sẽ được gán cho một nhãn tương ứng với điểm gần giống nó nhất.  
--> Kết quả:  

<img width="558" height="408" alt="Image" src="https://github.com/user-attachments/assets/eb386b49-e0d2-4282-9d1d-f9c935a65089" />  

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

