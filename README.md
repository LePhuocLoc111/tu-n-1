# Bài Thực Hành Xử Lý Ảnh với OpenCV

## Giới thiệu

Notebook này bao gồm nhiều đoạn mã sử dụng thư viện OpenCV và NumPy để thực hiện các thao tác xử lý ảnh cơ bản như:

* Tách các kênh màu RGB
* Hoán đổi các kênh màu
* Chuyển đổi và xử lý ảnh trong không gian màu HSV
* Áp dụng bộ lọc trung bình (mean filter) cho ảnh

Tất cả các đoạn mã đều thao tác trên ảnh đầu vào `bird.png` hoặc một thư mục chứa nhiều ảnh.

---

## Nội dung

### 1. Tách các kênh màu RGB

* Đọc ảnh `bird.png` bằng OpenCV (`cv2.imread`).
* Dùng `cv2.split()` để tách ảnh thành ba kênh màu riêng biệt: **Blue**, **Green**, và **Red**.
* Tạo ba ảnh mới chỉ giữ lại một trong ba kênh, hai kênh còn lại được gán giá trị 0.
* Lưu mỗi ảnh kết quả vào thư mục `output_images`.

### 2. Hoán đổi các kênh màu RGB

* Đọc ảnh `bird.png`.
* Thay đổi thứ tự các kênh màu trong ảnh bằng cách sử dụng slicing numpy:

  * Hoán đổi R <-> G
  * Hoán đổi G <-> B
  * Hoán đổi B <-> R
* Lưu các ảnh kết quả vào thư mục `output_swapped_colors`.

### 3. Hiển thị kênh H, S, V từ không gian màu HSV

* Dùng `cv2.cvtColor` để chuyển ảnh từ không gian BGR sang HSV.
* Dùng `cv2.split()` để lấy ba kênh: Hue (H), Saturation (S), và Value (V).
* Tạo các ảnh màu dễ quan sát từng kênh:

  * Hue: Giữ nguyên H, S = 255, V = 255
  * Saturation: Giữ nguyên S, H = 90, V = 255
  * Value: Giữ nguyên V, H = 90, S = 255
* Dùng `cv2.cvtColor` để chuyển về BGR và lưu ảnh vào thư mục `output_hsv_images`.

### 4. Biến đổi kênh HSV

* Chuyển đổi ảnh sang không gian HSV.
* Biến đổi các kênh:

  * Hue: giảm còn 1/3 giá trị gốc (giữ trong giới hạn 0–179)
  * Value: giảm còn 3/4 giá trị gốc (giữ trong giới hạn 0–255)
  * Saturation: giữ nguyên
* Kết hợp lại các kênh đã xử lý thành ảnh HSV mới và chuyển lại sang BGR để lưu vào thư mục `output_modified_hsv`.

### 5. Áp dụng Mean Filter (lọc trung bình)

* Duyệt tất cả các ảnh trong thư mục đầu vào (ví dụ: `D:\197ct09831\baitap t1`).
* Dùng hàm `cv2.blur()` với kernel kích thước (5, 5) để làm mờ ảnh theo bộ lọc trung bình.
* Lưu các ảnh đã xử lý vào thư mục `Exercise_mean_filtered`.

---

## Hướng dẫn sử dụng

### Yêu cầu

* Python 3.x
* Thư viện:

  * OpenCV
  * NumPy
* Cài đặt bằng lệnh:

```bash
pip install opencv-python numpy
```

---

## Giải thích thuật toán

### Tách kênh RGB

* Dữ liệu ảnh màu là một tensor 3 chiều (H x W x 3), mỗi lớp tương ứng một kênh màu.
* `cv2.split()` tách các lớp riêng biệt.
* `cv2.merge()` dùng để kết hợp các kênh thành ảnh mới.

### Hoán đổi kênh màu

* Dùng slicing của NumPy để thay đổi vị trí các kênh màu trong tensor ảnh.
* Các phép đổi thứ tự sẽ dẫn đến thay đổi trong cách ảnh hiển thị màu.

### Không gian màu HSV

* Hue (H): Màu sắc cơ bản (góc trên vòng màu).
* Saturation (S): Độ bão hòa màu (từ xám đến màu đậm).
* Value (V): Độ sáng của màu.
* `cv2.cvtColor()` chuyển đổi ảnh từ không gian BGR sang HSV.

### Biến đổi HSV

* Giảm giá trị H (1/3) → chuyển dịch vòng màu → tạo cảm giác thay đổi màu chủ đạo.
* Giảm giá trị V (3/4) → giảm độ sáng.
* `np.clip()` đảm bảo giá trị hợp lệ, tránh tràn khi xử lý ảnh.

### Lọc trung bình (Mean Filter)

* Là kỹ thuật làm mịn ảnh bằng cách tính trung bình lân cận của mỗi điểm ảnh.
* Giảm nhiễu nhưng có thể làm mờ các chi tiết.
* Thực hiện qua `cv2.blur(img, (5,5))`, tương đương với tích chập kernel đều.

---

> 📌 Mẹo: Các thư mục kết quả được tạo sẵn bằng `os.makedirs(..., exist_ok=True)` giúp tránh lỗi khi chạy lại code nhiều lần.
