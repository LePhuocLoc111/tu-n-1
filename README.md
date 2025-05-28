 Bài 1

import numpy as np
import os
import cv2
Nhập thư viện cần thiết: numpy (xử lý mảng), os (quản lý tệp), cv2 (OpenCV).


os.makedirs('output_images', exist_ok=True)
Tạo thư mục lưu ảnh đầu ra. Nếu đã tồn tại thì không báo lỗi.

img = cv2.imread('bird.png')
Đọc ảnh gốc từ file.


b, g, r = cv2.split(img)
Tách ảnh thành 3 kênh màu: Blue, Green, Red (BGR – mặc định của OpenCV).


zero = np.zeros_like(b)
Tạo một ma trận zero cùng kích thước với kênh ảnh, dùng để "vô hiệu hóa" các kênh không mong muốn.


red_img = cv2.merge([zero, zero, r])
green_img = cv2.merge([zero, g, zero])
blue_img = cv2.merge([b, zero, zero])
Tạo ảnh chỉ giữ 1 kênh màu, 2 kênh còn lại là 0 (đen).


cv2.imwrite('output_images/red_image.png', red_img)

Ghi ảnh đã xử lý ra tệp.

 Bài 2: 

img = cv2.imread('bird.png')
Đọc ảnh gốc.


rg_img = img.copy()
rg_img[:, :, [1, 2]] = rg_img[:, :, [2, 1]]
Hoán đổi kênh G và R. Sử dụng indexing để thay đổi trật tự kênh.


gb_img[:, :, [0, 1]] = gb_img[:, :, [1, 0]]
br_img[:, :, [0, 2]] = br_img[:, :, [2, 0]]
Hoán đổi G–B và B–R theo cách tương tự.


cv2.imwrite(...), print(...)
Lưu ảnh và in thông báo.

Bài 3: 

hsv_img = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
Chuyển ảnh từ hệ màu BGR sang HSV.


h, s, v = cv2.split(hsv_img)
Tách 3 kênh Hue, Saturation, Value.


cv2.merge([h, 255 * ones, 255 * ones])
Tạo ảnh hiển thị riêng kênh Hue với S và V đặt ở mức tối đa để dễ nhìn.


cv2.cvtColor(..., cv2.COLOR_HSV2BGR)
Chuyển ảnh HSV sang lại BGR để hiển thị và lưu.

Bài 4:
h_new = np.clip((h / 3), 0, 179).astype(np.uint8)
Chia kênh Hue cho 3 để thay đổi màu. Dùng clip để giới hạn giá trị trong khoảng hợp lệ (0–179).


v_new = np.clip((v * 0.75), 0, 255).astype(np.uint8)
Giảm độ sáng (Value) xuống 75%.


hsv_modified = cv2.merge([h_new, s, v_new])
result_img = cv2.cvtColor(hsv_modified, cv2.COLOR_HSV2BGR)
Gộp lại và chuyển về BGR để lưu ảnh.

Bài 5: 

cv2.blur(img, (5, 5))
Áp dụng mean filter (lọc trung bình) để làm mịn ảnh. (5, 5) là kích thước kernel (khung lọc).


for filename in os.listdir(input_folder):
Lặp qua toàn bộ ảnh trong thư mục.

Bài 6:
cv2.blur(...) → mean filter  
cv2.GaussianBlur(...) → gaussian filter  
cv2.medianBlur(...) → median filter
Lọc ảnh bằng 3 kỹ thuật khác nhau để so sánh hiệu quả làm mịn hoặc giảm nhiễu.

Bài 7:

gray = cv2.cvtColor(denoised, cv2.COLOR_BGR2GRAY)
Chuyển ảnh về xám để xác định biên.


cv2.Canny(gray, 100, 200) → Canny edge detector  
cv2.Sobel(gray, ...) → Tính đạo hàm Sobel theo x  
cv2.Laplacian(gray, ...) → Toán tử Laplacian
3 phương pháp tìm biên phổ biến trong xử lý ảnh.

Bài 8: 

channels = list(cv2.split(denoised))
np.random.shuffle(channels)
Tách các kênh màu rồi xáo trộn ngẫu nhiên thứ tự.


randomized_rgb = cv2.merge(channels)
Ghép lại để tạo ảnh có màu sắc bất thường/khác lạ.

Bài 9: 

hsv_img = cv2.cvtColor(denoised, cv2.COLOR_BGR2HSV)
h, s, v = cv2.split(hsv_img)
np.random.shuffle([h, s, v])
Tương tự như bài 8 nhưng thực hiện trên không gian màu HSV → tạo hiệu ứng màu mạnh mẽ hơn.


cv2.cvtColor(shuffled_hsv, cv2.COLOR_HSV2BGR)
Chuyển về BGR để hiển thị ảnh kết quả.

