**Writeup treasure from pwn**

   Đọc theo hướng dẫn thì em thấy người viết bảo flag được chia làm 3 phần được giấu trong file. Em chạy thử file file thì thấy được phần 1 như sau
   ![image](https://user-images.githubusercontent.com/116651808/212811939-8496dd04-4d0d-4ca8-8735-8fd3aa429527.png)

   **==> Phần 1: KCSC{**
   Tiếp theo em kiểm tra file thì thấy file ELF 64bit nên em mở file bằng IDA 64
   ![image](https://user-images.githubusercontent.com/116651808/212812167-541764f2-b696-4897-9c0d-5030bb81b59d.png)

    Mở bằng IDA 64 em thấy ngay được phần 2
    ![image](https://user-images.githubusercontent.com/116651808/212812327-1d014445-66fc-43c4-97cb-d8739c7ad965.png)

   **Phần 2: 4_t1ny_tr34sur3**
   
   Sau khi em đọc qua các function và xem nội dung của tab IDA - View A thì cũng thấy được phần 3 ở tab IDA ViewA
   ![image](https://user-images.githubusercontent.com/116651808/212813601-99ea6a0f-6596-445c-a31d-2dd1694237af.png)

  **Phần 3: _27651d2df78e1998}**
  
  **Flag: KCSC{4_t1ny_tr34sur3 _27651d2df78e1998}**
