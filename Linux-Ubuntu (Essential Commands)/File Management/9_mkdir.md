 # mkdir -- make directories
  [I.Notes](#inotes)

  [II.Examples](#iiexamples)

  [III. Command Help(man mkdir)](#iii-command-helpman-mkdir)

## I.Notes
```
mkdir directory_name...
```

Người dùng phải có quyền ghi trong thư mục cha.

## II.Examples
- Create a directory
![Screenshot_5](https://i.imgur.com/jviLFSC.png)

- Tạo nhiều thư mục và tuỳ chọn các thư mục con của chúng:
    ```
    $ mkdir folder folder/folder1 folder/folder2
    ```

- Thêm option `-p` để tạo thư mục con và thư mục cha của chúng néu chúng chưa tồn tại:
    ```
    mkdir -p folder/folder2
    ```

- Tạo thư mục với quyền chỉ định:
    ```
    mkdir -m 777 folder
    ```

## III. Command Help(man mkdir)
```

-m <mode>
|Set the file permission mode of the created directory.
|The mode argument can be in any of the formats specified by the chmod command.
|If a symbolic mode is specified, the operation characters "+" and "-" are interpreted relative to an initial mode of "a=rwx".

-p
|Create intermediate directories as required.
|If this option is not specified, the full path prefix of each operand must already exist.
|On the other hand, with this option specified, no error will be reported if a directory given as an operand already exists.
|Intermediate directories are created with permission bits of rwxrwxrwx (0777) as modified by the current umask, plus write and search permission for the owner.

-v
|Cause mkdir to be verbose, showing files as they are created.
```