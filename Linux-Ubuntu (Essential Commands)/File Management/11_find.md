## I.Notes
```
find path...
```

Muốn tản lờ lỗi báo quyền truy cập và chuyển hướng chúng tới `/dev/null` bằng cách sử dụng toán tử chuyển hướng STDERR:
```
find path ... 2> /dev/null
```

Để lọc kết quả tìm kiếm,bạn sử dụng các option sau: `-or`,`-o`,`-and`,`-not`.

Để kết hợp nhiều option và tạo thành một biểu thức, ta có thể làm như sau : `\(expresion\)`.
```
$ find . \( -name file1 -or -name folder1 \) -ls
```

```
$ find . \( -name file1 -o -name folder1 \) -ls
```

Bạn có thể khởi tạo câu lệnh bằng kết quả tìm kiếm bằng cách sử dụng option `-exec`, `-ok`.

Option `-exec` khởi tạo câu lệnh trên mỗi file được tìm thấy(hoặc thư mục),không hỏi trước để xác nhận.

Option `-ok` hỏi xác nhận trước khi khởi tạo câu lệnh trên mỗi file được tìm thấy (hoặc thư mục). Bạn có thể xác nhận khởi tạo với lệnh bằng  cách gõ `y` và ấn Enter.

Cú pháp:
```
$ find . -exec command {} \;
```

```
$ find . -ok command {} \;
```

Chú ý việc sử dụng dấu ngoặc nhọn `{}` đóng vai trò giữ chỗ cho tên tệp hoặc thư mục được tìm thấy.Dòng lệnh phải kết thúc bằng dấu chấm phẩy `;`hoặc dấu cộng `+`.

Dấu chấm phẩy `;` bắt thực hiện lệnh cho mỗi tệp được tìm thấy.

Dấu công `+` cho phếp thực hiện câu lệnh trên một nhóm tệp được tìm thấy.

Dấu `;` nên được đi cùng với dấu `/` để tránh việc shell diễn giải dấu `;` như một kí tự được biệt.Tương tự với dấu cộng `+`.

```
$ find . -exec echo {} \;
./folder1
./folder2
```

```
$ find . -exec echo {} \+
./folder1 ./folder2
```

## II. Examples
- Tìm file:
    ```
    find . -type f
    ```