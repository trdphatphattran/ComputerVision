# LAB 5: PHÂN ĐOẠN ẢNH (IMAGE SEGMENTATION)  
## Thông tin  
Sinh viên: Trần Đại Phát  
MSSV: 2374802010379  
Môn học: Thị giác máy tính  
GVHD: Đỗ Hữu Quân  
Năm học: 2025 - 2026  

## Phần 1: Lý thuyết  
Phân đoạn ảnh (Image Segmentation) là quá trình chia một bức ảnh thành nhiều vùng (region) hoặc đối tượng có ý nghĩa, sao cho các pixel trong cùng một vùng có đặc điểm giống nhau (màu sắc, độ sáng, kết cấu, v.v.).  
## Phần 2: Bài tập  
### Bài 1: Thresholding để phân đoạn ảnh  
- Phân đoạn cơ bản: thresh_simple
```python
ret, thresh_simple = cv.threshold(gray, 127, 255, cv.THRESH_BINARY)
```
- Phân đoạn tự động: thresh_otsu
```python
ret2, thresh_otsu = cv.threshold(gray, 0, 255, cv.THRESH_BINARY + cv.THRESH_OTSU)  
```
--> Kết quả:  
<img width="708" height="405" alt="image" src="https://github.com/user-attachments/assets/96209ea4-b0a6-4380-92a2-cc48bdd32e85" />  

### Bài 2: Otsu algorithm để phân đoạn ảnh vân tay  
- Otsu tự động tìm ngưỡng tối ưu T. Phân tách thành nền (đen) và đường vân tay (trắng). Giá trị ret chính là ngưỡng T mà otsu tìm được.
```python
ret, thresh = cv.threshold(blur, 0, 255, cv.THRESH_BINARY + cv.THRESH_OTSU)
```
--> Kết quả:  
<img width="591" height="243" alt="image" src="https://github.com/user-attachments/assets/97cb0b4e-fcb5-488f-bb41-040831c75716" />  


### Bài 3: Clustering techniques trong phân đoạn ảnh, K-mean clustering  
- K-means nhóm các pixel có màu giống nhau vào cùng 1 cụm. Mỗi cụm đại diện bởi 1 màu trung tâm (center).
```python
K = 3 
ret, label, center = cv.kmeans(data, K, None, criteria, 10, cv.KMEANS_RANDOM_CENTERS)
```
--> Kết quả:  
<img width="709" height="405" alt="image" src="https://github.com/user-attachments/assets/ab39b52c-27eb-4570-8ecf-956e80188ba6" />


### Bài 4: Sử dụng thuật toán Region Growing  
- Chọn một điểm seed (điểm bắt đầu) ở giữa ảnh  
- So sánh các pixel xung quanh với seed  
- Nếu độ khác biệt nhỏ hơn ngưỡng (threshold) → đưa vào cùng vùng  
- Lặp lại để mở rộng vùng cho đến khi không còn pixel phù hợp
```python
def region_growing(img, seed, threshold):
    h, w = img.shape
    segmented = np.zeros_like(img)
    list_points = [seed]
    seed_value = img[seed]
    segmented[seed] = 255 

    while len(list_points) > 0:
        pix = list_points.pop(0)
        
        for x in range(-1, 2):
            for y in range(-1, 2):
                curr_x, curr_y = pix[0] + x, pix[1] + y
                
                if 0 <= curr_x < h and 0 <= curr_y < w:
                    if segmented[curr_x, curr_y] == 0:
                        diff = abs(int(img[curr_x, curr_y]) - int(seed_value))
                        if diff < threshold:
                            segmented[curr_x, curr_y] = 255
                            list_points.append((curr_x, curr_y))
    return segmented
```
--> Kết quả:  
<img width="839" height="478" alt="image" src="https://github.com/user-attachments/assets/16aed957-ed72-455e-8e2d-fc690716b8c9" />  

### Bài 5: Sử dụng thuật toán Split and Merge để phân đoạn ảnh  
- Split (chia nhỏ): Nếu vùng không đồng nhất → chia thành 4 phần.
- Merge (gộp): Nếu vùng đồng nhất (std < threshold) → gán cùng 1 giá trị.
```python
def split_region(img, x, y, w, h, threshold, mask):
    region = img[y:y+h, x:x+w]
    if check_homogeneity(region, threshold) or w <= 2 or h <= 2:
        mask[y:y+h, x:x+w] = np.mean(region)
    else:
        w2, h2 = w // 2, h // 2
        split_region(img, x, y, w2, h2, threshold, mask)          
        split_region(img, x + w2, y, w2, h2, threshold, mask)      
        split_region(img, x, y + h2, w2, h2, threshold, mask)      
        split_region(img, x + w2, y + h2, w2, h2, threshold, mask)
```
--> Kết quả:  
<img width="886" height="442" alt="image" src="https://github.com/user-attachments/assets/c2324f53-74a3-44dc-be8b-a00afa9c8c55" />  

### Bài 6: Phân đoạn ảnh với Edge-based segmentation  
- Dùng thuật toán Canny. Tìm các đường biên trong ảnh (nơi có sự thay đổi mạnh về độ sáng).
```python
edges = cv.Canny(blur, 100, 200)
```
--> Kết quả:  
<img width="694" height="403" alt="image" src="https://github.com/user-attachments/assets/974a2837-bf2f-41e2-9f43-f2f98af5fd9d" />  

# LAB 6: NHẬN DIỆN ẢNH (IMAGE DETECTION)  
## Phần 1: Lý thuyết  

## Phần 2: Bài tập  
### Bài 1: Tham khảo đoạn code trên để tạo 1 đoạn code mới, kết hợp sử dụng hình ảnh sau và file: haarcascade_frontalface_default.xml (tải về từ đường dẫn bên dưới) để nhận diện khuôn mặt:  

### Bài 2: Sử dụng các tham khảo và hình ảnh trên, có thể sử dụng thêm các ảnh tập thể, kỷ yếu khác để nhận diện: Nụ cười, tai, mắt, mũi, miệng, … của người trong bức ảnh.  

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


