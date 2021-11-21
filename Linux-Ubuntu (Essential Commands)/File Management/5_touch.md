# touch -- change file access and modification times

## Notes
Mặc định, lệnh `touch` thay đổi  thời gian sửa dổi và thời gian truy cập của tệp.
Nếu file không tồn tại, nó sẽ được tạo(file rỗng) với quyền mặc định(tên người dùng và tên nhóm của người dùng sẽ được sử dụng như người sở hữu file)

## II.Examples
- Tạo file không tồn tại
  ![Screenshot_18](https://i.imgur.com/EJLEGTw.png)

- Không tạo file nếu file đó không tồn tạo
    ```
    $ touch -c file2

    #file2 doesn't exist im my system, so because of the option "-c" it won't be created.

    $ ls file2
    ls: file2: No such file or directory
    ```
- Thay đổi thời gian truy cập của file
  ![Screenshot_20](https://i.imgur.com/UTP2gBY.png)

- Thay đổi thời gian chỉnh sửa file
  ![Screenshot_21](https://i.imgur.com/Y3kaBTX.png)


## III. Command Help(man touch)

![Screenshot_19](https://i.imgur.com/RmS6miD.png)