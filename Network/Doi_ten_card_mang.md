  [I. Topo Lab](#i-topo-lab)

  [II.Mô hình](#iimô-hình)

  [III. Cách thực hiện](#iii-cách-thực-hiện)
  
# I. Topo Lab
- Giả lập trên VMware Workstation
- Centos 7
# II.Mô hình
![Screenshot_1](https://i.imgur.com/hqBYSiJ.png)
# III. Cách thực hiện

Bước 1: Chỉnh sử tham số khởi động nhân
Chính sửa file `/etc/default/grub` và thêm `net.ifnames=0 biosdevname-0` vào dòng `GRUB_CMDLIN_LINUX`

![Screenshot_2](https://i.imgur.com/miLm4fB.png)

Sau khi chỉnh sửa xong chính ta khởi tạo lại file và viết đề lên file đã tồn tại

![Screenshot_4](https://i.imgur.com/RufC2s7.png)

Bước 2: Chỉnh sửa file cấu hình ifcfg
Ta sẽ sửa hai dòng `NAME` và   `DEVICE` thành tên mình muốn

![Screenshot_3](https://i.imgur.com/yHgSSv1.png)

Bước 3: Disable NetworkManger

![Screenshot_6](https://i.imgur.com/VPHf4ix.png)

Bước 4: Khởi động lại hệ thống 
```
#shutdown -r now
```
Check lại kết quả 

![Screenshot_5](https://i.imgur.com/0FRfRXM.png)