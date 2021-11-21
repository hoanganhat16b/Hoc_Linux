# rm -- remove
  [I.Notes](#inotes)

  [II.Examples](#iiexamples)

  [III. Command Help(man rm)](#iii-command-helpman-rm)

## I.Notes
```
rm source_file
```

Lệnh `rm` không thể đảo ngược. Shell không thể cung cấp thùng rác nơi có thể khôi phục file hay thư mục bị xoá.
Option `-i` được sử dụng để xác nhận trước khi xoá file hoặc thư mục.

## II.Examples
- Xoá một file
  ```
  ![Screenshot_3](https://i.imgur.com/M65ln7z.png)
  ```

- Xoá tất cả file(bao gồm cả file bắt đầu bằng dấu `.`):
  ```
  [hoanganh@localhost folder1]$ rm file1/*

  ```

- Xoá tất cả các file bắt đầu bằng dấu chấm `.`:
  ```
  $ rm folder1/.*
  ```
Nó có thể hiện thông báo "`rm: "." and ".." may not be removed.`".

- Xoá thư mục
  ```
  [hoanganh@localhost ~]$ ls
  folder1
  folder2
  [hoanganh@localhost ~]$ rm -R folder1
  [hoanganh@localhost ~]$ ls
  folder2
  [hoanganh@localhost ~]$

  ```

## III. Command Help(man rm)
![Screenshot_4](https://i.imgur.com/m0Y58BS.png)