# ls -- list directory contents

  [I.Notes](#inotes)

  [II. Examples](#ii-examples)

  [III. Command Help(man ls)](#iii-command-helpman-ls)

## I.Notes
```
ls file...
```
- Đối với files, `ls` hiển thị tên và thông tin của mỗi file.
- Đối với thư mục, `ls` hiển thị tên và thông tin của file hoặc thư mục được chứa nằm trong mỗi thư mục
- Nếu không có file/thư mục tồn tại, tiêu đề của thư mục hiện tại được hiển thị
- Nếu có nhiều hơn một thư mục/file, các filé được hiển thị đầu tiên
  
## II. Examples
- (Option `-1`): Liệt kê tên của từng file và thư mục trong một dòng
  ![Screenshot_22](https://i.imgur.com/etPH0LU.png)

- Liệt kê tên và thông tin của từng file và thư mục(bao gồm `.`,`..` và file và thư mục bắt đầu bằng `.`)
![Screenshot_23](https://i.imgur.com/YZlDWJ5.png)

    **Note**: Đối với thư mục, số bytes đại diện cho kích cỡ của siêu file mà nó chứa thông tin về thư mục. Nó không đưa bất cứ thông tin gì về kích cỡ thật của file và thư mục nằm trong thư mục đó
- Liệt kê thông tin file và thư mục con với tiêu đề của chúng(bao gồm `.`,`..`, và file và thư mục bắt đầu với `.`)
    ![Screenshot_1](https://i.imgur.com/pG6RXNd.png)

- (Option `-d`) Liệt kê thông tin file và thư mục con với tiêu đề của chúng(bao gồm `.`,`..`, và file và thư mục bắt đầu với `.`)
![Screenshot_2](https://i.imgur.com/p1fquud.png)

- (Option `-S`) Sắp xếp các file và thư mục theo kích thước

    ![Screenshot_3](https://i.imgur.com/SGcnV1V.png)

- (Option `-t`) Sắp xếp file và thư mục theo thời gian chỉnh sửa
    ```
    $ls -alt ~/folder/*
    ```

## III. Command Help(man ls)
![Screenshot_4](https://i.imgur.com/VCmEbyE.png)

Option `-l`(long display): 
`-l` cung cấp nhiều thông tin hơn về thư mục và filé. Dòng đầu tiên của kết quả hiển thị tổng số khối được chứa trong thư mục.
Các dòng tiếp theo miêu tả chi tiết về từng thư mục và file.
Mỗi dòng cung cấp những thông tin sau:
- Kiểu file
- Quyền đối với file
- Số lượng hard link
- Tên người sở hữu file
- Tên nhóm chính của tệp
- Kích thước byte
- Thời gian lần cuối chỉnh sửa
- Tên file
  
**Các kí tự kiểu file**
- `-`: file thông thường
- `d`: thư mục
- `l`: soft link
- `b`: File kí tự khối(thiết bị khối)
- `c`: file kí tự đặc biệt đại diện cho thiết bị
- `s`: socket link
- `p`: FIFO
  
**Quyền đối với file**
|Permission   |File   |Directory   |
|---|---|---|
|read   |Cung cấp khả năng đọc/xem dữ liệu được lưu trữ trong file   |Cho phép người dùng liệt kê các file chứa trong thư mục  |
|write   |Cho phép một người dùng chỉnh sửa dữ liệu trong file   |Cho phép người dùng tạo,di chuyển( đặt lại tên),chỉnh sửa thuộc tính, xoá file trong thư mục   |
|execute   |Cung cấp khả năng chạy file   |Cho phép người dùng thay đổi thư mục làm việc hiện tại họ tới vị trí này miễn là quyền này được đặt tên tất cả thư mục mẹ cũng như vậy   |
|-|File không đọc được, không ghi được, không khởi tạo được|

Đối với một lệnh cụ thể,bạn có thể thấy kí tự `s` thay thế cho kí tự `x`(`-rwsrwsr--`).Kí tự `s` có thể đặt cho các quyền của người dùng(SUID). Nó cho phép một người dùng được thực thi lệnh nhưng quyền sở hưu lệnh đang chạy sẽ do người dùng hoặc nhóm người dùng sở hữu lệnh đó nắm giữ.

Đối với thư mục, đôi khi kí tự `t` sẽ thay thế cho kí tự `x`
(`drwxrwxr-t`). Nó hiển thị rằng sticky bit dã được thêm vào chúng, nghĩa là người dùng có thể thêm hoặc xoá file trong thư mục nhưng họ không thể xoá những file khác.

Đối với file và thư mục, bạn có thể thấy kí tự `+`(`-rwsrwsr--+`).Điều này có nghĩa những file và thư mục này có thêm tính năng được đăng kí với chúng.
