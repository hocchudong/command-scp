Hướng dẫn sử dụng lệnh SCP
==========
#### Tìm hiểu lệnh SCP.

#### I. SCP là gì?
- SCP (Secure Copy – Sao chép an toàn) là một ứng dụng sử dụng SSH để mã hóa toàn bộ quá trình chuyển tập tin.
- SCP  là lệnh dùng để di chuyển file dữ liệu giữa các máy tính chạy hệ điều hành Linux từ xa chỉ cần biết địa chỉ ip
- SCP dùng ssh để di chuyển dữ liệu, có chế độ bảo mật giống như ssh.

#### II. Cài đặt và sử dụng:

###### 2.1 .Cài đặt scp:

- Scp có sẵn trong các bản dis của hệ điều hành Linux.Nếu chưa có , cài đặt như sau :
    
```
       Ubuntu/Debian : sudo apt-get install scp -y
       Fedora/RedHat/Centos: yum install scp -y
```
    
- Cài đặt gói ssh trên các máy cần trao đổi dữ liệu:(ubuntu server 12.04,Desktop 12.04)
    
     ```
      sudo apt-get install -y openssh-server
     ```
     
- Kiểm tra ip của máy:
   
    ````
       ifconfig -a 
    ````
   
###### 2.2. Sử dụng scp:
 * Trên hệ điều hành linux:(Ubuntu 12.04):
     
      cú pháp sử dụng chuẩn:

       ```
       scp [-pqrvBC46 ] [-F ssh_config ] [-S program ] [-P port ] [-c cipher ] [-i identity_file ] [-o ssh_option ] [[user@ ] host1 : file1 ] [... ] [[user@ ] host2 : file2 ]
       
       ```
  option:
   ```
    -c  : Chọn thuật toán mã hóa để sử dụng cho việc mã hóa việc truyền dữ liệu.
   
    -i  : Lựa chọn các tập tin mà từ đó nhận dạng (khóa riêng) cho RSA xác thực được đọc
	
    -p : backup lại file gốc.
	
    -r : sao chép lại toàn bộ thư mục.
    
    -C : nén  file trong khi thực hiện:
	   
    -v : cung cấp thông tin chi tiết của quá trình.
    
    -1 : Forces scp to use protocol 1.
   
    -2 : Forces scp to use protocol 2.
    
   ```
 

 #####2.3.Áp dụng:
  
     - Mô hình:
	   
<img src="http://i.imgur.com/9w0qELk.png " width-"400" height="400"> 
		 
    - Thông tin số các thiết bị :
    
  ```    
     * Máy local :
       
	|   OS   |  Ubuntu-12.04 Desktop |
	|--------|:----------------------|
	|   ip   | 192.168.1.14/24       |
	|--------|:----------------------|
	| Ram    |  2GB                  |
	|------- |:----------------------|
	| CPU    |     1                 |
	        
	      * Máy remote: 
	|   OS   |  Ubuntu-12.04 Server  |
	|--------|:----------------------|
	|   ip   | 192.168.1.15/24       |
	|--------|:----------------------|
	| Ram    |  2GB                  |
	|--------|:----------------------|
	| CPU    |     1                 |
   ```

  * Ví dụ:
  
   - Đẩy file "ubuntu1204.qcow2" lên máy Remote /root:
   ```
       scp ubuntu1204.qcow2 root@'192.168.1.15':/root
   ```
   -Copy  file "foobar.txt" từ remote host sang máy local/home/kvm
   
   ```
      scp  root@:foobar.txt  /home/kvm
   ```

   - copy toàn bộ thư mục backup về /home/kvm
   ```
      scp -r root@192.168.1.15:/root/backup /home/kvm
   ```

   - Hiển thị chi tiết quá trình sao chép : 
   ```
      scp -v Label.pdf  root@192.168.1.15
   ```

   - Copy file "test1.sh" và  "test2.sh" từ máy local nên máy remote:
    ```
       scp test1.sh test1.sh root@192.168.1.15:~
    ```

   - Copy file "test.txt" từ máy local host sang máy  remote host sử dụng port 2264:
   
    ```
      scp -P 2264 test.txt root@192.168.1.15:/home/remote/
    ```

   - Copy nhiều tập tin từ máy remote về máy local : 
   ```
     scp remote@192.168.1.15:foo.txt,bar.txt /root .
   ```

   - Giới hạn băng thông sử dụng khi truyền tải:
   ````
      scp -l 400 Label.pdf root@192.168.1.15:
   ````

* SCP còn nhiều tính năng khác nữa. Trên đây chỉ nêu một vài tính năng phổ biến
 
   ======================================================================================================================
#####2.4:  Trên hệ điều hành windows. Ta có thể dùng phần mềm có tính năng tương tự là: WinSCP
   - Dùng để trao đổi dữ liệu giữa máy windows với máy Linux.
   - Tải phần mềm và cài đặt:
   
     ```
	   http://winscp.net/eng/download.php
	 ```
	- Chạy file .exe để  cài đặt
	 ```
	    WinSCP/winscp.exe
     ```

	
  - Sử dụng winscp: 
      Đăng nhập vào phần mềm:
	   <img src="http://i.imgur.com/gIdXo3C.png">


  - Giao diện chính phần mềm:
          <img src="http://i.imgur.com/NqimEhz.png">


   => Từ giao diện phần mềm copy file từ thư mục trong  máy windows sang máy thư mục trong máy linux . OK đợi đến lúc thành công
#### Nguồn tham khảo 
- [10 SCP Commands to Transfer Files/Folders in Linux](http://www.tecmint.com/scp-commands-examples)

