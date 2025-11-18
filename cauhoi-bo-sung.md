# BỘ CÂU HỎI TRẮC NGHIỆM BỔ SUNG

> Dựa trên nội dung trong `tomtat-noidung.md` – đã đánh dấu sẵn đáp án đúng.

## A. Lọc ảnh & Biến đổi

**Câu 1.** Bộ lọc nào sau đây có tổng hệ số kernel bằng 0, thích hợp để làm sắc nét (sharpening)?  
A. Mean 3×3  
B. Gaussian 5×5  
✅ C. Sobel X  
D. Box filter 5×5  

**Câu 2.** Khi tăng giá trị σ của Gaussian filter, hiệu ứng nào xảy ra rõ nhất?  
A. Ảnh sắc nét hơn, biên rõ hơn  
✅ B. Ảnh mờ hơn, mất chi tiết nhỏ  
C. Ảnh không thay đổi nhiều  
D. Ảnh xuất hiện ringing  

**Câu 3.** Biến đổi Gamma với γ < 1 thường dùng để:  
A. Làm tối vùng sáng  
✅ B. Làm sáng vùng tối  
C. Tạo ảnh nhị phân  
D. Xóa biên ảnh  

**Câu 4.** Ưu điểm chính của Median filter so với Mean filter là:  
A. Tính nhanh hơn  
B. Loại bỏ nhiễu Gaussian tốt hơn  
✅ C. Bảo toàn cạnh, loại bỏ nhiễu salt-pepper tốt hơn  
D. Có thể tách thành 2D = 1D×1D  

**Câu 5.** Bộ lọc nào dưới đây thường gây hiện tượng ringing mạnh nhất trong miền không gian?  
A. Gaussian low-pass  
✅ B. Ideal low-pass  
C. Butterworth low-pass bậc thấp  
D. Median filter  

**Câu 6.** DCT (Discrete Cosine Transform) được nhắc đến chủ yếu với vai trò:  
A. Phát hiện biên trong ảnh  
✅ B. Nén ảnh và gom năng lượng vào hệ số thấp  
C. Tìm đường thẳng trong ảnh  
D. Phát hiện góc (corner)  

**Câu 7.** Wavelet transform có ưu điểm nổi bật so với DFT/DCT ở điểm:  
A. Không cần tính toán trong miền tần số  
✅ B. Cung cấp thông tin cả miền thời gian (không gian) và tần số  
C. Không cần kernel  
D. Không dùng trong nén hoặc khử nhiễu  

## B. Hình thái học & Segmentation

**Câu 8.** Phép toán nào thích hợp để loại bỏ các đối tượng nhỏ sáng trên nền tối mà vẫn giữ hình dạng các đối tượng lớn?  
A. Closing  
✅ B. Opening  
C. Dilation  
D. Erosion  

**Câu 9.** Watershed segmentation thường gặp vấn đề over-segmentation. Theo tài liệu, giải pháp chính là:  
A. Giảm kích thước ảnh  
B. Tăng cường nhiễu  
✅ C. Sử dụng marker và làm trơn trước  
D. Chuyển sang không gian HSV  

**Câu 10.** Phương pháp nào yêu cầu histogram của ảnh có 2 đỉnh rõ rệt để hoạt động tốt?  
A. Watershed  
B. Region Growing  
✅ C. Otsu Thresholding  
D. Graph-based segmentation  

**Câu 11.** Đặc điểm nào đúng nhất về Region Growing?  
A. Không cần seed point  
B. Dễ áp dụng với ảnh nhiễu nặng  
✅ C. Nhạy với seed và nhiễu  
D. Chỉ dùng được cho ảnh nhị phân  

**Câu 12.** Structuring element (SE) trong morphology càng lớn thì:  
A. Hiệu ứng càng yếu  
B. Không ảnh hưởng đến kết quả  
✅ C. Hiệu ứng mạnh hơn, dễ phá chi tiết nhỏ  
D. Ảnh luôn sắc nét hơn  

## C. Edge, Hough, RANSAC

**Câu 13.** Trong Canny, bước Non-maxima Suppression nhằm mục đích:  
A. Giảm nhiễu Gaussian  
✅ B. Chỉ giữ lại các điểm là cực đại theo hướng gradient  
C. Tạo mask nhị phân từ ảnh biên  
D. Tính hướng gradient  

**Câu 14.** Biến đổi Hough phát hiện đường thẳng dựa trên:  
A. Cực trị của đạo hàm bậc 2  
B. Zero-crossing của LoG  
✅ C. Bỏ phiếu trong không gian tham số $(\rho, \theta)$  
D. So khớp template  

**Câu 15.** RANSAC đặc biệt phù hợp khi dữ liệu có:  
A. Rất ít điểm dữ liệu  
✅ B. Nhiều outlier (điểm ngoại lai)  
C. Không có nhiễu  
D. Tập dữ liệu hoàn toàn tuyến tính  

## D. Feature, BoW, Clustering

**Câu 16.** Để đạt bất biến với scale, các detector hiện đại làm gì?  
A. Chỉ tăng contrast  
B. Tìm cực trị trên từng ảnh riêng lẻ  
✅ C. Tìm cực trị trên miền không gian-scale  
D. Chỉ dùng ảnh nhị phân  

**Câu 17.** Trong BoW cho ảnh, bước "Dictionary Learning" sử dụng:  
A. PCA trên đặc trưng toàn cục  
✅ B. K-means trên đặc trưng cục bộ  
C. RANSAC trên keypoints  
D. Hough transform trên histogram  

**Câu 18.** K-means phù hợp nhất với dạng cụm:  
A. Cụm bất kỳ, hình dạng bất kỳ  
✅ B. Cụm hình cầu/lồi, variance tương đối giống nhau  
C. Cụm rất lệch (elongated)  
D. Cụm chứa nhiều outlier nặng  

**Câu 19.** Thuật toán phân cụm nào không cần biết trước số cụm k?  
A. K-means  
B. K-medoids  
✅ C. Mean Shift  
D. GMM-EM  

**Câu 20.** Khi dữ liệu có nhiều outlier, theo tài liệu nên ưu tiên:  
A. K-means  
✅ B. K-medoids hoặc Mean Shift  
C. Agglomerative  
D. GMM-EM  

## E. Detection, Deep Learning & Metrics

**Câu 21.** RetinaNet cải thiện one-stage detector bằng cách:  
A. Dùng Selective Search  
✅ B. Dùng Focal Loss để xử lý mất cân bằng anchor  
C. Dùng Integral Image  
D. Thêm nhiều lớp FCN  

**Câu 22.** Trong phát hiện đối tượng, IoU (Intersection over Union) đo:  
A. Sự khác biệt màu sắc giữa 2 ảnh  
B. Độ trùng khớp giữa mask dự đoán và mask thật  
✅ C. Độ trùng khớp giữa box dự đoán và ground truth  
D. Tốc độ hội tụ của mô hình  

**Câu 23.** Precision cao nhưng Recall thấp thường có nghĩa là:  
A. Dự đoán rất nhiều nhưng sai nhiều  
✅ B. Dự đoán ít, nhưng phần lớn dự đoán là đúng  
C. Bỏ sót rất ít đối tượng  
D. Accuracy luôn cao  

**Câu 24.** Trong kiến trúc CNN, lớp Fully-Connected (FC) có vai trò:  
A. Thực hiện convolution  
B. Thực hiện pooling  
✅ C. Kết hợp đặc trưng thành vector và ra quyết định phân loại  
D. Chuẩn hóa dữ liệu đầu vào  

**Câu 25.** Transfer Learning giúp:  
A. Huấn luyện từ đầu các mô hình lớn  
✅ B. Dùng mô hình đã huấn luyện trước cho bài toán mới để giảm dữ liệu và thời gian  
C. Chỉ áp dụng được cho ảnh grayscale  
D. Không dùng được với CNN  

