# mv -- move

  [I.Notes](#inotes)
  
  [II. Examples](#ii-examples)

  [III. Command Help(man mv)](#iii-command-helpman-mv)
  
## I.Notes
```
mv source_file target_file

mv source_file ... target_directory

mv source_directory ... target_directory
```

Di chuyển một thư mục,sẽ di chuyển thư mục và tất cả nội dung của nó.

Khi di chuyển file và thư mục, chỉ số và dấu thời gian của file và thư mục không bị thay đổi.

## II. Examples
- Moving file:
  - Chuyển file1 từ folder1 sang folder2
    ```
    $ mv folder1/file1 folder2/

    #Optionally you can also specify the file name to be used for the destination folder
    $ mv folder1/file1 folder2/file1
    ```

  - Chuyển file1 từ folder1 sang folder2(đặt lại tên file2)
    ```
    $ mv folder1/file1 folder2/file2
    ```

- Đổi tên file
  ```
  mv file1 file2
  ```

- Chuyển thư mục
  ```
  mv folder1 folder3
  ```

- Đổi tên thư mục:
  ```
  mv folder1 folder3
  ```

- Bạn có thể dùng cả `cp` và `rm` để di chuyển file.Lần đầu tiên copy file1 từ folder1 sang folder2 và sau đó xoá file1 trong folder1:
  ```
  cp folder1/file1 folder2/; rm folder1/file1
  ```
## III. Command Help(man mv)
![Screenshot_2](https://i.imgur.com/Mkv8XDe.png)