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
