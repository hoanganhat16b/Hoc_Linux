- [Chap 4](#chap-4)
# Chap 4
## Using File Management Commands
File trong hệ thống Linux được lưu trữ trong một cấu trúc thư mục độc lập, được gọi là thư mục ảo. Thư mục ảo chưa file của tất cả các thiết bị lưu trữ và ghép chúng lại thành một cấu trúc thư mục duy nhất.Cấu trúc này có một thư mục gốc duy nhất gọi là thư mục `root` (/).
### Naming and Listing Files
Trước khi tìm hiểu cấu trúc thư mục ảo, bạn nên tìm hiểu một số khái niệm cơ bản liên quan đến việc xem xét nội dung của thư mục và sử dụng các thủ thuật như tập tin đính kèm.
####   Displaying Filenames with the *ls* command
Siêu dữ liệu là thông tin mà nó mô tả và cung cấp thông tin bố sung về dữ liệu. 
Lệnh `ls` được sử dụng để liệt kê thông tin các tệp và thư mục.
Cú pháp:
```
ls [OPTION] [FILE]
```
Một số tuỳ chọn hay dùng
|Short   |Long   |Description   |
|---|---|---|
|-1   |N/A   |Liệt kê 1 file hoặc tên thư mục con trên mỗi dòng   |
|-a   |--all   |Liệt kê tất cả file và tên thư mục con, bao gồm cả các file ẩn   |
|-d   |--directory   |Hiển thị siêu dữ liểu của một thư mục thay thế cho tiêu đề  |
|-F   |--classify   |Phân loại từng loại tệp bằng mã chỉ báo(*,/,=,>,@ or ``|`` |
|-i   |--inode   |Hiển thị tất cả file và tên thư mục với chỉ số liên kết của chúng   |
|-l   |N/A   |Hiển thị file và siêu dữ liệu thư mục con, nơi chứa kiểu file, quyền truy cập file, đếm hard link,chủ sở hữu file ... |
|-R   |N/A   |Hiển thị tiêu đề của một thư mục,và cho bất kì thư mục con nằm bên trong cây thư mục gốc,liên tiếp hiển thị tiêu đề của nó(đệ quy)    |
Lưu ý vớI `ls -F`:
* @: là 1 symbol link
* (*):
#### Tạo và đặt tên file
Lệnh `touch` cho phép bạn tạo một file rỗnG. Mục đích chính của lệnh này là cập nhật timestamp của một file và chỉnh sửa. Tuy nhiên, với mục đích học,`touch` rất hữu dụng trong trường hợp tạo file nhanh chóng .
Cách dùng `touch`:
```
$ touch Project43.txt
$
$ ls
Everything Project42.txt Project43.txt 
$
$ touch Project44.txt Project45.txt 
$
$ ls
Everything Project42.txt Project44.txt Project43.txt Project45.txt 
$
```
Lệnh `touch` có thể giúp bạn tạo một file duy nhất hoặc nhiều file cùng một lúc.Để tạo nhiều file, chỉ cần ngăn cách tên file bằng một dấu cách.
Linux rất linh hoạt khi đặt tên file.Tuy nhiên, ta nên quy thủ một số quy ước để giảm bớt sự nhầm lẫn và khó khăn xung quanh việc đặt tên không theo quy ước.Tránh sử dụng các siêu kí tự cho việc đặt tên:
```
* ? [ ] ' " \ $ ; & ( ) | ^ < >
```
Để xác định kiểu tệp, ta sử dụng lệnh `file`:
```
$ file Project42.txt
Project42.txt: ASCII text
$
$ file Everything
Everything: directory
$
```
#### Exploring Wildcard Expansion Rules
Khi sử dụng lệnh `ls` , xác định tệp và tên thư mục có thể gặp một chút khó khăn do tên `file globbing`.
> File globbing là hoạt đỘng nhận dạng các mẫu và thực hiện câu lệnh với phần đuôi mở rộng.

File globbing xảy ra khi bạn sử dụng kí tự đại diện, như dấu (*)..., với một tên file ở trong 1 dòng lệNh. Khi kí tự đại diện được dùng trong phần chính, file globbing khiến tên file mở rộng thành nhiều tên(hay còn gọi là `wildcard expansion`.Ví dụ,  `password` có thể trở thành `password` hoặc `passwrd`.
Khi sử dụng một kí tự đại diện, một dấu sao đại diện cho bất kì kí tự hay số nào.
```
$ ls
cake.txt carmelCake.sh carmelPie.txt carrotCake.txt
$
$ ls c*.txt
cake.txt carmelPie.txt carrotCake.txt
$
```
Dùng dấu hỏi với lệnh `ls`
```
$ ls
bard bat beat bed bet bird bit bot bunt
$
$ ls b?t
bat bet bit bot
$
$ ls b??d
bard bird
$
```
Bạn có thể dùng hai dấu hỏi nếu bạn cần bao gồm hai kí tự.
Dùng ngoặc vuông với lệNh `ls`
```
$ ls
bard bat beat bed bet bEt bird bit bot bunt
$
$ ls b[eio]t
bet bit bot
$
```
Chú ý rằng kí tự ngoặc vuông là cho kí tự vị trí thứ hai trong tên file.
Sử dụng ngoặc vuông có khoảng cách vs `ls`
```
$ ls b[a-z]t
bat bet bEt bit bot
$
```
### Understanding the File Commands
#### Creating Directory
Lệnh `mkdir` giúp bạn tạo thư mục nhanh chóng.Ta dùng lệnh `ls -F` để hiển thị bất kì thư mục nào, bao gồm cả file moiws được tạo với dấu `/` để hiển thị các file trong mỗi thư mục hiển thị
```
$ ls -F
Everything/ Project42.txt Project44.txt Project46.txt 
Life/ Project43.txt Project45.txt Universe/
$
$ mkdir Galaxy
$
$ ls -F
Everything/ Life/ Project43.txt Project45.txt Universe/Galaxy/ 
Project42.txt Project44.txt Project46.txt
```
Xét ví dụ này
```
$ ls -F
Everything/ Life/ Project43.txt Project45.txt Universe/ 
Galaxy/ Project42.txt Project44.txt Project46.txt
$
$ mkdir Projects/42/
mkdir: cannot create directory 'Projects/42/': No such file or directory
$
$ mkdir -p Projects/42/
$
$ ls -F
Everything/ Life/ Project43.txt Project45.txt Projects/ 
Galaxy/ Project42.txt Project44.txt Project46.txt Universe/
$
$ ls -F Projects
42/
$
```
Lỗi xảy ra khi bạn định dùng `mkdir` để tạo thư mục Projects và thư mục con của nó `42`. Thư mục con `42` không thể được tạo mà thư mục cha `Project` không tồn tại trước. Do đó thêm tiền tố `-p` (--parent) cho phép tạo thành công.
#### Copying Files and Directories
Để sao chép một file hay thư mục, sử dụng công cụ `cp`.
Cú pháp
```
cp [OPTION]… SOURCE DEST
```
Ví dụ
```
$ pwd
/home/Christine/SpaceOpera/Emphasis
$
$ ls
melodrama.txt
$
$ cp melodrama.txt space-warfare.txt
$
$ ls
melodrama.txt space-warfare.txt
$
$ cp melodrama.txt
cp: missing destination file operand after 'melodrama.txt' 
Try 'cp --help' for more information.
$
```
Lần đầu lệnh `cp` được sử dụng, cả file nguồn và file đích đều được chỉ định. Do đó không có lỗi gì xảy ra.Tuy nhiên, lần thứ hai lệnh `cp` được dùng, tên file đích không xuất hiện.Nó dẫn đến file nguồn không được sao chép và tạo nên tin nhắn báo lỗi.
Nếu muốn sao chép cả một thư mục ta dùng tuỳ chọn `-R`
```
$ ls -F
Emphasis/
$
$ cp Emphasis Story-Line
cp: omitting directory 'Emphasis'
$
$ ls -F
Emphasis/
$
$ cp -R Emphasis Story-Line
$
$ ls -F
Emphasis/ Story-Line/
$
$ ls -R Emphasis
Emphasis:
chivalric-romance.txt melodrama.txt 
$
$ ls -R Story-Line/
Story-Line/:
chivalric-romance.txt melodrama.txt 
$
```
Trong lần đầu tiên sử dụng lệnh `cp`, ta thiếu tuỳ chọn `-R`. Do đó thư mục nguồn không được sao chép. Tin nhắn lỗi được tạo ra thông báo lệnh `cp` không được dùng với thư mục. Khi đó chỉ cần thêm tuỳ chọn `-R`, lệnh được khởi tạo thành công.
#### Moving /Remaning Files and Directories
Để di chuyển hoặc đặt lại tên cho file hoặc thư mục, ta dùng một lệnh duy nhất : lệnh `mv`.
```
mv [OPTION]… SOURCE DEST
```
Đặt lại tên với `mv`:
```
mv [Ten ban dau] [Ten moi]
```
Ta có thể vừa đổi tên vừa di chuyển :
```
$
$ ls
Emphasis Story-Topics
$
$ ls Emphasis/
chivalric-romance.txt risk-taking.txt
$
$ ls Story-Topics/
chivalric-romance.txt  space-warfare.txt
$
$ mv Emphasis/risk-taking.txt Story-Topics/risks.txt
$
$ ls Emphasis/
chivalric-romance.txt
$
$ ls Story-Topics/
chivalric-romance.txt  space-warfare.txt risks.txt
$
```
#### Deleting Files and Directories
Cú pháp
```
rm [OPTION]… FILE
```
Xoá phân vùng bất kể lý do gì
```
rm -rf [file]
```
Lưu ý khi dùng lệnh `rm -rf` nếu không có tên file đi kèm nó sẽ xoá tất cả mọi thứ
Để cẩn thân ta thêm option `-i` để hỏi nhắc lại trước khi ta xoá
```
$ rm -i Parrot-full-3.7_amd64.iso
rm: remove write-protected regular file 'Parrot-full-3.7_amd64.iso'? y
```
Xoá một cây thư mục hoặc một thư mục đầy file có thể gây nguy hiểm.
Để xoá thư mục và tât cả các file nó quản lý dùng option `-R`
```
$
$ rm -i Emphasis/
rm: cannot remove 'Emphasis/': Is a directory
$
$ rm -ir Emphasis
rm: descend into directory 'Emphasis'? y
rm: remove regular empty file 'Emphasis/melodrama.txt'? y
rm: remove regular empty file 'Emphasis/interplanatary-battles.txt'? y
rm: remove regular empty file 'Emphasis/chivalric-romance.txt'? y
rm: remove directory 'Emphasis'? y
$
```
Xoá một thư mục rỗng 
```
$ mkdir -v EmptyDir
mkdir: created directory 'EmptyDir'
$
$ rmdir -v EmptyDir/
rmdir: removing directory, 'EmptyDir/'
$
```
### Compressing File Commands
### Archiving File Commands
Một số cung cụ giải nén file hay dùng

**gzip**

Tạo 1 file nén đuôi `gz`:

```
gzip test1.txt
```

Giải nén 1 file đuôi `gz`:

```
gzip -d test.txt.gz
```

**tar**

Nén 1 thư mục:

```
tar -zcf folder.tar.gz folder
```
Giải nén thư mục: 
```
tar -zxvf file.tar.gz
```

**zip**

Nén thư mục: 

```
zip -r folder1.zip folder1
```

Giải nén thư mục: 

```
unzip file2.zip
```
#### Duplicating with `dd`
Công cụ `dd` cho phép bạn back up sớm mọi thứ trên 1 ổ đĩa.
Cú pháp
```
dd if=INPUT_DEVICE of=OUTPUT-DEVICE [OPERANDS]
```
### Managing Links
Có hai loại liên kết
* Symbolic Link or Soft Link
* Hard Link
#### Establishing a Hard Link
Một Hard link  là một file hoặc thư mục mà có một chỉ sổ(index/inode number) nhưng ít nhất có hai tên tệp khác nhau.Có một chỉ số duy nhất có nghĩa là có một tệp dữ liệu duy nhất trên hệ thống tệp.Có 2 hoặc nhiều tên nghĩa là file có thể được liên kết bằng nhiều cách. Hard link có 2 tên tệp, một chỉ số, và do đó có 1 vị trí hệ thống tệp nằm trên phân vùng ổ đĩa
![Screenshot_5](https://i.imgur.com/J9tFYRJ.png)
Một Hard link cho phép bạn dùng sao chép giả (`pseudo-copy`) của một tệp mà không thực sự sao chép dữ liệu của nó. Nó thường được sủ dụng trong backup file nơi không đủ dung lượng cho hệ thống file tồn tại để back up dữ liệu.Nếu ai đó xoá tên file, bạn vẫn còn tên file khác được liên kết với data của file trước.
Cú pháp
```
ln file1 file2
```
Khi bạn tạo và sử dụng hard link, một vài điều cần lưu ý
* File gốc phải tồn tại nếu bạn khởi tạo lệnh `ln`
* Tên file thứ hai được liệt kê trong lệnh `ln` phải không tồn tại trước đó để sử dụng lệnh.
* File gốc và hard link của nó chia sẻ cùng chỉ số
* File góc và hard link của nó chia sẻ cùng dữ liệu
* File gốc và bất kì hard link nào của nó có thể tồn tại trong những thư mục khác nhau
* File gốc và hard link của nó phải tồn tại trên cùng hệ thống tệp
#### Constructing a Soft Link
Thông thường, một soft link cung cấp một con trỏ tới một file mà nó có thể tồn tại ở một hệ thống file khác.Hai file không chia sẻ chỉ số bởi vì chúng không cùng trỏ tới cùng dữ liệu.
![Screenshot_6](https://i.imgur.com/H8gzX0i.png)
Để tạo một soft link , ta dùng lệnh sau
```
ln -s [file1]   [file2]
```
Một số điều lưu ý khi sử dụng 1 soft link
* File gốc phải tồn tại trước khi bạn dùng lệnh `ln -s`
* Tên file thứ hai được liệt kê trong `ln -s` phải không tồn tại trước khi dùng lệnh
* File gốc và soft link của nó không chia sẻ cùng chỉ số
* File gốc và soft link của nó không chia sẻ cùng data
* File gốc và bất kể soft link của nó có thể tồn tại trên những thư mục khác nhau
* File gốc và soft link của nó có thể tồn tại trên những hệ thống tệp khác nhau.
#### Looking at Practical Link Uses
**Version Links**: Khi bạn sử dụng trình khởi chạy chương trình, như python or java, nó rất tiện ích nếu bạn không biết phiên bản hiện tại nào được cài đặt. Soft link sẽ giúp bạn điều đó
```
$ which java
/usr/bin/java
$
$ readlink -f /usr/bin/java
/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.201.b09-2.el7_6.x86_64/jre/bin/java
```
**Backups**: Hard link rất hữu ích như một backup giả. Điều này rất hữu ích khi bạn làm việ trên tệp lệnh shell, chương trình hoặc tệp dữ liệu trong thư mục chính.Bạn chỉ cần liên kết hard link với một tên file trong thư mục con để bảo vệ dữ liệu.
```
$ ln ImportantFile.txt SpaceOpera/ImportantFile.txt
$
$ ls -i ImportantFile.txt SpaceOpera/ImportantFile.txt
17671201 ImportantFile.txt 17671201 SpaceOpera/ImportantFile.txt
```
## Managing File Ownership
### Assesing File Ownership
Linux sử dụng 3 tầng tiếp cận để bảo vệ file và thư mục:
* Owner: Trong hệ thống Linux, mỗi file và thư mục được đăng kí với một chủ nhân duy nhất
* Group: Hệ thống Linux cũng đăng kí mỗi file và thư mục một group người dùng duy nhất. Người quản trị có thể chỉ định các đặc quyền cụ thể của nhóm cho tệp và thư mục mà nó khác với đặc quyền của chủ sở hữu.
* Other: Loại quyền này được chỉ định cho các tài khoản không là người sở hữu tệp cũng như người được đăng kí trong nhóm.
Bạn có thể xem người dùng được đăng kí và nhóm cho một file hoặc thư mục bằng cách dùng lệnh `ls -l`
```
$ ls -l
total 12
-rw-rw-r-- 1 Rich sales 1521 Jan 19 15:38 customers.txt
-rw-r--r-- 1 Christine sales 479 Jan 19 15:37 research.txt
-rw-r--r-- 1 Christine sales 696 Jan 19 15:37 salesdata.txt
$
```
### Changing a File's Owner
Chỉ tài khoản người dùng root hoặc người với đặc quyền super user mới có thể thay đổi người dùng đăng kí của một file hoặc thư mục bằng lệnh  `chown`.
Cú pháp
```
chown [OPTIONS] NEWOWNER FILENAMES
```
Tham số `NEWOWNER` là tên người sở hữu mới để thừa hưởng file hoặc thư mục.Bạn có thể chỉ dụng nhiều hơn 1 file hoặc thư mục bằng cách thêm dấu cách giữa các file hoặc tên thư mục.
### Changing a File's Group
Cú pháp
```
chgrp [OPTIONS] NEWGROUP FILENAMES
```
Ta có thể thêm tham số `-R` để thay đổi nhóm thừa hưởng toàn bộ file và thư mục dưới thư mục được chỉ định.
Nếu bạn có quyền super user, lệnh `chown` cho phép bạn thay đổi cả người sở hữ và group được giao phó cho 1 file hoặc thư mục trong cùng 1 lần sử dụng lệnh này.
## Controlling Access to Files
### Understanding Permissions
Khi bạn sử dụng `ls -l` nó sẽ hiển thị thông tin của một file bao gồm cả phần cho phép
```
$ ls -l cake.txt
-rw-rw-r--. 1 Christine Bakers 42 Apr 24 10:45 cake.txt
$
```
Ta sẽ mô tả ngắn gọn từng thông tin có trong dòng trên
* Mã kiểu file(-)
* Kí tự sự cho phép(rw-rw-r--)
* Hard Link(1)
* File owner(Christine)
* File group(Bakers)
* File size(42 bytes)
* Thông tin ngày chỉnh sửa cuối cùng(April 24 10:45)
* Tên file(cake.txt)

Ta sẽ tìm hiểu kĩ hơn về mã kiểu file:
|Code   |Description   |
|---|---|
|-   |File này có thể là file nhị phân, file đọc được, 1 file hình ảnh hoặc 1 file nén lại  |
|d   |Thư mục   |
|l   |File nay là soft link tới một file hay thư mục khác   |
|p   |File này là một đường ống(pipe) để kết nối giữa hai hay nhiều quá trình   |
|s   |File nay là file socket,tương tự như pipe nhưng cho nhiều kiểu giao tiếp hơn, chẳng hạn như hai chiều hoặc nhiều mạng   |
|b   | File là một thiết bị khối, giống như ổ đĩa  |
|c   |File này là một kí tự thiết bị   |

**Quyền đối với thư mục và file**
|Permission   |File   |Directory   |
|---|---|---|
|read   |Cung cấp khả năng đọc/xem dữ liệu được lưu trữ trong file   |Cho phép người dùng liệt kê các file chứa trong thư mục  |
|write   |Cho phép một người dùng chỉnh sửa dữ liệu trong file   |Cho phép người dùng tạo,di chuyển( đặt lại tên),chỉnh sửa thuộc tính, xoá file trong thư mục   |
|execute   |Cung cấp khả năng chạy file   |Cho phép người dùng thay đổi thư mục làm việc hiện tại họ tới vị trí này miễn là quyền này được đặt tên tất cả thư mục mẹ cũng như vậy   |

`r`,`w`,`x` lần lượt thay thế cho read,write,excute.
![Screenshot_7](https://i.imgur.com/mNmi1bp.png)
### Changing a File's Mode
Bất kì tài khoản nào với đặc quyền super user hoặc người sở hữu file/thư mục có thể đăng kí quyền bằng việc sử dụng lệnh `chmod`
Có hai cách đặt mode với `chmod` là `symbol` và `octal` 
#### Using `chmod` with Sysmbolic Mode
**Mức độ chế độ symbol**
|Level   |Description   |
|---|---|
|u   |owner   |
|g   |group   |
|o   |other   |
|a   |all tiers   |
Hai mã được phân chia với kí tự `+` nếu bạn muốn thêm quyền, `-` nếu bạn muốn xoá quyền và dấu `=` nếu đặt quyền với những quyền sau.
Ví dụ
```
$ chmod g-w customers.txt
$
$ ls -l
total 12
-rw-r--r-- 1 Christine marketing 1521 Jan 19 15:38 customers.txt
$
```
`g-w` trong lệnh trên thể hiện xoá quyền `write` đối với nhóm khỏi tệp `custumer.txt`.
Thêm một ví dụ nữa
```
$ chmod ug=rwx research.txt
$
$ ls -l
total 12
-rwxrwxr-- 1 Christine sales 479 Jan 19 15:37 research.txt
$
```
#### Using `chmod` with OctalMode
**Octal mode permissions**
`1` `--x` `execute only`  
`2` `-w-` `write only`  
`3` `-wx` `write and execute`  
`4` `r--` `read only`  
`5` `r-x` `read and execute`  
`6` `rw-` `read and write`  
`7` `rwx` `read, write, and execute`  
Ví du
```
chmod 664 research.txt
```
#### Setting the Default Mode
Để đặt quyền mặc định đối với thư mục hoặc file, ta dùng lệnh umask.
```
$ umask
0022
$
```
Đầu ra của umask hiển thị 4 giá trị hệ bát phân.
* Giá trị đầu tiên thể hiện giá trị của mask cho SUID(4),SGID(1),sticky(1),ignore(0)
* Giá trị thứ hai mask cho người sở hữu
* Giá trị thứ ba mask cho nhóm
* Giá trị thứ tư mask cho quyền của other
Ta luôn có `666` là quyền mặc định đối với file, `777` là quyền mặc định đối với thư mục.
Như vậy để tính quyền mặc định ta tính như sau
```
666 - 022 = 644
777 - 022 = 755
```
Nếu giá trị trừ bị âm ta mặc định là  0
```
$ umask 027
$
$ touch test3
$ ls -l test3
-rw-r----- 1 rich rich 0 Jan 19 17:12 test3
$
```
### Changing Special Access Mode
Có 3 quyền bit đặc biệt mà Linux dùng kiểm soát hành vi nâng cao của tệp và thư mục: SUID,SGID, Sticky bit.
#### Looking at SUID
`Set User ID`(SUID) được dùng với các tệp thực thi. Nó gọi nhân Linux để chạy chương trình với quyền của chủ sở hữu tệp và không với tài khoản người dùng đang chạy.
SUID được biểu hiện bởi kí tự `s` thay cho vị trí `x` đối với chủ sở hữu tệp :`rwsr-xr--`.SUID sẽ cấp quyền tạm thời cho user chạy file với quyền người sở hữu.
Để đặt SUID bit với file, ta dùng 2 cách
```
# chmod u+s myapp // symbolic mode
```

```
# chmod 4750 myapp // octal mode ta thêm số 4 vào đầu phần cài đặt
```
#### Looking at SGID
Tương tự vs SUID, kí tự `s` sẽ thay thế cho kí tự `x`.Và cũng có 2 cách đặt
```
# chmod g+s /sales
```

```
# chmod 2660 /sales // Bao gồm số 2 khi bắt đầu khởi tạo
```
#### Looking at the Sticky Bit
Được dùng cho các thư mục chia sẻ, mục đích ngăn chặn người dùng này có thể xoá file của người dùng kia. Chỉ duy nhất người sở hữu và `root` mới có quyền xoá file.
Nó được kí hiệu `t` thay cho `x`.
Có 2 cách đặt
```
# chmod o+t /sales
```

```
# chmod 1777 /sales // thêm số 1 trước phần đặt quyền
```
## Locating Files
### Getting to Know the FHS
Filesystym Hierachy Standard (FHS) là chuẩn phân cấp hệ thống tệp trong Linux.
### Employing Tools to Locate Files
#### Using the `which` Command
Lệnh `which` hiện thị cho bạn đường dẫn đầy đủ của một lệnh shell được truyền với tham số.
```
$ which passwd
/usr/bin/passwd
$
$ echo $PATH
/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:
/home/Christine/.local/bin:/home/Christine/bin
$
```
#### Using the `where` Command
```
$ whereis diff
diff: /usr/bin/diff /usr/share/man/man1/diff.1.gz
/usr/share/man/man1p/diff.1p.gz
$
$ whereis line
line:
$
```
#### Using the `locate` Command
Một công cụ tiện lợi và đơn giản để tìm kiếm file là `locate`.
```
$ locate Project42.txt
/home/Christine/Answers/Project42.txt
$
```
Sử dụng `locate` với mẫu có thể rắc rối, bởi vì mẫu mặc định file globbing. Nếu bạn không thêm bất cứ kí tự đại diện nào vào mẫu của bạn, lệnh `locate` sẽ tự động thêm kí tự mặc định vào. Ví dụ mẫu của bạn là `passwd` thì nó sự động thành `*passwd*`.
Nếu bạn muốn tìm mẫu `passwd` mà không có file globbing, bạn chỉ cần thêm kí tự `\`.
#### Using the `find` Command
Lệnh `find` rất là linh hoạt. Nó cho phép bạn tìm vị trí file dựa trên dữ liệu cũng như ai là người sở hữu file, lần cuối họ chỉnh sửa, quyền đặt với file ...
Cú pháp
```
file [PATH...] [OPTION] [EXPRESSION]
```

Tham số `PATH` thư mục điểm bắt đầu, bởi vì bạn chỉ định điểm khởi đầu trong cây thư mục và sẽ tìm kiếm qua thư mục đó và tất cả thư mục con(recuisively).
Tìm file với tuỳ chọn `-name` để tránh các kết quả không mong muốn
```
$ find . -name "*.txt"
./Project47.txt
./Answers/Project42.txt
./Answers/Everything/numbers.txt
...
```
Tìm kiếm với chiều sâu thư mục nhất định
```
$ find . -name "*.txt"
./Project47.txt
./Answers/Project42.txt
./Answers/Everything/numbers.txt
...
$
```
Tìm kiếm file với đặc quyền nhất định
```
$ find /usr/bin -perm /4000
/usr/bin/newgrp
/usr/bin/chsh
/usr/bin/arping
/usr/bin/gpasswd
/usr/bin/chfn
/usr/bin/traceroute6.iputils
/usr/bin/pkexec
/usr/bin/passwd
/usr/bin/sudo
$
```
#### Using the `type` Command
Lệnh `type` giúp bạn xem kiểu file
```
$ type ls
ls is aliased to 'ls --color=auto'
$
$ type cd
cd is a shell builtin
$
$ type find
find is /usr/bin/find
$
```