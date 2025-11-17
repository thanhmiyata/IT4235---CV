Chắc chắn rồi. Dựa trên các tài liệu đã cung cấp về Thị giác máy tính (Computer Vision), dưới đây là 30 câu hỏi trắc nghiệm bao quát các chủ đề từ giới thiệu chung, thu nhận ảnh, tăng cường chất lượng ảnh, phát hiện biên, trích chọn đặc trưng cho đến nhận dạng đối tượng và học sâu (Deep Learning).

### 30 CÂU HỎI TRẮC NGHIỆM

#### Phần 1: Giới thiệu và Thu nhận ảnh

**Câu 1:** Thị giác máy tính (Computer Vision) được định nghĩa là gì?
A. Là lĩnh vực khoa học liên ngành cho phép máy tính có thể hiểu được nội dung bức ảnh/video ở mức cao.
B. Là quá trình cầu nối giữa giá trị của các điểm ảnh (pixel) và ngữ nghĩa của bức ảnh.
C. Là lĩnh vực khoa học liên quan đến việc thu nhận và xử lý ảnh 2D.
D. Là lĩnh vực nghiên cứu về trí tuệ nhân tạo để máy tính có thể học mà không cần lập trình rõ ràng.
**Đáp án: A**.

**Câu 2:** Quá trình xử lý ảnh tập trung vào việc tăng cường độ tương phản, lọc nhiễu, biến đổi ảnh 2D được xếp vào cấp độ nào của Thị giác máy tính?
A. Mức cao (High-level Vision).
B. Mức giữa (Middle-level Vision).
C. Mức thấp (Low-level Vision).
D. Mức ngữ nghĩa cao.
**Đáp án: C**.

**Câu 3:** Nhiệm vụ nhận dạng vật thể (object recognition) và hiểu nội dung bức ảnh (scene understanding) thuộc cấp độ xử lý nào?
A. Mức thấp (Low-level Vision).
B. Mức giữa (Middle-level Vision).
C. Mức cao (High-level Vision).
D. Tiền xử lý (pre-processing).
**Đáp án: C**.

**Câu 4:** Trong mô hình ảnh số (Digital image), ảnh đa mức xám (grayscale) thường được biểu diễn bằng bao nhiêu bit cho mỗi điểm ảnh (pixel)?
A. 1 bit.
B. 8 bits (1 byte).
C. 24 bits (3 bytes).
D. 32 bits.
**Đáp án: B**.

**Câu 5:** Hai loại tế bào thụ cảm quang (photoreceptor cells) chính trên võng mạc mắt người là gì?
A. Iris và Pupil.
B. Cones và Lenses.
C. Rods và Cones.
D. Mống mắt và Con ngươi.
**Đáp án: C**.

#### Phần 2: Tăng cường chất lượng ảnh và Lọc ảnh

**Câu 6:** Mục đích chính của kỹ thuật Cân bằng Histogram (Histogram Equalization) là gì?
A. Thay đổi giá trị điểm ảnh chỉ phụ thuộc vào giá trị hiện tại của điểm ảnh đó.
B. Kéo giãn dải động ảnh (dynamic range) một cách tuyến tính.
C. Làm cho histogram của ảnh sau thay đổi hướng tới phân phối đều.
D. Thay đổi ảnh để có một histogram mong muốn (Histogram Matching).
**Đáp án: C**.

**Câu 7:** Biến đổi Log (Log transformations), với công thức $s = c \times \log(1 + r)$, có hiệu ứng gì lên ảnh?
A. Nén các điểm ảnh ở mức xám thấp, làm cho chúng tối hơn.
B. Làm sáng hơn các điểm có mức xám thấp trong khi nén các giá trị có mức xám cao.
C. Làm giảm độ tương phản trong khoảng từ $r_1$ đến $r_2$.
D. Chỉ tạo ra ảnh nhị phân.
**Đáp án: B**.

**Câu 8:** Bộ lọc nào là bộ lọc phi tuyến và rất phù hợp để loại bỏ nhiễu xung (impulse noise) hoặc nhiễu muối tiêu (salt & pepper noise) trong khi vẫn bảo toàn cạnh (edge preserving)?
A. Bộ lọc Trung bình (Mean filter).
B. Bộ lọc Gauss (Gaussian filter).
C. Bộ lọc Laplace (Laplacian filter).
D. Bộ lọc Trung vị (Median filter).
**Đáp án: D**.

**Câu 9:** Để tránh thay đổi độ sáng trung bình của ảnh khi thực hiện lọc tuyến tính (linear filtering), các hệ số của mặt nạ (kernel) phải thỏa mãn điều kiện gì?
A. Tổng các hệ số phải bằng 0.
B. Tổng các hệ số phải bằng 1.
C. Tổng các hệ số phải nhỏ hơn 1.
D. Mặt nạ phải đối xứng gương.
**Đáp án: B**.

**Câu 10:** Khi xử lý ảnh màu (ví dụ: RGB), phương pháp nào được gợi ý để tăng cường độ tương phản mà tránh tạo ra những thay đổi màu bất thường?
A. Thực hiện cân bằng histogram trên mỗi kênh R, G, B.
B. Chuyển ảnh sang không gian màu Lab, HSL/HSV và thực hiện cân bằng histogram trên kênh độ sáng (L hay V).
C. Thực hiện biến đổi Gamma trên kênh R.
D. Thực hiện phép toán Logic AND trên ảnh.
**Đáp án: B**.

**Câu 11:** Khái niệm "tần số cao" trong ảnh tương ứng với loại vùng nào?
A. Vùng đồng nhất / vùng mờ (homogeneous /blur regions).
B. Các thay đổi chậm (Slow changes).
C. Các thay đổi nhanh/đột ngột (fast/abrupt changes) như cạnh, đường viền, nhiễu.
D. Vùng chứa hầu hết năng lượng của ảnh.
**Đáp án: C**.

**Câu 12:** Phép toán hình thái học (Morphological Operations) nào được mô tả là "Erode, then dilate" (Co rồi Giãn) và được dùng để loại bỏ các đối tượng nhỏ, nhưng vẫn giữ hình dạng gốc?
A. Phép giãn (Dilation).
B. Phép co (Erosion).
C. Phép mở (Opening).
D. Phép đóng (Closing).
**Đáp án: C**.

#### Phần 3: Phát hiện Biên và Hình học

**Câu 13:** Biên (Edge) trong ảnh được định nghĩa chủ yếu là nơi có đặc điểm gì?
A. Nơi có giá trị mức xám cố định.
B. Nơi có sự thay đổi cường độ sáng trong ảnh.
C. Vị trí có giá trị đạo hàm bậc 2 bằng 0.
D. Vị trí đạt giá trị trung bình cường độ sáng.
**Đáp án: B**.

**Câu 14:** Về mặt toán học rời rạc, biên là vị trí đạt cực trị trên đại lượng nào?
A. Đạo hàm bậc 0.
B. Đạo hàm bậc 1.
C. Đạo hàm bậc 2.
D. Gradient hướng.
**Đáp án: B**.

**Câu 15:** Bộ phát hiện biên Canny được coi là "tối ưu" nhờ ba tiêu chí chính. Ba tiêu chí đó là gì?
A. Good detection, Low noise, và Unique response.
B. Good detection, Good localization, và Fast processing.
C. Good detection, Good localization, và Single response (độ dày biên = 1).
D. Good localization, High sensitivity, và Low complexity.
**Đáp án: C**.

**Câu 16:** Biến đổi Hough (Hough Transform) có khả năng phát hiện các đường thẳng, đường tròn và các cấu trúc khác với điều kiện nào?
A. Phải biết trước độ lớn của Gradient.
B. Phải sử dụng tọa độ cực $(\rho, \theta)$.
C. Phương trình tham số của cấu trúc đó là xác định.
D. Ảnh đầu vào phải là ảnh nhị phân.
**Đáp án: C**.

**Câu 17:** Phương pháp RANSAC (RANdom SAmple Consensus) được sử dụng để ước lượng tham số mô hình từ dữ liệu quan sát bằng cách nào?
A. Lấy mẫu ngẫu nhiên từ dữ liệu và tìm ra tập hợp các điểm "inliers".
B. Bỏ phiếu (voting) cho tất cả các mô hình tương thích với các đặc trưng.
C. Tính toán sai số bình phương nhỏ nhất (least-squares) trên toàn bộ tập dữ liệu.
D. Sử dụng một tập hợp seed points để tính toán phép biến đổi.
**Đáp án: A**.

#### Phần 4: Trích chọn đặc trưng và So khớp ảnh

**Câu 18:** Đặc trưng toàn cục (Global Features) được sử dụng để làm gì?
A. Mô tả từng vùng nhỏ trong ảnh.
B. Mô tả toàn bộ ảnh như 1 đối tượng.
C. Mô tả đặc trưng kết cấu/màu sắc trong mỗi vùng cục bộ.
D. Xác định điểm đặc trưng (keypoint).
**Đáp án: B**.

**Câu 19:** Moment bất biến của Hu (Hu's moments) được coi là bất biến (invariant) đối với những phép biến đổi hình học cơ bản nào?
A. Tịnh tiến (translation).
B. Tịnh tiến, tỷ lệ (scale), và phép quay (rotation).
C. Tỷ lệ và phép phản chiếu (reflection).
D. Chỉ là tịnh tiến và phép quay.
**Đáp án: B**.

**Câu 20:** Ý tưởng chính của Bộ phát hiện góc Harris (Harris corner detector) là gì?
A. Tìm vị trí mà đạo hàm bậc 2 đi qua 0 (zero-crossing).
B. Tìm vị trí mà gradient có ít nhất 2 hướng biến đổi mạnh trong vùng xung quanh.
C. Tìm vị trí có phản hồi cực đại trên Laplacian-of-Gaussian (LoG).
D. Sử dụng hiệu của các hàm Gauss (DoG) để phát hiện cực trị.
**Đáp án: B**.

**Câu 21:** Để đạt được tính bất biến với tỷ lệ (scale invariance), các bộ phát hiện hiện đại như SIFT thường tìm kiếm cực trị địa phương (local maxima) trên miền nào?
A. Miền tần số.
B. Miền không gian (spatial domain).
C. Miền không gian-scale (space – scale).
D. Miền tọa độ x-y.
**Đáp án: C**.

**Câu 22:** Bộ mô tả SIFT (Scale-Invariant Feature Transform) đạt được tính bất biến với sự thay đổi độ sáng như thế nào?
A. Bằng cách sử dụng các đặc trưng chữ nhật (Rectangular Features).
B. Bằng cách sử dụng đạo hàm bậc 1 và chuẩn hóa vector mô tả (độ lớn vector = 1.0).
C. Bằng cách sử dụng mô hình pin-hole camera.
D. Bằng cách sử dụng phép cân bằng histogram.
**Đáp án: B**.

**Câu 23:** Trong so khớp đặc trưng cục bộ, tiêu chí "Tỷ lệ khoảng cách lân cận gần nhất" (Nearest neighbor distance ratio) được dùng để làm gì?
A. Đảm bảo tất cả các cặp ghép đều được giữ lại.
B. So sánh khoảng cách tới đặc trưng gần nhất ($f_2$) và đặc trưng gần thứ hai ($f'_2$) để lọc ra các cặp ghép kém tin cậy.
C. Chỉ tính toán khoảng cách Euclidean giữa $f_1$ và $f_2$.
D. Thay thế cho thuật toán RANSAC.
**Đáp án: B**.

#### Phần 5: Phân loại, Phát hiện Đối tượng và Học sâu

**Câu 24:** Trong mô hình Túi từ (Bag-of-Words) cho phân loại ảnh, bước "Dictionary Learning" (Học từ điển) được thực hiện bằng cách nào?
A. Sử dụng Biến đổi Fourier.
B. Sử dụng thuật toán phân cụm (clustering) như K-means trên các đặc trưng cục bộ đã trích xuất.
C. Sử dụng phương pháp RANSAC.
D. Sử dụng phân tích thành phần chính (PCA).
**Đáp án: B**.

**Câu 25:** Bộ phát hiện khuôn mặt Viola-Jones (Viola-Jones face detector) đạt được tốc độ phát hiện thời gian thực (real-time) nhờ cơ chế cốt lõi nào?
A. Sử dụng Bộ lọc trung vị (Median filter).
B. Sử dụng Mô hình Deformable Part Model (DPM).
C. Sử dụng mạng Tích chập (CNN).
D. Sử dụng cấu trúc phân tầng (Attentional Cascade) và Ảnh tích lũy (Integral Image).
**Đáp án: D**.

**Câu 26:** Trong Viola-Jones, thuật toán AdaBoost đóng vai trò gì?
A. Chỉ tính toán Ảnh tích lũy.
B. Lựa chọn ra một tập hợp nhỏ các đặc trưng chữ nhật có tính phân biệt cao nhất và kết hợp chúng thành bộ phân loại mạnh.
C. Huấn luyện một mô hình Support Vector Machine (SVM).
D. Thực hiện lọc nhiễu Gaussian.
**Đáp án: B**.

**Câu 27:** Nhược điểm chính của phương pháp phát hiện đối tượng dựa trên Cửa sổ trượt (Sliding Window) truyền thống là gì?
A. Không tương thích với bộ phân loại nhị phân.
B. Chỉ hoạt động với ảnh đơn sắc.
C. Độ phức tạp tính toán cao do phải kiểm tra một số lượng rất lớn các vị trí và tỷ lệ.
D. Không cần dữ liệu huấn luyện âm tính.
**Đáp án: C**.
s
**Câu 28:** Trong các mô hình phát hiện đối tượng hiện đại, mô hình nào thuộc nhóm "One-stage detectors" (Bộ phát hiện một giai đoạn) dựa trên **Anchor**?
A. R-CNN.
B. Faster R-CNN.
C. YOLO (You Only Look Once) / SSD / RetinaNet.
D. Mask R-CNN.
**Đáp án: C**.

**Câu 29:** Sự khác biệt cốt lõi giữa Phân vùng ngữ nghĩa (Semantic Segmentation) và Phân vùng thực thể (Instance Segmentation) là gì?
A. Semantic Segmentation phân biệt các thực thể riêng lẻ, Instance Segmentation thì không.
B. Semantic Segmentation gán nhãn cho từng pixel nhưng không phân biệt các thực thể riêng lẻ, Instance Segmentation phân biệt các thực thể khác nhau của cùng một lớp đối tượng.
C. Semantic Segmentation chỉ dùng CNN, Instance Segmentation chỉ dùng R-CNN.
D. Semantic Segmentation chỉ phân loại, Instance Segmentation chỉ định vị.
**Đáp án: B**.

**Câu 30:** Khi đánh giá hiệu suất của mô hình phát hiện đối tượng, công thức tính Precision (Độ chính xác) là gì?
A. $\frac{TP}{TP + FN}$ (TP: True Positives, FN: False Negatives).
B. $\frac{TP}{TP + FP}$ (FP: False Positives).
C. $\frac{TP + TN}{Tổng số pixel}$ (TN: True Negatives).
D. $\frac{TP}{Tổng số ground truth}$.
**Đáp án: B**.