**Writeup ShortJumps of Pwn**

**1. Tìm lỗi**
    
    Ta có mã nguồn như sau:
    
    ![image](https://user-images.githubusercontent.com/116651808/213092464-71ff7c75-34a4-4a7a-8499-2bfd5140e645.png)


   Ở hàm main có thể tận dụng lỗi bof ở lệnh scanf. Khi xem thêm hàm jmp2 thì thấy có câu lệnh đặc biệt là system(command)
   
   ![image](https://user-images.githubusercontent.com/116651808/213092982-e5b3e639-2529-4dea-ba08-05811852621a.png)

   Nhưng điều khó khăn ở đây là phải thỏa làm một điều kiện jmp = 1 (khai thác lỗi bof ở đây không được) trong khi trước đó iến jmp được khai báo bằng 0. Nhìn lên hàm 
   jmp2 ta lại thấy điểm đặc biệt là có câu lệnh jmp++ có thể làm cho jmp=1.
   
**2. Ý tưởng**
   
   Chúng ta sẽ khai thác lỗi bof ở biến dream để điều hướng đến hàm jmp1 và tràn cho a có giá trị 0xdeadbeef rồi điều hướng lại hàm main
   Ở đây chúng ta tiếp tục khai thác lỗi bof ở biến dream để điều hướng đến hàm jmp2 và tràn cho a có giá trị 0xcafebabe và a+b = 0x13371337. Lúc này chúng ta sẽ lấy
   được shell
 
**3. Viết script**
   
   ![image](https://user-images.githubusercontent.com/116651808/213095735-3344945a-852f-4a78-94a6-e35bba8af638.png)

**4. Lấy flag**

   ![image](https://user-images.githubusercontent.com/116651808/213095967-1d268b05-e62f-4465-9abb-2188c25357f9.png)
