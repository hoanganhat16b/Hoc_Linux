  [I. Đổi IP trên Ubuntu](#i-đổi-ip-trên-ubuntu)
  - [1. Mô hình](#1-mô-hình)
  - [2. Cách thực hiện](#2-cách-thực-hiện)
  
 [II. Đổi IP trên Centos](#ii-đổi-ip-trên-centos)
  - [1. Mô hình](#1-mô-hình-1)
  - [2. Cách thực hiện](#2-cách-thực-hiện-1)
  
  [III. Tổng kết](#iii-tổng-kết)
# I. Đổi IP trên Ubuntu
## 1. Mô hình
![Screenshot_15](https://i.imgur.com/6oFabo5.png)
## 2. Cách thực hiện


Bước 1: Vào Terminal

Bước 2: Cài đặt sudo apt install net-tools

Bước 3:Gõ `nmcli dev show` check IP gateway

![Screenshot_3](https://i.imgur.com/5xSuQ4z.png)

Bước 4:Gõ `nm-connection-editor` 

![Screenshot_4](https://i.imgur.com/c6SXjb6.png)

Bước 5:

![Screenshot_5](https://i.imgur.com/72uiHJv.png)

Bước 6:Chọn Add rồi điền địa chỉ IP mong muốn

![Screenshot_6](https://i.imgur.com/06P2Ii8.png)

Bước 7:Bật tắt lại wifi rồi thử ping 8.8.8.8 để kiểm tra

![Screenshot_8](https://i.imgur.com/rK3ps7a.png)

# II. Đổi IP trên Centos
## 1. Mô hình

![Screenshot_14](https://i.imgur.com/9lO8lnS.png)
## 2. Cách thực hiện

Bước 1: Vẫn sử dụng câu lệnh `nmcli dev show`:

![Screenshot_10](https://i.imgur.com/Uet17bC.png)

Bước 2: Dùng vi để chỉnh sửa file config 

`vi /etc/sysconfig/network-scripts/ifcfg-ens33`

![Screenshot_11](https://i.imgur.com/ma6Tuom.png)

 Dưới đây là các option bạn nên lưu ý khi cấu hình, còn lại để mặc định cũng được.

    * DEVICE : tên card mạng đã được liệt kê ở phần 1, nên điền chính xác tên card mạng thì hệ thống mới nhận biết được card nào để cấu hình card mạng cho nó.
    * ONBOOT : phải để option "yes" thì khi reboot hệ thống, network mới tự động được bật lên với cấu hình card mạng tương ứng.
    * BOOTPROTO : cấu hình IP tĩnh hay DHCP. Nếu là DHCP thì để giá trị "dhcp".
    * IPV6INIT : tắt/mở - yes/no chức năng hỗ trợ sử dụng IPv6 trên card mạng ens33.
    * IPADDR : địa chỉ IP tĩnh.
    * PREFIX : subnet mask của lớp mạng IP sử dụng.255.255.255.0 (24)
    * GATEWAY : địa chỉ IP cổng gateway.
    *  DNS1 : thông tin DNS1 server.
    *  DNS2: thông tin DNS2 server.
![Screenshot_12](https://i.imgur.com/jPl0N4l.png)

Bước 3: Lưu file rồi ssh lại để kiểm tra kết quá

![Screenshot_13](https://i.imgur.com/XGbaMPI.png)

# III. Tổng kết

Ping bên máy Ubuntu

![Screenshot_16](https://i.imgur.com/gGz9Ezf.png)

Ping bên Centos

![Screenshot_17](https://i.imgur.com/xZkP9JT.png)

Như vậy đã xong
