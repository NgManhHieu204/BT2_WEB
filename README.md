# BÀI TẬP 02: NGUYỄN MẠNH HIẾU - K225480106020
## NỘI DUNG BÀI TẬP:
### 1. Cài đặt Apache web server
### 2. Cài đặt nodejs và nodered => Dùng làm backend
### 3. Tạo csdl tuỳ ý trên mssql (sql server 2022), nhớ các thông số kết nối: ip, port, username, password, db_name, table_name
### 4. Cài đặt thư viện trên nodered
### 5. Tạo api back-end bằng nodered
### 6. Tạo giao diện front-end
### 7. Nhận xét bài làm của mình
______
### 1. Cài đặt Apache Web Server

B1. Tắt IIS: Mở CMD quyền Admin để chạy lệnh: iisreset /stop

<img width="1220" height="766" alt="image" src="https://github.com/user-attachments/assets/2bd82afd-4e46-4b93-b783-a6af68449e62" />

B2. 
- Download Apache Server

<img width="871" height="52" alt="image" src="https://github.com/user-attachments/assets/ab617696-fd8d-4daa-8453-0f931ca4396a" />

--> Lưu ý: đảm bảo đã cài Visual C++ Redistributable 14.44.35208

- Giải nén File ra ổ D:

<img width="825" height="727" alt="image" src="https://github.com/user-attachments/assets/6db48b4f-45f4-4884-9e50-f26386bf5900" />

B3. Cấu hình: File httpd.conf: 

- Tạo thư mục chứa Website với tên: nguyenmanhhieu

<img width="905" height="736" alt="image" src="https://github.com/user-attachments/assets/ca59142f-b3cd-433a-a47c-a64f1f09b352" />

- Tạo 1 File index đơn giản để kiểm tra:

<img width="893" height="376" alt="image" src="https://github.com/user-attachments/assets/b1c09e33-1315-4e29-9f1b-8184b3d87cec" />

- Mở D:\Apache24\conf\httpd.conf bằng Notepad với quyền Admin

  - Sửa dòng ServerRoot

   <img width="893" height="612" alt="Screenshot 2025-10-26 015732" src="https://github.com/user-attachments/assets/4e908cb6-ac61-40de-a0de-257bfe98dcfe" />

  - Sửa DocumentRoot và Directory

   <img width="978" height="560" alt="Screenshot 2025-10-26 020234" src="https://github.com/user-attachments/assets/c9746c8e-045e-4756-88c9-85350da23dac" />

  - Tìm và bỏ dấu '#' trước dòng #Include conf/extra/httpd-vhosts.conf

   <img width="693" height="674" alt="image" src="https://github.com/user-attachments/assets/1011780d-cb1a-4a1b-bd4c-af013edcad8b" />

  - Tìm và bỏ dấu '#' trước dòng #LoadModule vhost_alias_module modules/mod_vhost_alias.so để có thể chạy nhiều website khác nhau trên cùng một server Apache

   <img width="817" height="707" alt="image" src="https://github.com/user-attachments/assets/daf54b43-085b-42a7-93af-fb3c4a516538" />

B4. Cấu hình: File httpd-vhosts.conf: 

- Mở D:\Apache24\conf\extra\httpd-vhosts.conf bằng Notepad với quyền Admin và thêm cấu hình website

<img width="1033" height="679" alt="image" src="https://github.com/user-attachments/assets/6dda10f2-2614-4c4d-98f7-129c3a29d6e4" />

B5. Fake IP: 

- Mở Notepad với quyền Admin -> Chọn File -> Chọn Open rồi tìm với đường dẫn C:\Windows\System32\drivers\etc -> Chọn All File -> Chọn hosts

- Thêm dòng 127.0.0.1 nguyenmanhhieu.com vào cuối

<img width="879" height="682" alt="image" src="https://github.com/user-attachments/assets/515252b4-ee51-4fdb-ad63-2d30cd0e52ff" />

- Thao tác dòng lệnh trên File D:\Apache24\bin\httpd.exe: -k install, -k start và -t để kiểm tra -> nếu báo Syntax OK là thành công

<img width="1162" height="677" alt="image" src="https://github.com/user-attachments/assets/704b5edc-f1e6-4651-bd30-b7a862b16efa" />

- Kết quả: Mở trình duyệt và truy cập http://localhost hoặc http://nguyenmanhhieu.com

<img width="1013" height="604" alt="image" src="https://github.com/user-attachments/assets/ed54ef2f-70f5-4998-91b7-32ada38b3ff6" />

### 2. Cài đặt nodejs và nodered => Dùng làm backend

B1. Cài đặt Nodejs v20.19.5 vào D:\nodejs

<img width="798" height="677" alt="image" src="https://github.com/user-attachments/assets/897af146-2a0a-406f-bd9b-9e7c5ae76526" />

B2. Cài đặt Nodered: Mở CMD với quyền Admin vào D:\nodejs và chạy lệnh npm install -g --unsafe-perm node-red --prefix "D:\nodejs\nodered"

<img width="793" height="495" alt="image" src="https://github.com/user-attachments/assets/f017a497-1ad6-4005-970a-327c545ab5c6" />

B3. Cài đặt NSSM: Giải nén và Copy nssm.exe vào thư mục D:\Nodejs\Nodered

<img width="807" height="536" alt="image" src="https://github.com/user-attachments/assets/2c43a619-6280-4c19-85b1-bd4326720fc0" />

B4. Tạo file khởi động Node-RED

- Vào Notepad với quyền Admin -> Tạo 1 file mới với nội dung: @echo off REM fix path set PATH=D:\nodejs;%PATH% REM Run Node-RED node "D:\nodejs\nodered\node_modules\node-red\red.js" -u "D:\nodejs\nodered\work" %*

- Sau đó lưu với tên run-nodered.cmd vào D:\Nodejs\Nodered

<img width="810" height="570" alt="image" src="https://github.com/user-attachments/assets/74bd5e9e-8041-43da-8aac-ff8a78c06351" />

B5. cài đặt service `a1-nodered`:

- Vào CMD gõ cd /d D:\Nodejs\Nodered

- Chạy lệnh nssm.exe install a1-nodered

- Khi cửa sổ NSSM Service Installer hiện ra:
   
   - Path: trỏ tới "D:\Nodejs\Nodered\run-nodered.cmd"
 
   - Startup directory: là D:\Nodejs\Nodered
 
   --> Ấn Install 

- Cài dặt thành công

<img width="619" height="113" alt="image" src="https://github.com/user-attachments/assets/3e9c9701-1a29-4778-8fe3-12b40c9100d8" />

- Chạy lệnh nssm start a1-nodered --> báo The operation completed successfully là thành công

<img width="573" height="92" alt="image" src="https://github.com/user-attachments/assets/d831ff1d-b506-4a1f-8670-4e1544f6839e" />

- Kết quả:

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/dd6b36d7-ed12-48f2-b36e-bb5ab8f670b2" />

### 3. Tạo csdl tuỳ ý trên mssql (sql server 2022), nhớ các thông số kết nối: ip, port, username, password, db_name, table_name

B1. Tạo Database: 

- Dùng code để tạo DB và thông tin User nhanh chóng

<img width="1791" height="660" alt="image" src="https://github.com/user-attachments/assets/972880e9-a806-41ff-bf91-73898d393318" />

B2. Ghi nhớ thông tin

- IP

<img width="802" height="142" alt="image" src="https://github.com/user-attachments/assets/643ec7dd-ba82-40a6-850c-9b01eb1e49d7" />

- PORT

<img width="504" height="622" alt="image" src="https://github.com/user-attachments/assets/9fd6f511-5fa3-480b-aaa0-8e325e4ceb7b" />

### 4. Cài đặt thư viện trên nodered

B1. Truy cập Nodered bằng url: http://localhost:1880

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/dd6b36d7-ed12-48f2-b36e-bb5ab8f670b2" />

B2. Cài đặt các thư viện:

- Tại Nodered -> menu -> Manage palette -> install -> Tìm và cài các package sau:

   - Node-red-contrib-mssql-plus

     <img width="886" height="386" alt="image" src="https://github.com/user-attachments/assets/457b5414-8971-46fe-bd3f-60550d64e6c5" />

   - Node-red-node-mysql

     <img width="889" height="356" alt="image" src="https://github.com/user-attachments/assets/26445c72-b7b5-4444-bd12-a7f92ebe5b29" />

   - Node-red-contrib-telegrambot

     <img width="892" height="352" alt="image" src="https://github.com/user-attachments/assets/a44d036e-c236-45f2-a54c-5a54f737890d" />

   - Node-red-contrib-moment

     <img width="885" height="383" alt="image" src="https://github.com/user-attachments/assets/c0dc8493-2323-4d75-9163-c36a7ec8bc0e" />

   - Node-red-contrib-influxdb

      <img width="1010" height="396" alt="image" src="https://github.com/user-attachments/assets/c062f59a-52b3-40ac-b33a-0a9978c0cb9e" />

   - Node-red-contrib-duckdns

      <img width="947" height="411" alt="image" src="https://github.com/user-attachments/assets/a52a5d41-e962-493a-b0e3-eaff79112afc" />

   - Node-red-contrib-cron-plus

     <img width="928" height="413" alt="image" src="https://github.com/user-attachments/assets/bd054615-8ba5-4a92-9275-393594e61866" />

B3. Sửa file D:\nodejs\nodered\work\settings.js:

- Tìm đến chỗ adminAuth, bỏ // ở đầu dòng (8 dòng) 

<img width="1197" height="487" alt="image" src="https://github.com/user-attachments/assets/24e3330b-b966-42ce-b44f-0da40d8c1eb8" />

- Sinh mật khẩu mã hoá mới: dùng Tool: https://tms.tnut.edu.vn/pw.php

<img width="836" height="471" alt="image" src="https://github.com/user-attachments/assets/3fd8fc2d-9a0e-445d-86bc-0934b96a7f63" />

B4. Khởi động lại Nodered

<img width="748" height="278" alt="image" src="https://github.com/user-attachments/assets/4df035d9-8f62-43cf-96fd-d76d60be3ac8" />

B5. Truy cập lại Nodered:

<img width="1526" height="974" alt="Screenshot 2025-10-26 165421" src="https://github.com/user-attachments/assets/0fe36a11-d22d-4bcd-ac94-ed6ea0a18b60" />

### 5. Tạo api back-end bằng nodered

B1. Tại giao diện Nodered - Flow1: Thực hiện kéo thả các node như sau: http in, http response, MSSQL, function

B2. Cấu hình các Node

- Http in:

<img width="725" height="497" alt="image" src="https://github.com/user-attachments/assets/92aba2bc-710a-4f00-a12a-6254e4bb7526" />

- MSSQL:

<img width="758" height="718" alt="image" src="https://github.com/user-attachments/assets/389faed2-9de6-4ca2-a823-265d3592eac0" />

- Function 1:

<img width="1354" height="508" alt="image" src="https://github.com/user-attachments/assets/78a40b2e-fd73-4a0a-b473-0027f74982a3" />

- Kết quả:

<img width="725" height="639" alt="image" src="https://github.com/user-attachments/assets/a14ddde5-959d-4ab3-a903-9278c105de69" />

- Truy vấn theo mssv:

<img width="1307" height="680" alt="image" src="https://github.com/user-attachments/assets/69ce0abb-ea31-41d0-93a8-1562fcd632ac" />

- Kết quả:

<img width="861" height="411" alt="image" src="https://github.com/user-attachments/assets/ebd56b1d-b7f7-492f-a3de-70f0a3fbd38d" />

### 6. Tạo giao diện front-end

- Tạo 3 File index.html, hieu.css, hieu.js:

<img width="1445" height="1002" alt="image" src="https://github.com/user-attachments/assets/30718b90-a4c2-4459-afae-55a3f61ee767" />

<img width="1420" height="941" alt="image" src="https://github.com/user-attachments/assets/5a439ebb-5dbf-4d0e-b972-ac5016926daa" />

<img width="1370" height="898" alt="image" src="https://github.com/user-attachments/assets/33b2ee64-b2c9-4952-a119-4da143389b37" />

- Kết quả: Truy cập nguyenmanhhieu.com

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/79b322d5-6405-4dc5-b80e-9207595efeb8" />

- Hiển thị tất cả sinh viên:

<img width="1531" height="981" alt="image" src="https://github.com/user-attachments/assets/cd5d9f3c-9566-4eae-aa2b-aa9517cb1fa3" />

- Tìm kiếm theo mã sinh viên:

<img width="1566" height="960" alt="image" src="https://github.com/user-attachments/assets/b3438695-1902-48d9-b33a-ced4917de354" />

### 7. Nhận xét bài làm của mình

- Qua quá trình làm bài em đã hiểu rõ cách cài đặt và cấu hình Apache, Nodejs, Nodered:

   - Apache được cấu hình làm web server nội bộ, giúp truy cập giao diện qua địa chỉ http://localhost.

   - Node.js được cài đặt trước để làm môi trường chạy cho Node-RED. Node-RED mặc định chạy trên cổng 1880, có giao diện kéo thả rất dễ thao tác.

   - Trong Node-RED, em sử dụng các node cơ bản như HTTP In, Function, MSSQL, và HTTP Response để xử lý yêu cầu và trả kết quả dạng JSON.

- Em đã nắm được cách tạo và triển khai API trong Node-RED bằng cách thực hành trực tiếp trên giao diện
