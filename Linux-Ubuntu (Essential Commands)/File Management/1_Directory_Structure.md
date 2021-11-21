
# Directory Structure (Filesystem Hierarchy)

  [I. Directory Structure(Filesystem Hierarchy)](#i-directory-structurefilesystem-hierarchy)

  [II. The Root Directory](#ii-the-root-directory)

  [III. Directories Paths](#iii-directories-paths)

  [IV. Paths starting with a period (.), two periods (..), or a tilde (~)](#iv-paths-starting-with-a-period--two-periods--or-a-tilde-)

  [V. Using wildcard characters to identify files and directories names(meatacharacter wildcards)](#v-using-wildcard-characters-to-identify-files-and-directories-namesmeatacharacter-wildcards)
  
## I. Directory Structure(Filesystem Hierarchy)
Hệ thống tệp lưu trữ thông tin theo cấu trúc phân cấp dạng cây.

Mức gốc của cây được gọi là thư mục `root`, hoặc thư mục ảo(kí hiệu `/`).

Thư mục root chưa toàn bộ file và thư mục từ tất cả các thiết bị(kể cả vật lý hay mount point) của hệ thống.

Mỗi thư mục có thể có file hoặc thư mục con nằm trong nó.

Một file hoặc thư mục được đặt tên bắt đầu bằng dấu chấm `.` thì được ẩn đi và không hiển thị với trình quản lý file mặc định.(Nó sẽ bị ẩn nếu lệnh `ls` không có option `-a`).

## II. The Root Directory

![Screenshot_12](https://i.imgur.com/dc5lTsC.png)

* /bin: chứa lệnh của người dùng(cp,rm,....)
* /sbin: chứa lệnh của người quản trị
* /boot: chứa file khởi động nhân Linux và file nạp cấu hình khởi động
* /dev:chứa file đại diện cho các điểm truy cập vào thiết bị
* /etc/: chứa các file cấu hình của quản trị viên
* /home: chứa các thư mục của người dùng
* /lib: chứa file thư viện
* /media: điểm gắn kết cho các thiết bị
* /mnt: điểm gắt kết cho các thiết bị, phân vùng ổ đĩa,xoá hệ thống file
* /cdrom: điểm gắn kết với cd-roms
* /proc: chứa các file đại diện cho tài nguyên hệ thống
* /root: thư mục root của user
* /run: chứa các file chương trình tạm thời
* /tmp: chứa các file chương trình tạm thời
* /usr: chứa file của người dùng
* /var: chứa file của chương trình

## III. Directories Paths
Bạn có thể xác định một thư mục hoặc 1 file bằng cách sử dụng đường dẫn hoàn chỉnh (bắt đầu từ thư mục root).

Bạn cũng có thể sử dụng đường dẫn rút gọn(rút gọn từ thư mục hiện tại) để xác định thư mục hoặc file.

Ngoài ra còn có một số dạng đặc biệt để xác định đường dẫn của một thư mục hoặc file, bằng cách sử dụng dấu chấm `.`hoặc dấu ngã `~`.

Đường dẫn cũng có thể chứa biến mà chúng có thể thay thế bằng giá trị của chúng khi phân giải tên đường dẫn.


## IV. Paths starting with a period (.), two periods (..), or a tilde (~)
Cấu trúc thư mục sẽ được dùng trong ví dụ dưới đây:
```
[hoanganh@localhost ~]$ mkdir ~/folder ~/folder/folder1 ~/folder/foler2

```

- Một đường dẫn bắt đầu với dấu chấm `.` đại diện cho toàn bộ tên đường dẫn của thư mục hiện tại

    ![Screenshot_13](https://i.imgur.com/twb3VRk.png)

- Một đường dẫn bắt đầu với hai dấu chấm `..` đại diện cho tên đường dẫn hoàn chỉnh của thư mục cha của thư mục hiện tại.
  
    ![Screenshot_14](https://i.imgur.com/nJ7YTPJ.png)

- Một đường dẫn bắt đầu bằng dấu ngã `~` đại diện cho tên đường dẫn hoàn chỉnh của thư mục home của người dùng.
  
    ![Screenshot_15](https://i.imgur.com/wkqGUIC.png)

- Một chuỗi đứng trước dấu ngã `~` đại diện cho tên đường dẫn hoàn chỉnh của người dùng thư mục chỉnh của người dùng được tham chiểu bởi giá trị của chuỗi

    ![Screenshot_16](https://i.imgur.com/N1pBSlm.png)

## V. Using wildcard characters to identify files and directories names(meatacharacter wildcards)

- `*`:Khớp với bất  kì kí tự nào
![Screenshot_17](https://i.imgur.com/wrYrszz.png)

- `?`: Khớp một lần xuấn hiện với một kí tự
![Screenshot_18](https://i.imgur.com/tO6oAqF.png)

- `[...]`: định nghĩa một lần xuất hiện, một bộ, hoặc một khoảng kí tự
  ![Screenshot_19](https://i.imgur.com/l7WQPaO.png)

Bạn cũng có thể sử dụng dấu ngoặc nhọn `{}` để mở rộng tập hợp các kí tự để khớp với một phần của tên tệp hoặc tên thư mục.

![Screenshot_20](https://i.imgur.com/IkZKh35.png)

Bạn cũng có thể sử dụng dấu chấm than `!` để loại từ mẫu:
![Screenshot_21](https://i.imgur.com/6sHcOxq.png)

