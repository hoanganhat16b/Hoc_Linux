# cp/scp -- copy files/directories
  [I.Notes](#inotes)

  [II. Examples](#ii-examples)

  [III. Command Help(man cp)](#iii-command-helpman-cp)
  
## I.Notes
```
cp source_file target_file

cp source_file ... target_directory

scp source_file {DOMAIN_NAME}\\{USER_NAME}@{HOST_NAME}:target_directory

scp {DOMAIN_NAME}\\{USER_NAME}@{HOST_NAME}:source_file target_directory
```

## II. Examples
- Copy file:
  - Tạo một bản sao mới của file1 và đặt tên cho nó là file2
    ```
    cp file1 file2
    ```

  - Copy file1 từ folder1 đến folder2
    ```
    cp folder1/file1 folder2/

    hoặc
    
    cp folder1/file1 folder2/file2
    ```

  - Copy file1( đặt tên thành file2) từ folder1 sang folder2:
    ```
    $ cp folder1/file1 folder2/file2
    ```
  - Copy tất cả các file từ folder1 sang folder2:
    ```
    $ cp folder1/* folder2/
    ```
  - Copy tất cả các file bắt đầu bằng dấu chấm `.`:
    ```
    $ cp folder1/.* folder2/
    ```

- Copy thư mục:
  - Copy từ folder1 sang folder2:
    ```
    cp -R folder1 folder2/
    ```

  - Copy nội dung file và thư mục con bắt đầu bằng dấu chấm `.`:
    ```
    cp -R folder1/* folder2/
    ```

- Secure-copying file/directory:
  - Copy một file từ xa của thư mục cục bộ:
    ```
    $ scp user1@my-remote-host.com:/folder1/folder2/index.php ~/
    ```

  - Copy thư mục từ xa của một thư mục cục bộ:
    ```
    $ scp -r user1@my-remote-host.com:/folder1/folder2/ ~/
    ```

  - Copy một file cục bộ từ một thư mục từ xa:
    ```
    $ scp ~/file1 user1@my-remote-host.com:/folder1/folder2/
    ```
  - Copy một thư mục cục bộ từ một thư mục từ xa:
    ```
    $ scp -r ~/folder user1@my-remote-host.com:/folder1/folder2/
    ```

## III. Command Help(man cp)
![Screenshot_22](https://i.imgur.com/dtYVBi2.png)