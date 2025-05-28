#Bài1
1.Import thư viện:
cv2: xử lý ảnh.
numpy: xử lý mảng.
os: quản lý thư mục.
2.Tạo thư mục nếu chưa có:

![image](https://github.com/user-attachments/assets/a651fbc1-dc53-4475-b5f1-122ea76e6269)

3.Đọc ảnh gốc (bird.png):
![image](https://github.com/user-attachments/assets/3884575a-e603-45c8-8fd4-092abf122e87)
4.Tách ảnh thành 3 kênh màu B, G, R:

![image](https://github.com/user-attachments/assets/12ee98b8-0c95-40e4-8bd7-558f9badce80)

5.Tạo ảnh đen (zero) để làm trống các kênh không cần dùng:

![image](https://github.com/user-attachments/assets/72c1f3c7-f627-43fd-9126-6c4c8316ff0b)

6.Tạo và lưu ảnh với từng kênh màu:

![image](https://github.com/user-attachments/assets/393bf25e-abfd-4a57-ba3c-0467d3483ed0)

-Red: chỉ giữ kênh r:


![image](https://github.com/user-attachments/assets/fe51def8-6ba1-4286-9037-1aed81a1079b)


-Green: chỉ giữ kênh g:

![image](https://github.com/user-attachments/assets/4c35648b-ab21-4dbe-87cc-868940a284f8)

-Blue: chỉ giữ kênh b:

![image](https://github.com/user-attachments/assets/3417ca8b-9237-4bc8-b7e2-34ab39955bef)

7.Thông báo hoàn tất:

![image](https://github.com/user-attachments/assets/2f826f3c-4dc3-4f67-81b1-08f57b93fa01)
 Kết quả:
Bạn sẽ có 3 ảnh được lưu trong thư mục output_images:

red_image.png

green_image.png

blue_image.png
