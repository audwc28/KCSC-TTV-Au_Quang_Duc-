 **Writeup Cat from Pwn** 
 
 **#1 Tìm lỗi**
 
  Em sẽ dùng lệnh 'file' để tìm thông tin của file và có kết quả như sau
     
  ![image](https://user-images.githubusercontent.com/116651808/212807726-3f02e914-3565-49b9-8246-2cc62cf8145a.png)
     
  Em sẽ được file được viết là file ELF 64bit nên em mở file cat bằng ida 64 sẽ thấy soure của hàm main như sau:     
  
  ![image](https://user-images.githubusercontent.com/116651808/212927906-184e928f-c703-489f-a670-c3d376e183c4.png)

  
  
  Đọc hàm main em thấy chương trình sẽ tiến hành thực hiện hàm read_flag()(Kiểm tra hàm này thì thấy đã lưu giá trị flag vào biến flag), sau đó tiếp tục cho người dùng
    nhập username và password rồi đem đi so sánh với giá trị đã có sẵn. Nếu đúng thì tiếp tục cho phép nhập vào biến secret và in biến secret rồi kết thúc chương trình.
    Đến đây em nghĩ đến nhập buffer từ biến secret đến biến flag. Em dùng lệnh 'checksec' trong gdb để kiểm tra xem có buffer được không.
    ![image](https://user-images.githubusercontent.com/116651808/212809077-1438d894-e51b-4018-b5fe-4cf951058cc3.png)
    Em thấy được Canary đang disabled nên sẽ tận dụng lỗi buffer over flow được
   
   
   
 **2. Ý tưởng**
    Sau khi đọc source thì em sẽ nhập KCSC_4dm1n1str4t0r cho username và wh3r3_1s_th3_fl4g cho password.
    Dùng gdb thì thấy được khoảng cách từ biến flag đến secret là 512 nên sẽ nhập 512 ký tự cho biến secret
    
    
  **3. Viết script**
  
    from pwn import *
    r = process("./cat")

    r.recvuntil("Username: ")
    r.sendline("KCSC_4dm1n1str4t0r")
    r.recvuntil("Password: ")
    r.sendline("wh3r3_1s_th3_fl4g")
    r.sendline("a"*512)
    r.interactive()
    
 **4. Lấy flag**
   ![image](https://user-images.githubusercontent.com/116651808/212811067-c7f63163-7b62-4d60-a8fb-a65951c3a539.png)
    flag: KCSC{Th1s_1s_f4k3_fl4g} (Chạy trên local nên đây là flag em tự tạo).
