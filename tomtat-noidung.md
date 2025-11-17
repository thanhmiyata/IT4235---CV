Đây là file tổng hợp chi tiết toàn bộ nội dung môn học Thị giác Máy tính, bao gồm các định nghĩa, thuật toán, cấp độ xử lý, không gian màu và các phương pháp chính, được trích xuất và tổng hợp từ các tài liệu đã cung cấp.

***

# TỔNG HỢP CHI TIẾT NỘI DUNG MÔN HỌC THỊ GIÁC MÁY TÍNH

## I. GIỚI THIỆU TỔNG QUAN

### 1. Định nghĩa và Mục đích

*   **Thị giác máy tính (Computer Vision - CV):** Là lĩnh vực khoa học liên ngành cho phép máy tính có thể **hiểu được nội dung bức ảnh/video ở mức cao**.
*   **Mục đích:** Là cầu nối giữa **giá trị của các điểm ảnh (pixel)** và **"ngữ nghĩa"** của bức ảnh.
*   **Thông tin trích xuất từ ảnh:** Thông tin 3D (ảnh như thiết bị đo lường) và Thông tin ngữ nghĩa (ảnh là nguồn chứa ngữ nghĩa).

### 2. Các Cấp độ Xử lý (Levels of Vision)

Thị giác máy tính được chia thành ba cấp độ xử lý chính:

| Cấp độ | Tên (Tiếng Anh) | Đặc điểm chính | Đầu vào/Đầu ra | Ví dụ/Nhiệm vụ |
| :--- | :--- | :--- | :--- | :--- |
| **Mức thấp** | **Low-level Vision** (Xử lý ảnh) | Tạo ảnh, thu nhận và **xử lý dữ liệu ảnh 2D** (tiền xử lý: tăng cường độ tương phản, lọc nhiễu, biến đổi ảnh). | Đầu vào: ảnh, Đầu ra: ảnh. | Khử nhiễu, chỉnh mức xám, nén ảnh. |
| **Mức giữa** | **Middle-level Vision** | Trích chọn các đặc trưng phức tạp, so khớp ảnh, phân vùng ảnh. | | Cạnh, góc, đường, kết cấu, hình dáng. |
| **Mức cao** | **High-level Vision** | Xử lý mức ngữ nghĩa cao. | Đầu vào: ảnh, Đầu ra: thông tin ngữ nghĩa, ra quyết định. | Nhận dạng object (phân loại), định danh, phát hiện, phân tích chuyển động, tái tạo cảnh, dựng 3D. |

## II. THU NHẬN ẢNH VÀ BIỂU DIỄN ẢNH SỐ

### 1. Cơ chế Thị giác Người và Máy ảnh

*   **Tế bào thụ cảm quang (Photoreceptor cells):** Nằm trên võng mạc.
    *   **Rods (hình que):** Độ nhạy cao, hoạt động trong ánh sáng yếu, rất ít nhạy cảm với màu sắc.
    *   **Cones (hình nón):** Ít nhạy cảm, hoạt động trong ánh sáng mạnh, cảm thụ màu sắc. Có 3 loại: S (~440nm), M (~530nm), L (~560nm).
*   **Mô hình camera:** **Mô hình pin-hole camera** (camera không ống kính, độ mở lỗ thủng quyết định độ mờ). Camera thực tế sử dụng ống kính quang học.
*   **Độ sâu vùng quan sát (Depth of field - DOF):** Tỷ lệ nghịch với kích thước độ mở (aperture size).
*   **Số hóa (Digitization):** Quá trình chuyển tín hiệu 2D liên tục thành ảnh số, bao gồm **Lấy mẫu (Sampling)** đều trên không gian 2D và **Lượng tử hóa (Quantization)** (làm tròn đến số nguyên gần nhất).

### 2. Biểu diễn Ảnh Số

Ảnh $I$ kích thước $N \times M$ là một ma trận.

| Loại ảnh | Biểu diễn giá trị $I(x,y)$ | Bit/Pixel |
| :--- | :--- | :--- |
| **Ảnh nhị phân** | $I(x,y) \in \{0, 1\}$ | 1 bit. |
| **Ảnh đa mức xám** | $I(x,y) \in [0..255]$ (mức xám, cường độ sáng) | 8 bits (1 byte). |
| **Ảnh màu (RGB)** | $I_R, I_G, I_B \in [0..255]$ | 24 bits (3 bytes). |

### 3. Không gian màu (Color Spaces)

Là không gian gồm các thành phần màu (primary color) được kết hợp để biểu diễn màu sắc.

*   **RGB (Red – Green – Blue):**
    *   Phổ biến, dùng trong thiết bị hiển thị.
    *   Hệ thống phối màu **cộng**.
    *   **Không** độc lập với thiết bị và thường **không** tuyến tính với cảm nhận màu của mắt người.
*   **CMY (Cyan-Magenta-Yellow):**
    *   Thường dùng trong in ấn, photo.
    *   Hệ thống không gian màu **trừ**.
*   **HSV (Hue – Saturation-Value/Lightness):**
    *   Phù hợp với cảm nhận màu của thị giác người, hay dùng cho phân vùng/nhận dạng.
    *   Thành phần: **H** (sắc tố, tông màu), **S** (độ bão hòa, sắc độ), **V** (cường độ sáng/Value).
    *   **V** nhạy cảm với điều kiện chiếu sáng, nhưng **H** (Hue) có giá trị tập trung (compact) và ổn định hơn khi điều kiện chiếu sáng thay đổi.
*   **CIE Luv/Lab (L*a*b*):**
    *   Được nghiên cứu dựa trên thị giác người, **độc lập thiết bị** và **tuyến tính** với cảm nhận màu của mắt người.
    *   Thành phần: **L** (độ sáng), **a*** (green đến red), **b*** (blue đến yellow).
    *   Có mức độ tập trung trên kênh AB tốt hơn HSV và RGB khi điều kiện chiếu sáng thay đổi.
*   **YUV/YCbCr:** Y (Luminance - Độ sáng), U/Cb và V/Cr là thành phần sắc độ (chrominance).

## III. XỬ LÝ ẢNH MỨC THẤP (LOW-LEVEL VISION)

### 1. Phép toán ở mức điểm ảnh (Point Processing)

Giá trị mới của điểm ảnh chỉ phụ thuộc vào giá trị hiện tại của điểm ảnh đó, không phụ thuộc vào các điểm lân cận.

#### A. Tăng cường Độ tương phản (Contrast Enhancement)

Mục tiêu là thay đổi giá trị điểm ảnh để có độ tương phản cao hơn.

| Phương pháp | Công thức/Ý tưởng | Đặc điểm |
| :--- | :--- | :--- |
| **Kéo giãn tuyến tính** (Linear Stretching) | Biến đổi tuyến tính dải động ảnh. | Nếu kéo giãn có bão hòa (saturation), có thể loại bỏ các giá trị nhiễu ở hai đầu dải động. |
| **Tuyến tính theo đoạn** (Piecewise-Linear) | Tăng/giảm độ tương phản ở các khoảng mức xám khác nhau. | Trường hợp đặc biệt: **Lấy ngưỡng (Thresholding)** tạo ra ảnh nhị phân (nếu $s_1=0, s_2=L-1$). |
| **Cân bằng Histogram** (Histogram Equalization) | Thay đổi ảnh để histogram hướng tới phân bố đều. | Là phương pháp không tham số. Nên thực hiện trên kênh độ sáng (L hay V) của không gian màu Lab/HSV cho ảnh màu. |
| **Biến đổi Log** | $s = c \times \log(1 + r)$. | Làm **sáng hơn** các điểm có mức xám thấp, nén các giá trị mức xám cao. |
| **Biến đổi Luật Lũy thừa** (Power-Law / Gamma) | $s = c \cdot r^\gamma$. | Dùng để hiệu chỉnh gamma ($\gamma < 1$: mở rộng vùng tối; $\gamma > 1$: nén vùng tối). |

#### B. Phép toán Logic và Số học

*   **Phép cộng ảnh:** Dùng để giảm nhiễu (lấy trung bình) hoặc tăng độ sáng.
*   **Phép trừ ảnh:** Dùng để phát hiện sự khác biệt hoặc chuyển động.
*   **Phép nhân ảnh:** Dùng để tăng độ tương phản hoặc độ sáng.
*   **Phép toán Logic (AND, OR):** Thường dùng trên ảnh nhị phân.

### 2. Lọc Ảnh (Image Filtering)

Tính giá trị mới của điểm ảnh dựa trên một hàm theo các điểm trong lân cận của nó.

*   **Nhân chập (Convolution):** Là phép lọc tuyến tính (I' = I \* K), tổng có trọng số của các điểm ảnh lân cận.
    *   **Điều kiện tránh thay đổi độ sáng:** Tổng các hệ số của mặt nạ (kernel) phải bằng 1.
*   **Tương quan không gian (Spatial Correlation):** Dùng để tìm mẫu (template matching). Nếu mặt nạ đối xứng, Correlation và Convolution là một.

#### A. Bộ lọc trong miền không gian (Spatial Domain Filters)

| Loại lọc | Bộ lọc (Kernel) | Mục đích | Đặc điểm |
| :--- | :--- | :--- | :--- |
| **Làm trơn/Thông thấp** (Smoothing/Low-pass) | **Trung bình** (Mean/Box) | Lọc nhiễu, làm trơn. | Thay giá trị bởi giá trị trung bình của lân cận. |
| | **Gauss** (Gaussian) | Lọc nhiễu hiệu quả hơn trung bình. | Có tính phân tách được (2D = 1D theo x $\times$ 1D theo y). |
| **Làm sắc nét** (Sharpening/High-pass) | **Đạo hàm bậc 1:** Robert, Prewitt, **Sobel**. | Tìm biên, nơi cường độ sáng thay đổi nhanh (cực trị đạo hàm bậc 1). | Sobel ít nhạy cảm với nhiễu hơn Robert/Prewitt. |
| | **Đạo hàm bậc 2:** **Laplacian**. | Tìm biên, nơi đạo hàm bậc 2 đi qua 0 (zero-crossing). | Rất nhạy với nhiễu. |
| **Phi tuyến** | **Trung vị** (Median) | Loại bỏ nhiễu xung (salt & pepper). | **Bảo toàn cạnh** (edge preserving). |
| | **Max/Min** | | Thay giá trị bằng max/min trong cửa sổ. |

**Các kernel thường gặp & mẹo nhớ nhanh:**

*   **Mean 3×3:** $\frac{1}{9}\begin{bmatrix}1&1&1\\1&1&1\\1&1&1\end{bmatrix}$ → tổng hệ số = 1 nên không đổi độ sáng.
*   **Gaussian 5×5 (σ≈1):** $\frac{1}{273}\begin{bmatrix}1&4&7&4&1\\4&16&26&16&4\\7&26&41&26&7\\4&16&26&16&4\\1&4&7&4&1\end{bmatrix}$, tách được thành hai kernel 1D.
*   **Sobel X:** $\begin{bmatrix}-1&0&1\\-2&0&2\\-1&0&1\end{bmatrix}$ (Sobel Y là chuyển vị); bền với nhiễu hơn Prewitt/Roberts.
*   **Laplacian 4-neighbor:** $\begin{bmatrix}0&-1&0\\-1&4&-1\\0&-1&0\end{bmatrix}$; bản 8-neighbor thay 4 bằng 8 và thêm -1 ở góc.
*   **LoG (Laplacian-of-Gaussian):** Làm trơn bằng Gaussian trước khi đạo hàm bậc 2 → zero-crossing ổn định.

**Gợi ý ôn thi:** Tổng hệ số kernel = 0 → high-pass; = 1 → low-pass. σ lớn → làm mờ mạnh, loại bỏ chi tiết; σ nhỏ → giữ cạnh tốt nhưng hết nhiễu kém.

#### B. Lọc trong miền tần số (Frequency Domain Filters)

*   **Biến đổi Fourier (Fourier Transform):** Công cụ cơ bản để chuyển ảnh từ miền không gian sang miền tần số.
    *   **Tần số thấp (Low frequencies):** Thay đổi chậm, tương ứng với vùng đồng nhất/mờ. Hầu hết năng lượng ảnh tập trung ở tần số thấp.
    *   **Tần số cao (High frequencies):** Thay đổi nhanh/đột ngột (cạnh, nhiễu, đường viền).
*   **Lọc tần số:**
    *   **Bộ lọc Thông thấp (Low-pass filter):** Dùng để làm trơn ảnh (smoothing). Ví dụ: Ideal low-pass filter (gây hiệu ứng ringing) và Gaussian lowpass filter (làm mờ mềm mại, không ringing).
    *   **Bộ lọc Thông cao (High-pass filter):** Dùng để làm sắc nét ảnh (sharpening), giữ lại các thay đổi đột ngột (cạnh).
    *   **Bộ lọc Thông dải (Band-pass filter):** Giữ lại một dải tần số nhất định.

**Công thức DFT 2D cần thuộc:** $F(u,v)=\sum_{x=0}^{M-1}\sum_{y=0}^{N-1}f(x,y)e^{-j2\pi(\frac{ux}{M}+\frac{vy}{N})}$; biến đổi ngược lấy lại $f(x,y)$. Tính chất: dịch trong miền không gian ↔ pha tuyến tính trong miền tần số, ảnh thực cho phổ đối xứng quanh tâm.

| Bộ lọc | Đặc điểm | Ứng dụng | Nhược điểm |
| :--- | :--- | :--- | :--- |
| **Ideal LPF/HPF** | Cắt “cứng” tại $D_0$. | Nhấn mạnh tần số cụ thể. | Gây ringing mạnh (do sinc). |
| **Butterworth** | Độ dốc điều chỉnh bởi bậc $n$. | Linh hoạt giữa Ideal và Gaussian. | Vẫn có ringing nhẹ. |
| **Gaussian** | Đáp ứng mượt, không ringing. | Làm trơn/sắc nét tự nhiên. | Không loại bỏ hoàn toàn dải ngoài. |

**Tip thi:** Nhắc tới ringing → Ideal/Butterworth; cần đáp ứng mượt → Gaussian. Để tăng cường biên, dùng High-pass với hệ số tổng = 0 hoặc cộng kết quả vào ảnh gốc (unsharp masking).

### 3. Các Phép toán Hình thái học (Morphological Operations)

Thường áp dụng trên ảnh nhị phân.

*   **Phép Giãn (Dilation, $A \oplus S$):** Mở rộng thành phần liên thông, lấp lỗ. Hoạt động như Max filter.
*   **Phép Co (Erosion, $A \ominus S$):** Thu hẹp thành phần liên thông, loại bỏ nhiễu/cầu nối nhỏ. Hoạt động như Min filter.
*   **Phép Mở (Opening):** **Erode, then dilate**. Loại bỏ các đối tượng nhỏ, giữ hình dạng gốc.
*   **Phép Đóng (Closing):** **Dilate, then erode**. Lấp đầy các lỗ nhỏ, giữ hình dạng gốc.

**Structuring element (SE):** chọn hình (vuông, đĩa, chữ thập) quyết định hướng ưu tiên. SE lớn → hiệu ứng mạnh hơn nhưng dễ phá chi tiết.

**Phép morphology nâng cao:**

*   **Top-hat:** $A - (A \circ S)$, làm nổi bật chi tiết sáng nhỏ hơn SE.
*   **Bottom-hat:** $(A \bullet S) - A$, làm nổi bật chi tiết tối.
*   **Skeletonization:** Lặp lại erode có điều kiện để giữ xương mảnh của đối tượng, hữu ích trong OCR và phân tích đường trung tâm.

**Tip thi:** Dilate để nối khe hở, Erode để tách đối tượng dính nhau, Opening = “Erode trước” giúp khử nhiễu-sáng; Closing = “Dilate trước” giúp lấp lỗ.

### 4. Các biến đổi quan trọng trong xử lý ảnh

*   **DCT (Discrete Cosine Transform):** Gom năng lượng vào hệ số thấp, dùng trong JPEG/nén, ít tạo ringing hơn DFT.
*   **Wavelet Transform:** Phân tích đa tỉ lệ (multi-resolution); ví dụ Haar, Daubechies. Ứng dụng: khử nhiễu, nén, phát hiện biên.
*   **Radon Transform:** Tính tích phân cường độ dọc theo các đường thẳng → cơ sở cho Hough và tái tạo CT.
*   **Hadamard/KLT (PCA):** Phân rã thành các trục eigen tối đa hóa phương sai, dùng giảm chiều (Eigenfaces).

Nhớ: Wavelet cung cấp thông tin cả miền thời gian + tần số, DCT chỉ miền tần số; Radon biến đường trong ảnh thành điểm trong không gian tham số $(\rho,\theta)$.

## IV. XỬ LÝ ẢNH MỨC GIỮA (MIDDLE-LEVEL VISION)

### 1. Phát hiện Biên (Edge Detection)

Biên (Edge) là nơi có sự thay đổi cường độ sáng trong ảnh, thường xảy ra ở ranh giới giữa các vùng khác nhau.

*   **Đặc điểm toán học:** Biên là vị trí đạt **cực trị trên đạo hàm bậc 1** hoặc đi qua không (**zero-crossing**) ở đạo hàm bậc 2.
*   **Bộ phát hiện Canny (Canny Detector):** Được coi là "tối ưu" theo ba tiêu chí:
    1.  **Good detection:** Tối thiểu "nhận nhầm" và "bỏ sót".
    2.  **Good localization:** Gần biên đúng nhất.
    3.  **Single response:** Độ dày biên = 1 (tối thiểu số lượng cực đại địa phương).
*   **Các bước của Canny:**
    1.  Lọc nhiễu bằng bộ lọc **Gaussian**.
    2.  Tính **độ lớn gradient** ($|G| = |G_x| + |G_y|$) và **hướng gradient** ($\theta$) (thường dùng Sobel).
    3.  **Loại bỏ các điểm không phải cực trị** (Non-maxima Suppression).
    4.  **Lấy ngưỡng Hysteresis** (sử dụng 2 ngưỡng cao $S_h$ và thấp $S_b$) để kết nối và giữ lại các cạnh yếu liên kết với cạnh mạnh.

### 2. Phát hiện Đường thẳng và Mô hình

*   **Biến đổi Hough (Hough Transform - HT):**
    *   Dùng để phát hiện các đường thẳng, đường tròn và các cấu trúc khác **nếu phương trình tham số là xác định**.
    *   Ý tưởng chính: Sử dụng kỹ thuật **bỏ phiếu** (voting) trong không gian tham số $(\rho, \theta)$. Các đường (từ các điểm biên) giao nhau tại một điểm trong không gian tham số tương ứng với một đường thẳng trong không gian ảnh.
*   **RANSAC (RANdom SAmple Consensus):**
    *   Phương pháp lặp để **ước lượng tham số mô hình** từ dữ liệu chứa nhiều điểm ngoại lai (outliers).
    *   Quy trình: Chọn ngẫu nhiên một tập hợp điểm nhỏ (**seed group**), tính mô hình, tìm các điểm phù hợp với mô hình (**inliers**), lặp lại và giữ lại mô hình có số inliers lớn nhất.

### 3. Trích chọn Đặc trưng (Feature Extraction)

#### A. Đặc trưng Toàn cục (Global Features)

Mô tả toàn bộ ảnh như 1 đối tượng.

*   **Histogram:** Mô tả màu sắc/cường độ sáng. Đơn giản, bất biến với quay, dịch, zoom, nhưng không tính đến phân bố không gian.
*   **GLCM (Grey Level Co-occurence Matrices):** Dùng để mô tả **kết cấu (texture)**, xác định mức lặp của cặp mức xám theo hướng và khoảng cách. Các đặc trưng **Haralick** (như energy, contrast, entropy) được tính từ GLCM.
*   **Moment bất biến của Hu (Hu's moments):** Bất biến với **tịnh tiến (translation), tỷ lệ (scale), và phép quay (rotation)**.
*   **PHOG (Pyramid Histogram of Oriented Gradients)**.

#### B. Đặc trưng Cục bộ (Local Features)

Mô tả từng vùng nhỏ trong ảnh (keypoint). Yêu cầu: lặp lại (repeatable), bất biến với scale/rotation, và có tính phân biệt (distinctiveness).

*   **Harris Corner Detector:**
    *   Ý tưởng: Tìm vị trí mà gradient có sự thay đổi mạnh theo **ít nhất 2 hướng** trong vùng xung quanh.
    *   Bất biến với tịnh tiến và quay, nhưng **không bất biến với tỷ lệ** (scale).
    *   Đánh giá góc bằng $\theta = \det(M) - \alpha \cdot \text{trace}(M)^2$.
*   **Đạt được tính Bất biến với Tỷ lệ (Scale Invariance):**
    *   Các bộ phát hiện hiện đại tìm kiếm cực trị địa phương trên miền **không gian-scale (space – scale)**.
    *   Sử dụng **Laplacian-of-Gaussian (LoG)** hoặc xấp xỉ của nó là **Difference-of-Gaussian (DoG)** để tìm **scale đặc trưng (characteristic scale)**.
*   **SIFT (Scale-Invariant Feature Transform):**
    *   **Detector:** Dựa trên cực trị của DoG trên miền không gian-scale.
    *   **Descriptor:** Vector 128 chiều, được chuẩn hóa theo hướng chủ đạo (dominant orientation).
    *   Đạt được tính bất biến với sự thay đổi độ sáng nhờ sử dụng **đạo hàm bậc 1** và **chuẩn hóa vector** (độ lớn vector = 1.0).

### 4. So khớp Đặc trưng (Feature Matching)

*   **So khớp:** Tìm kiếm lân cận gần nhất (Nearest Neighbor Search) giữa các đặc trưng.
*   **Tỷ lệ khoảng cách (Nearest neighbor distance ratio):** So sánh khoảng cách tới đặc trưng gần nhất ($f_2$) và đặc trưng gần thứ hai ($f'_2$) để lọc ra các cặp ghép kém tin cậy (chỉ giữ lại cặp có ratio nhỏ).
*   **Kiểm tra chéo (Cross check test):** Ghép cặp (fa, fb) nếu fb là điểm ghép tốt nhất cho fa, VÀ ngược lại.
*   **Mô hình Túi từ (Bag-of-Words - BoW):** Biểu diễn ảnh thành vector tần suất xuất hiện của các **từ thị giác (visual words)**.
    *   **Dictionary Learning:** Học từ điển thị giác bằng thuật toán phân cụm **K-means** trên các đặc trưng cục bộ.
    *   Sử dụng **TF-IDF** để gán trọng số cho các từ.

## V. XỬ LÝ ẢNH MỨC CAO VÀ HỌC SÂU (HIGH-LEVEL VISION & DL)

### 1. Phân loại Ảnh (Image Classification)

Gán một nhãn cho toàn bộ ảnh.

| Thuật toán | Đặc điểm |
| :--- | :--- |
| **K-Nearest Neighbors (kNN)** | Phương pháp phi tham số. Phân loại một điểm mới dựa trên **bỏ phiếu đa số** của k điểm lân cận gần nhất. |
| **Naïve Bayes** | Bộ phân loại xác suất dựa trên định lý Bayes, giả định các đặc trưng độc lập có điều kiện. |
| **Support Vector Machines (SVMs)** | Bộ phân loại phân biệt (discriminative classifier) dựa trên việc tìm **siêu phẳng phân tách tối ưu** để tối đa hóa lề (margin) giữa các lớp. |
| **Boosting (ví dụ: AdaBoost)** | Kết hợp nhiều **bộ phân loại yếu (weak learners)** để tạo ra một **bộ phân loại mạnh (strong classifier)**. |

### 2. Phát hiện Đối tượng (Object Detection)

Xác định vị trí (hộp giới hạn) và phân loại đối tượng.

#### A. Phương pháp truyền thống (Window-based)

*   **Cửa sổ trượt (Sliding Window):** Trượt một cửa sổ qua mọi vị trí và tỷ lệ trên ảnh để kiểm tra có đối tượng không.
    *   **Hạn chế:** Độ phức tạp tính toán cao (phải kiểm tra số lượng lớn vị trí/tỷ lệ).
*   **Viola-Jones Face Detector:**
    *   Đạt tốc độ thời gian thực nhờ sử dụng **Ảnh tích lũy (Integral Image)** để tính toán nhanh **Đặc trưng chữ nhật (Rectangular/Haar Features)**.
    *   Sử dụng **AdaBoost** để lựa chọn tập hợp nhỏ các đặc trưng phân biệt nhất và kết hợp chúng.
    *   Sử dụng cấu trúc **Phân tầng (Attentional Cascade)** để loại bỏ nhanh các cửa sổ không phải đối tượng ở các tầng đầu.
*   **HOG + SVM:** Sử dụng đặc trưng **Histogram of Oriented Gradients (HOG)** kết hợp với **Linear SVM** để phát hiện người (ví dụ: Dalal & Triggs).
*   **Đề xuất vùng (Object Proposals):** Học cách tạo ra các vùng/hộp có tính đối tượng thay vì duyệt cạn kiệt, giúp giảm số lượng vùng cần kiểm tra.

#### B. Phát hiện Đối tượng dựa trên Học Sâu (Deep Learning Detectors)

| Mô hình | Thuộc nhóm | Cơ chế cốt lõi | Đặc điểm/Kỹ thuật liên quan |
| :--- | :--- | :--- | :--- |
| **R-CNN** (Rich Feature CNN) | Hai giai đoạn (Two-stage) | Phân loại các vùng đề xuất (Selective Search). | Rất chậm do cần ~2k forward passes. |
| **Fast R-CNN** | Hai giai đoạn | Xử lý ảnh bằng CNN **trước** khi crop đặc trưng. | Sử dụng **RoI Pool** (Region of Interest Pooling) để tạo vector đặc trưng kích thước cố định từ các vùng có kích thước khác nhau. |
| **Faster R-CNN** | Hai giai đoạn | Sử dụng **Region Proposal Network (RPN)** để thay thế Selective Search. | RPN sử dụng **Anchor Box** để dự đoán khả năng đối tượng/không đối tượng. |
| **YOLO, SSD, RetinaNet** | Một giai đoạn (One-stage) - Anchor-based | Dự đoán hộp giới hạn và lớp trực tiếp từ đầu ra CNN, chia ảnh thành lưới. | **RetinaNet** sử dụng **Focal Loss** để giải quyết vấn đề mất cân bằng (imbalance) giữa anchor dương và âm. |
| **CornerNet** | Một giai đoạn - Anchor-free | Dự đoán đối tượng dưới dạng **cặp điểm góc** (Top-Left và Bottom-Right). |

### 3. Phân vùng Ảnh (Image Segmentation)

Gán nhãn cho từng pixel trong ảnh.

*   **Phân vùng ngữ nghĩa (Semantic Segmentation):** Gán nhãn cho từng pixel (ví dụ: "cỏ", "mèo"), nhưng **không phân biệt** các thực thể riêng lẻ.
    *   Sử dụng **Mạng Tích chập Toàn phần (Fully Convolutional Networks - FCN)**.
    *   Kỹ thuật upsampling: **Transpose Convolution** (hay còn gọi là Deconvolution/Upconvolution).
*   **Phân vùng thực thể (Instance Segmentation):** Gán nhãn cho từng pixel **và phân biệt** các thực thể riêng lẻ của cùng một lớp (ví dụ: "chó 1", "chó 2").
    *   **Mask R-CNN:** Mở rộng từ Faster R-CNN bằng cách thêm một nhánh mạng nhỏ để dự đoán mặt nạ nhị phân (mask) cho mỗi vùng đề xuất (RoI).

**Phương pháp phân vùng cổ điển (hay ra đề trắc nghiệm):**

| Phương pháp | Ý tưởng | Ưu | Nhược | Khi nên dùng |
| :--- | :--- | :--- | :--- | :--- |
| **Thresholding (Otsu)** | Chọn ngưỡng cực tiểu hóa intra-class variance. | Đơn giản, nhanh. | Nhạy chiếu sáng không đồng đều. | Histogram có 2 đỉnh rõ. |
| **Region Growing / Split-Merge** | Tăng trưởng từ điểm hạt giống hoặc chia nhỏ rồi gộp lại theo tiêu chí đồng nhất. | Giữ hình dạng tự nhiên. | Phụ thuộc seed/noise. | Ảnh có vùng đồng nhất rõ. |
| **Watershed** | Xem ảnh gradient như địa hình, nước tràn từ minima. | Phân tách tốt biên nối. | Dễ over-segmentation → cần marker. | Ảnh có đối tượng chồng lấn. |
| **Graph-based (Normalized Cuts, Felzenszwalb)** | Tối ưu hàm cắt đồ thị trên pixel/superpixel. | Dễ thêm ràng buộc toàn cục. | Chi phí tính lớn. | Khi cần cân bằng kết nối nội bộ và tách giữa vùng. |

Ghi nhớ: Watershed cần làm trơn + marker control; Otsu chỉ hiệu quả khi histogram rõ ràng; Region growing cần tiêu chí tương đồng (mức xám/texture).

### 4. Thuật toán Học Sâu (Deep Learning Algorithms)

*   **Mạng Nơ-ron Tích chập (CNN):** Kiến trúc bao gồm nhiều lớp tích chập xếp chồng lên nhau.
*   **Lớp Kết nối đầy đủ (Fully-Connected Layer):** Là phép nhân ma trận giữa vector đặc trưng ảnh và ma trận trọng số (Weight Matrix).
*   **Hàm Softmax:** Chuyển đổi vector điểm số đầu ra thành **xác suất lớp**, đảm bảo giá trị từ 0 đến 1 và tổng bằng 1.
*   **Hàm mất mát Cross-Entropy (Cross-Entropy Loss):** Dùng để đo lường mức độ sai lệch giữa xác suất dự đoán và nhãn thực tế.
*   **Gradient Descent và Backpropagation:** Thuật toán tối ưu để điều chỉnh trọng số (W) nhằm giảm thiểu hàm mất mát (Loss).
*   **Transfer Learning (Học chuyển giao):** Sử dụng các mô hình đã được huấn luyện trước trên tập dữ liệu lớn (ví dụ: ImageNet) để huấn luyện cho các nhiệm vụ khác.
*   **PCA (Principal Component Analysis):** Phép biến đổi không gian đầu vào thành không gian chiều thấp hơn, tìm các chiều độc lập có phương sai lớn nhất (ví dụ: Eigenfaces).

### 5. Phân cụm & phân đoạn không giám sát

| Thuật toán | Nguyên lý | Ưu | Nhược | Ghi chú ôn thi |
| :--- | :--- | :--- | :--- | :--- |
| **K-means** | Lặp gán điểm → cập nhật centroid để giảm SSE. | Nhanh, dễ cài. | Phải chọn k, nhạy khởi tạo, chỉ gom cụm lồi. | Nhớ bước cập nhật centroid, tiêu chí dừng. |
| **K-medoids (PAM)** | Dùng điểm dữ liệu làm đại diện. | Bền với outlier. | Chậm hơn K-means ($O(k(n-k)^2)$). | Áp dụng được với mọi khoảng cách. |
| **GMM + EM** | Mô hình tổng hợp Gaussian, EM học $\mu,\Sigma,\pi$. | Gom cụm elip, trả xác suất. | Cần khởi tạo tốt, dễ kẹt local optimum. | Ghi nhớ E-step/M-step. |
| **Mean Shift** | Dịch điểm tới vùng mật độ cao bằng kernel. | Không cần k, phát hiện số cụm tự nhiên. | Tính toán tốn kém, nhạy bandwidth. | Bandwidth lớn → gộp cụm. |
| **Agglomerative Clustering** | Ghép cụm gần nhau (single/complete/average linkage). | Không cần k ban đầu, cho dendrogram. | $O(n^2)$, nhạy lựa chọn linkage. | Có thể cắt cây để lấy số cụm mong muốn. |

**Liên hệ segmentation:** K-means/Mean Shift trên không gian màu (Lab/HSV) hoặc vector đặc trưng giúp tạo superpixel, làm đầu vào Watershed/Graph-cut. Khi đề hỏi “thuật toán phân cụm nào phù hợp ảnh nhiều outlier?”, chọn K-medoids/Mean Shift.

## VI. Pipeline ôn thi & flashcard key facts

1. **Tiền xử lý:** chuẩn hóa mức xám, cân bằng histogram, khử nhiễu bằng Gaussian (nhiễu Gaussian) hoặc Median (nhiễu salt-pepper).
2. **Lọc & phát hiện biên:** chọn kernel thích hợp (Sobel/LoG); dùng Canny → Hough/RANSAC để suy mô hình.
3. **Biến đổi miền tần số:** Fourier/DCT/Wavelet để lọc hoặc phân tích đa tỉ lệ; kiểm tra ringing khi dùng bộ lọc lý tưởng.
4. **Phân cụm/Segmentation:** K-means/Mean Shift để tạo vùng, sau đó Watershed hoặc Graph-cut tùy bài toán; nhớ điều kiện histogram để áp dụng Otsu.
5. **Nhận dạng/Học sâu:** trích đặc trưng (SIFT, HOG, CNN), phân loại bằng SVM/kNN hoặc fine-tune mạng sâu.

**Flashcard key facts:**

*   Tổng hệ số kernel = 0 → high-pass; = 1 → low-pass.
*   Canny = Gaussian → Gradient → Non-max suppression → Hysteresis.
*   Ideal filter gây ringing; Gaussian không.
*   Watershed cần marker để tránh over-segmentation; Otsu cần histogram 2 đỉnh.
*   EM: E-step tính responsibility, M-step cập nhật tham số.
*   Radon/Hough: điểm trong không gian tham số ↔ đường/điểm trong ảnh.

Sử dụng phần này như checklist cuối cùng trước khi vào phòng thi.