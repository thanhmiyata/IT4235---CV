# ĐỀ XUẤT ÔN TẬP MÔN THỊ GIÁC MÁY TÍNH

## 📋 I. CÁC ĐIỂM CẦN BỔ SUNG VÀO TÀI LIỆU

### 1. **Các Metric Đánh Giá (Evaluation Metrics)**
*Hiện tại thiếu, nhưng câu 30 có hỏi về Precision*

| Metric | Công thức | Ý nghĩa | Khi nào dùng |
|--------|-----------|---------|--------------|
| **Precision** | $\frac{TP}{TP + FP}$ | Tỷ lệ dự đoán đúng trong số các dự đoán dương | Khi chi phí false positive cao |
| **Recall (Sensitivity)** | $\frac{TP}{TP + FN}$ | Tỷ lệ phát hiện đúng trong số các ground truth | Khi không được bỏ sót |
| **F1-Score** | $\frac{2 \times Precision \times Recall}{Precision + Recall}$ | Cân bằng Precision và Recall | Khi cần đánh giá tổng thể |
| **IoU (Intersection over Union)** | $\frac{Area(Intersection)}{Area(Union)}$ | Độ trùng khớp giữa box dự đoán và ground truth | Đánh giá detection/segmentation |
| **Accuracy** | $\frac{TP + TN}{TP + TN + FP + FN}$ | Tỷ lệ dự đoán đúng tổng thể | Khi dữ liệu cân bằng |

**Ghi nhớ:** Precision = "Trong số những gì tôi nói đúng, có bao nhiêu phần trăm thực sự đúng?"; Recall = "Trong số những gì thực sự đúng, tôi tìm được bao nhiêu phần trăm?"

### 2. **So sánh chi tiết các bộ lọc gradient (Sobel, Prewitt, Roberts)**

| Bộ lọc | Kernel X | Kernel Y | Đặc điểm | Khi nào dùng |
|--------|---------|----------|----------|--------------|
| **Roberts** | $\begin{bmatrix}1&0\\0&-1\end{bmatrix}$ | $\begin{bmatrix}0&1\\-1&0\end{bmatrix}$ | Nhỏ nhất (2×2), nhanh, nhạy nhiễu | Ảnh ít nhiễu, cần tốc độ |
| **Prewitt** | $\begin{bmatrix}-1&0&1\\-1&0&1\\-1&0&1\end{bmatrix}$ | Chuyển vị | Cân bằng, ít nhạy nhiễu hơn Roberts | Ảnh có nhiễu vừa |
| **Sobel** | $\begin{bmatrix}-1&0&1\\-2&0&2\\-1&0&1\end{bmatrix}$ | Chuyển vị | Trọng số tâm cao hơn → ít nhạy nhiễu nhất | **Nên dùng** khi có nhiễu |

**Tip:** Sobel có hệ số 2 ở hàng/cột giữa → nhấn mạnh vùng trung tâm → ổn định hơn.

### 3. **Công thức chi tiết cần thuộc**

#### A. Harris Corner Response
$$R = \det(M) - k \cdot [\text{trace}(M)]^2$$
Trong đó:
- $M = \sum_{(x,y) \in W} w(x,y) \begin{bmatrix}I_x^2 & I_x I_y \\ I_x I_y & I_y^2\end{bmatrix}$ (ma trận cấu trúc)
- $k \approx 0.04-0.06$ (hệ số thực nghiệm)
- $R > threshold$ → góc (corner)

#### B. Công thức EM (Expectation-Maximization) cho GMM
- **E-step:** Tính responsibility (xác suất điểm thuộc cụm $k$):
  $$\gamma_{nk} = \frac{\pi_k \mathcal{N}(x_n|\mu_k, \Sigma_k)}{\sum_{j=1}^K \pi_j \mathcal{N}(x_n|\mu_j, \Sigma_j)}$$
- **M-step:** Cập nhật tham số:
  $$\mu_k = \frac{\sum_{n=1}^N \gamma_{nk} x_n}{\sum_{n=1}^N \gamma_{nk}}$$
  $$\Sigma_k = \frac{\sum_{n=1}^N \gamma_{nk}(x_n - \mu_k)(x_n - \mu_k)^T}{\sum_{n=1}^N \gamma_{nk}}$$
  $$\pi_k = \frac{1}{N}\sum_{n=1}^N \gamma_{nk}$$

#### C. Công thức K-means objective (SSE)
$$SSE = \sum_{k=1}^K \sum_{x_i \in C_k} ||x_i - \mu_k||^2$$
- Cập nhật centroid: $\mu_k = \frac{1}{|C_k|}\sum_{x_i \in C_k} x_i$

### 4. **Các bước thuật toán cần nhớ thứ tự**

#### A. Canny Edge Detection (4 bước)
1. **Gaussian smoothing** → giảm nhiễu
2. **Tính gradient** (Sobel) → $|G| = \sqrt{G_x^2 + G_y^2}$, $\theta = \arctan(G_y/G_x)$
3. **Non-maxima suppression** → chỉ giữ cực đại theo hướng gradient
4. **Hysteresis thresholding** → 2 ngưỡng ($T_{high}$, $T_{low}$) để kết nối cạnh

#### B. RANSAC (5 bước)
1. Chọn ngẫu nhiên **n điểm tối thiểu** (ví dụ: 2 điểm cho đường thẳng)
2. **Ước lượng mô hình** từ n điểm
3. **Đếm inliers** (điểm phù hợp với mô hình trong ngưỡng $\epsilon$)
4. **Lặp lại** N lần (hoặc đến khi đủ inliers)
5. **Chọn mô hình tốt nhất** (nhiều inliers nhất)

#### C. K-means (3 bước lặp)
1. **Gán điểm** vào cụm gần nhất: $c_i = \arg\min_k ||x_i - \mu_k||^2$
2. **Cập nhật centroid**: $\mu_k = \frac{1}{|C_k|}\sum_{x_i \in C_k} x_i$
3. **Kiểm tra hội tụ** (centroid không đổi hoặc SSE không giảm)

### 5. **Bảng so sánh các không gian màu**

| Không gian | Thành phần | Ưu điểm | Nhược điểm | Khi dùng |
|------------|------------|---------|------------|----------|
| **RGB** | R, G, B [0-255] | Phổ biến, dễ xử lý | Phụ thuộc thiết bị, không tuyến tính | Hiển thị, capture |
| **HSV** | H [0-360], S [0-1], V [0-1] | H ổn định với ánh sáng | V nhạy cảm ánh sáng | Phân vùng màu, nhận dạng |
| **Lab** | L [0-100], a* [-128,127], b* [-128,127] | Độc lập thiết bị, tuyến tính, AB ổn định | Phức tạp hơn | So khớp màu, phân tích |
| **YUV/YCbCr** | Y (luminance), U/Cb, V/Cr | Tách độ sáng và màu | Ít dùng trong CV | Video, nén |

**Tip thi:** Khi đề hỏi "không gian màu nào ổn định nhất với thay đổi ánh sáng?" → **Lab** (kênh AB) hoặc **HSV** (kênh H).

---

## 🎯 II. CHIẾN LƯỢC ÔN TẬP

### **Giai đoạn 1: Nắm vững lý thuyết (3-5 ngày)**
1. **Đọc kỹ file `tomtat-noidung.md`** theo thứ tự:
   - Ngày 1: Phần I, II (Giới thiệu, Thu nhận ảnh)
   - Ngày 2: Phần III (Low-level: Point processing, Filtering, Morphology)
   - Ngày 3: Phần IV (Middle-level: Edge, Hough, Features)
   - Ngày 4: Phần V (High-level: Classification, Detection, Segmentation, DL)
   - Ngày 5: Phần VI (Pipeline, Flashcard) + bổ sung các điểm trên

2. **Ghi chú lại các công thức** vào sổ riêng:
   - Công thức biến đổi (Log, Gamma, Histogram equalization)
   - Công thức kernel (Sobel, Laplacian, Gaussian)
   - Công thức metric (Precision, Recall, F1, IoU)
   - Công thức thuật toán (Harris, EM, K-means)

### **Giai đoạn 2: Làm bài tập trắc nghiệm (2-3 ngày)**
1. **Làm file `cauhoi.md`** 2-3 lần:
   - Lần 1: Làm không xem đáp án, ghi lại câu sai
   - Lần 2: Làm lại chỉ các câu sai
   - Lần 3: Làm toàn bộ để kiểm tra

2. **Tạo câu hỏi tự kiểm tra**:
   - Viết lại định nghĩa các khái niệm
   - So sánh các phương pháp (ví dụ: Sobel vs Prewitt)
   - Giải thích các bước thuật toán (Canny, RANSAC)

### **Giai đoạn 3: Ôn tập tổng hợp (1-2 ngày)**
1. **Tạo mindmap** theo 3 cấp độ:
   ```
   Low-level → Middle-level → High-level
   ```
   Mỗi cấp độ ghi các phương pháp chính

2. **Làm flashcard** (giấy hoặc app):
   - Mặt trước: Khái niệm/Công thức
   - Mặt sau: Định nghĩa/Giải thích
   - Ví dụ: "Canny 3 tiêu chí?" → "Good detection, Good localization, Single response"

3. **Ôn theo pipeline** (Phần VI trong tài liệu):
   - Tiền xử lý → Lọc → Phát hiện biên → Phân cụm/Segmentation → Nhận dạng

---

## 📊 III. BẢNG SO SÁNH QUAN TRỌNG (CẦN THUỘC)

### **Bảng 1: So sánh các bộ lọc làm sắc nét (Sharpening)**

| Bộ lọc | Loại | Tổng hệ số | Mục đích | Nhạy nhiễu |
|--------|------|------------|----------|------------|
| **Sobel** | Đạo hàm bậc 1 | 0 | Tìm biên (cực trị đạo hàm bậc 1) | Trung bình |
| **Laplacian** | Đạo hàm bậc 2 | 0 | Tìm biên (zero-crossing) | **Rất cao** |
| **LoG** | Laplacian-of-Gaussian | 0 | Tìm biên ổn định (Gaussian trước) | Thấp |
| **Unsharp Masking** | High-pass + Original | 1 | Tăng cường biên, giữ ảnh gốc | Trung bình |

### **Bảng 2: So sánh các phương pháp phân cụm**

| Thuật toán | Cần số cụm k? | Xử lý outlier | Tốc độ | Hình dạng cụm | Ghi chú |
|------------|---------------|---------------|--------|--------------|---------|
| **K-means** | ✅ Có | ❌ Không | Nhanh | Lồi (spherical) | SSE giảm dần |
| **K-medoids** | ✅ Có | ✅ Bền | Chậm | Lồi | Dùng điểm thật làm centroid |
| **GMM-EM** | ✅ Có | ❌ Không | Trung bình | Elip (ellipsoidal) | Trả xác suất |
| **Mean Shift** | ❌ Không | ✅ Bền | Chậm | Tùy kernel | Phát hiện số cụm tự nhiên |
| **Agglomerative** | ❌ Không | ❌ Không | Chậm ($O(n^2)$) | Tùy linkage | Cho dendrogram |

### **Bảng 3: So sánh các phương pháp segmentation**

| Phương pháp | Cần seed? | Cần histogram 2 đỉnh? | Xử lý over-segmentation | Khi dùng |
|-------------|-----------|----------------------|------------------------|----------|
| **Otsu Thresholding** | ❌ | ✅ Có | ❌ Không | Histogram rõ 2 đỉnh |
| **Region Growing** | ✅ Có | ❌ Không | ❌ Không | Vùng đồng nhất rõ |
| **Watershed** | ✅ (Marker) | ❌ Không | ✅ Cần marker | Đối tượng chồng lấn |
| **Graph-based** | ❌ | ❌ Không | ✅ Tốt | Cần cân bằng kết nối/tách |

### **Bảng 4: So sánh các detector (phát hiện đối tượng)**

| Mô hình | Loại | Tốc độ | Độ chính xác | Đặc điểm nổi bật |
|---------|------|--------|--------------|------------------|
| **Viola-Jones** | Traditional | Rất nhanh | Trung bình | Integral Image + Cascade |
| **HOG + SVM** | Traditional | Nhanh | Tốt | Phát hiện người |
| **R-CNN** | Two-stage | Chậm | Tốt | Selective Search |
| **Fast R-CNN** | Two-stage | Trung bình | Tốt | RoI Pooling |
| **Faster R-CNN** | Two-stage | Nhanh | Rất tốt | RPN thay Selective Search |
| **YOLO/SSD** | One-stage | Rất nhanh | Tốt | Anchor-based |
| **RetinaNet** | One-stage | Nhanh | Rất tốt | Focal Loss |

---

## ✅ IV. CHECKLIST ÔN THI (1 ngày trước thi)

### **Kiến thức cơ bản**
- [ ] Định nghĩa 3 cấp độ Vision (Low/Middle/High)
- [ ] Biểu diễn ảnh số (nhị phân: 1 bit, grayscale: 8 bits, RGB: 24 bits)
- [ ] Các không gian màu (RGB, HSV, Lab) và khi nào dùng
- [ ] Tế bào thụ cảm quang (Rods vs Cones)

### **Xử lý ảnh mức thấp**
- [ ] Các phương pháp tăng cường tương phản (Histogram equalization, Log, Gamma)
- [ ] Điều kiện kernel: tổng = 1 (low-pass), = 0 (high-pass)
- [ ] So sánh Sobel, Prewitt, Roberts
- [ ] Median filter: phi tuyến, bảo toàn cạnh, khử salt-pepper
- [ ] Morphology: Opening = Erode→Dilate, Closing = Dilate→Erode
- [ ] Tần số cao/thấp tương ứng với gì

### **Xử lý ảnh mức giữa**
- [ ] Biên: cực trị đạo hàm bậc 1 hoặc zero-crossing đạo hàm bậc 2
- [ ] Canny 4 bước + 3 tiêu chí
- [ ] Hough Transform: cần phương trình tham số xác định
- [ ] RANSAC: chọn ngẫu nhiên → tính mô hình → đếm inliers
- [ ] Harris: gradient thay đổi mạnh ≥2 hướng
- [ ] SIFT: DoG detector, 128-D descriptor, bất biến scale/rotation/illumination
- [ ] BoW: K-means tạo dictionary

### **Xử lý ảnh mức cao**
- [ ] Phân loại: kNN, Naïve Bayes, SVM, AdaBoost
- [ ] Viola-Jones: Integral Image + AdaBoost + Cascade
- [ ] Two-stage vs One-stage detectors
- [ ] Semantic vs Instance Segmentation
- [ ] Các metric: Precision, Recall, F1, IoU

### **Phân cụm & Segmentation**
- [ ] K-means: cần k, cập nhật centroid
- [ ] EM cho GMM: E-step (responsibility), M-step (cập nhật tham số)
- [ ] Mean Shift: không cần k, phát hiện số cụm tự nhiên
- [ ] Otsu: cần histogram 2 đỉnh
- [ ] Watershed: cần marker để tránh over-segmentation

### **Công thức cần thuộc**
- [ ] Log: $s = c \times \log(1 + r)$
- [ ] Gamma: $s = c \cdot r^\gamma$
- [ ] Harris: $R = \det(M) - k \cdot [\text{trace}(M)]^2$
- [ ] Precision: $\frac{TP}{TP + FP}$
- [ ] Recall: $\frac{TP}{TP + FN}$

---

## 🎓 V. MẸO LÀM BÀI THI TRẮC NGHIỆM

1. **Đọc kỹ câu hỏi**, gạch chân từ khóa:
   - "Không" → loại trừ
   - "Nhất" → chỉ có 1 đáp án đúng
   - "Chủ yếu" → có thể có nhiều nhưng chọn cái quan trọng nhất

2. **Loại trừ đáp án sai** trước:
   - Đáp án quá tuyệt đối thường sai
   - Đáp án có từ "chỉ", "luôn luôn" cần kiểm tra kỹ

3. **Nhớ các mẹo nhanh**:
   - Tổng kernel = 0 → high-pass; = 1 → low-pass
   - Ideal filter → ringing; Gaussian → không ringing
   - Median → bảo toàn cạnh; Mean → làm mờ cạnh
   - Opening → loại đối tượng nhỏ; Closing → lấp lỗ

4. **Câu hỏi về "khi nào dùng"**:
   - Nhiễu salt-pepper → Median
   - Histogram 2 đỉnh → Otsu
   - Đối tượng chồng lấn → Watershed
   - Nhiều outlier → K-medoids/Mean Shift

5. **Câu hỏi về "bước thuật toán"**:
   - Canny: Gaussian → Gradient → Non-max → Hysteresis
   - RANSAC: Chọn ngẫu nhiên → Tính mô hình → Đếm inliers → Lặp
   - K-means: Gán → Cập nhật centroid → Kiểm tra hội tụ

---

## 📝 VI. TÀI LIỆU THAM KHẢO THÊM (NẾU CẦN)

1. **File `tomtat-noidung.md`** - Tài liệu chính
2. **File `cauhoi.md`** - 30 câu hỏi mẫu
3. **File này** - Đề xuất ôn tập

**Lưu ý:** Chỉ học theo kiến thức trong `tomtat-noidung.md`, không thêm kiến thức từ nguồn khác để tránh nhầm lẫn.

---

**Chúc bạn ôn thi tốt! 🎯**

