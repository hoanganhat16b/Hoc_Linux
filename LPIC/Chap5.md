- [Chap 5](#chap-5)
# Chap 5
## Understanding the Boot Process
Khi bạn bật hệ thống Linux,nó kích hoạt một chuỗi sự kiện mà sau cùng dẫn đến lời nhắc đăng nhập.
### The Boot Process
* Phần mềm máy chủ được khởi tạo,thực hiện kiểm tra nhanh phần cứng(`Power On Self-Test` - POST) và sau đó tìm kiếm chương trình boot loaders để chạy từ thiết bị có thể khởi động
* Bộ nạp khởi động chạy và xác định chương trình nhân Linux để chạy
* Chương trình nhân Linux nạp vào trong bộ nhớ, chuẩn bị hệ thống, cũng như gắn đến phân vùng root, rồi sau đó chạy chương trình khởi tạo.
* Quá trình khởi tạo bắt đầu chạy các chương trình cần thiết để hệ thống hoạt động.
### Extracting Information about the Boot Process
Sử dụng lệnh `dmesg` để hiện thị nội dung của bộ đệm vòng nhân
```
$ dmesg
[ 0.000000] Initializing cgroup subsys cpuset 
[ 0.000000] Initializing cgroup subsys cpu
[ 0.000000] Initializing cgroup subsys cpuacct
[ 0.000000] Linux version 3.10.0-957.10.1.el7.x86_64 
...
```
Lệnh `journalctl` hiển thị các bản ghi systemd log.
## Looking at Firmware