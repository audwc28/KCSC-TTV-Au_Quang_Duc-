**Writeup OverTheWrite of Pwn**

**1. Tìm lỗi**
   Em dùng lệnh 'file' để kiêm tra file đã cho thì xác định được là file ELF 64bit nên em mở file bằng IDA 64
   ![image](https://user-images.githubusercontent.com/116651808/212815156-59388bec-afe7-4794-92d5-b0e68b4a03d2.png)

   Sau khi em mở file bằng IDA 64 thì em có được source như sau:
   ![image](https://user-images.githubusercontent.com/116651808/212815999-3a64abbb-fb1e-4eb8-8558-f8b0064b3926.png)

   Đọc source thì em thầy chương trình sẽ cho phép người dùng nhập vào biến buf, rồi dùng các biến v8, v9, v7, s1 so sánh với các giá trị cho trước. Nếu sau sẽ gọi đến
   hàm fail (hàm này sẽ dừng chương trình), nếu đúng hết thì thực hiện lệnh system("bin/sh"), lúc này chúng ta có thể cat flag
   Sử dụng lệnh 'checksec' để xem có thể bof được không
   ![image](https://user-images.githubusercontent.com/116651808/212817837-e366b5b7-649d-43d9-be95-169d1716a014.png)

   Em thấy canary đang disabled nên có thể thực hiện bof
   
   
**2. Ý tưởng**

   Sử dụng gdb để xem cho phép nhập bao nhiêu ký tự cho biến buf
    
   ![image](https://user-images.githubusercontent.com/116651808/212818107-a5285f68-36a8-4081-afef-33bdcf731f80.png)

    Em thấy được biến buf ở vị trí rbp - 0x50 mà chương trình cho phép nhập 0x50 ký tự nên có thể nhập tràn đến rbp. Lúc nhập tràn đẩy các giá trị thỏa mãn theo đề bài
    vào các biến v8, v9, v7, s1
     
   ![image](https://user-images.githubusercontent.com/116651808/212819105-ddc6a997-facf-487f-b870-f09bd96ee0ea.png)

  Stack có dạng như trên nên việc ta nhập tràn từ biến buf sẽ thỏa mãn
   
   
**3. Viết script**
    
  ![image](https://user-images.githubusercontent.com/116651808/212819528-a8e6dee6-46d6-4dc9-8ed0-4e43c16797d6.png)

**4. Lấy flag**

   ![image](https://user-images.githubusercontent.com/116651808/212819599-d63fc73d-1613-4aa6-bdd9-1a5b4e8da8be.png)
