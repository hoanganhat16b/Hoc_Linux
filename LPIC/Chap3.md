### Hệ- [CHap 3](#chap-3)
  - [Configuring the Firmware and Core Hardware](#configuring-the-firmware-and-core-hardware)
    - [Understang the Role of Firmware](#understang-the-role-of-firmware)
    - [Device Interfaces](#device-interfaces)
      - [PCI Boards](#pci-boards)
    - [The USB Interface](#the-usb-interface)
    - [The GPIO Interface](#the-gpio-interface)
    - [The /dev Directory](#the-dev-directory)
    - [The /proc Directory'](#the-proc-directory)
    - [Interrupt Request](#interrupt-request)
    - [Hệ](#hệ)
# CHap 3
## Configuring the Firmware and Core Hardware
### Understang the Role of Firmware
### Device Interfaces
Mỗi thiết bị kết nối với hệ thống Linux sử dụng một số loại giao tiếp chuẩn để kết nối với phần cứng của hệ thống. Phần mềm nhân Linux phải hiểu để gửi và nhận data từ phầm cứng sử dựng các giao thức trên.
#### PCI Boards
Peripheral Component Interconnect(PCI) được phát triển vào năm 1993 như một phương thức để kết nối bo mạch cứng tới bo mạch chủ.Chuẩn PCI Express(PCIe) vẫn được sử dụng cho rất nhiều server và máy trạm để bàn để cung cấp một giao diện phổ thông cho các thiết bị phần cứng bên ngoài.
* Ổ cứng bên trong(Internal hard drives): Ổ cứng sử dụng Serial Advanced Technology Attachment(SATA) and Small Computer System Interfavce(SCSI) thường sử dụng PCI board để kết nối với máy trạm hoặc server.Nhân Linux tự động tiếp nhận cả ổ cứng SATA và SCSI  đã được kết nối tới PCI board.
* Ổ cứng bên ngoài(External hard drives): Ổ cứng mạng sử dụng tiêu chuẩn Fibre Channel cung cấp môi trường ổ đĩa chia sẻ tốc độ cao cho môi trường máy chủ. Để giao tiếp trên mạng cáp quang, máy chủ thường sử dụng bảng PCI hỗ trợ tiêu chuẩn bộ điều hợp BUS (HBA - host bus adapter).
* Network interface cards: Hard-wired network card cho phép bạn kết nối máy chủ hoặc máy chủ với mạng cục bộ(LAN) bằng tiêu chuẩn RJ-45. Các loại kết nói này chủ yếu được tìm thấy trong môi trường mạng tốc độ cao yêu cầu thông lượng cao vào mạng.
* Wireless card: PCI board thích hợp hỗ trợ chuẩn IEEE 802.11 cho việc kết nối không dây tới LANs.
* Thiết bị bluetoothL Công nghệ Bluetooth cho phép kết nối không dây trong phạm vi ngắn với các thiết bị Bluetooth trong mạng peer-to-peer.
* Video accelerators: Các ứng dụng yêu cầu đồ họa nâng cao thường sử dụng thẻ tăng tốc video, giúp giảm tải các yêu cầu xử lý video từ CPU để cung cấp đồ họa nhanh hơn. 
* Audio card: Tương tự, các ứng dụng yêu cầu âm thanh chất lượng cao thường sử dụng thẻ âm thanh đặc biệt để cung cấp khả năng xử lý và phát âm thanh nâng cao, chẳng hạn như xử lý âm thanh vòm Dolby để nâng cao chất lượng âm thanh của phim
### The USB Interface
Giao tiếp Universal Serial Bus(USB) ngày càng phổ biến để sử dụng và hỗ trợ truyền dữ liệu tốc độ cao. 
### The GPIO Interface
Giao tiếp Gerenal Purpose Input/Output(GPIO) trở lên ngày càng phổ biến với các công cụ hệ thống Linux, được thiết kế để điều khiển các thiết bị bên ngoài cho các dự án tự dộng. Nó bao gồm một vài hệ thống như Raspberry Pi or BeagleBone...
### The /dev Directory
Sau khi nhân Linux kết nối với thiết bị qua 1 giao diện, nó phải có thể truyền dữ liệu đến và đi từ thiết bị.File thiết bị được lưu trữ trong thư mực /dev để giao tiếp với phần cứng.
Để lấy lại data từ một thiết bị cụ thể,một chương trình chỉ cần đọc file thiết bị Linux đã được liên kết với thiết bị. Hệ điều hành Linux xử lý tất cả những điều khó khăn khi giao tiếp với phần cứng thực tế.
Khi thêm các thiết bị như USB, network card hoặc ổ cứng, Linux tạo một file trong thư mục /dev đại diện cho thiết bị phần cứng đó. Các ứng dụng có thể tương tác trực tiếp với file để lưu trữ hoặc trích xuất dữ liệu trên thiết bị.
Có hai kiểu file thiết bị trên Linux, dựa trên cách Linux truyền dữ liệu tới thiết bị:
* Tệp thiết bị kí tự(Character device files): Truyền dữ diệu bằng cách gửi 1 kí tự trong 1 khoảng thời gian. Đây là phương thức thường được sử dụng trong nhiều thiết bị như USB hoặc terminals.
* Tệp thiết bị khối(Block device files):Truyền dữ liệu bằng cách gửi những khối dữ liệu lớn. Đây là cahcs thường được sử dụng trên các thiết bị truyền dữ liệu tốc độ cao, điển hình như ổ cứng và card mạng.
Kiểu của file được biểu thị bởi kí tự đầu tiên trong danh sách cho phép.
```
Listing 3.1: Partial	output	from	the	/dev directory
$ ls -al sd* tty*
brw-rw---- 1 root disk 8, 0 Feb 16 17:49 sda
brw-rw---- 1 root disk 8, 1 Feb 16 17:49 sda1
crw-rw-rw- 1 root tty 5, 0 Feb 16 17:49 tty
crw--w---- 1 root tty 4, 0 Feb 16 17:49 tty0
crw--w---- 1 gdm tty 4, 1 Feb 16 17:49 tty1
```
Các thiết bị ổ cứng, `sda` và `sda1`, biểu thị kí tự `b`, biểu thị cho `block device file`. `tty`  terminal file hiển thị  `c`,biểu thị `character device file`.

Bên cạnh file thiét bị, Linux cũng cung cấp một hệ thống gọi là  trình lập bản đồ thiết bị(device mapper).Chức năng của nó được thực hiện bởi nhân Linux. Nó ánh xạ các thiết bị khối vậy lý với các thiết bị khối ảo. Các thiết bị khối ảo này cho phép hệ thống chặn dữ liệu được ghi hoặc được đọc từ các thiết bị vậy lý và thực hiện một số hoạt động trên chúng. Mapped devices được sử dụng bởi Logical Volume Manager(LVM) để tạo ổ cứng vật lý và bởi Linux Unified Key Setup(LUKS) để giải mã dữ liệu trong ổ cứng khi những tính năng này được cài đặt trong hệ thống Linux.
### The /proc Directory'
Thư mục /proc là một trong những công cụ quan trọng mà bạn có thể sử dụng để giải quyết các lỗi phần cứng của hệ thống Linux. Nó không phải là thư mục vật lý trong hệ thống file, nhưng thay thế 1 thư mục ảo mà nhân tự động cung cấp quyền truy cập vào thông tin về cài đặt và trạng thái phần cứng hệ thống.
Nhân Linux thay đổi file và data trong thư mục /proc vì nó giám sát các phần cứng của hệ thống. Để xem trạng thái của các thiết bị phần cứng và cái đặt, bạn chỉ cần đọc tiêu đề của file ảo sử dụng các lệnh văn bản tiêu chuẩn của Linux.
### Interrupt Request
Interrupt REquest(IRQs) cho phép thiết bị phần cứng biểu thị khi chúng có data để gửi tới CPU. Hệ thống PnP phải đăng kí mỗi thiết bị phần cứng được cài đặt trong hệ thống có một địa chỉ IRQ riêng biệt.
Ta có thể xem IRQs hiện tại sử dụng trong hệ thống Linux bằng cách tìm kiếm tại files  /proc/interrupts
```
$ cat /proc/interrupts
CPU0
0: 36 IO-APIC 2-edge timer
1: 297 IO-APIC 1-edge i8042
8: 0 IO-APIC 8-edge ~~rtc0~~
9: 0 IO-APIC 9-fasteoi ~~acpi~~
12: 396 IO-APIC 12-edge i8042
14: 0 IO-APIC 14-edge ata_piix
...
```
### I/O Ports
Cổng hệ thống I/O nằm bên trong bộ nhớ nơi CPU có thể gửi và nhận data từ thiết bị phần cứng. Giống với IRQs, hệ thống phải đăng kí mỗi thiết bị một địa chỉ I/O riêng biệt.
Tra cứu cổng I/O đã được đăng kí tại /proc/ioports
```
$ sudo cat /proc/ioports
0000-0cf7 : PCI Bus 0000:00
0000-001f : dma1
0020-0021 : pic1
0040-0043 : timer0
0050-0053 : timer1
0060-0060 : keyboard
...
```
### Direct Memory Acess
Sử dụng cổng I/O để gửi data tới CPU đôi khi có thể chậm chạp.Để tăng tốc, nhiều thiết bị sử dụng các kênh truyền bộ nhớ trực tiếp(DMA).Giống như I/O ports, mỗi thiết bị phần cứng sử dụng DMA phải được đăng kí một kênh số riêng.
```
$ cat /proc/dma
4: cascade
$
``` 
### The /sys Directory
Thư mục /sys là một thứ mục ảo khác, tương tự /proc. Nó được tạo bởi nhân ở định dạng tệp hệ thống sysfs, và nó dung cấp thông tin thêm về thiết bị phần cứng mà người dùng có thể truy cập.
Thư mục /sys có thể chia nhỏ thành nhiều thư mục con dựa trên thiết bị và tính năng của hệ thống.Ta có thể xem thư mục con và file có sẵn trong /sys với lệnh `ls`
```
$ sudo ls -al /sys
total 4
dr-xr-xr-x 13 root root 0 Feb 16 18:06 .
drwxr-xr-x 25 root root 4096 Feb 4 06:54 ..
drwxr-xr-x 2 root root 0 Feb 16 17:48 block
drwxr-xr-x 41 root root 0 Feb 16 17:48 bus
drwxr-xr-x 62 root root 0 Feb 16 17:48 class
```
### Working with Devices
Linux cung cấp 1 lượng lớn công cụ dòng lệnh để thiết bị được kết nối tới hệ thống của bạn, như theo dõi và xử lý vấn đề nếu bạn có kinh nghiệm.
#### Finding Devices
Lệnh `lsdev` hiển thị thông tin về thiết bị phần cứng đã được cài đặt trong hệ thống Linux. Nó lấy thông tin từ /proc/interrupts,/proc/dma,/proc/ioports và kết hợp chúng với nhau để cho 1 kết quả đầu ra
```
$ sudo lsdev
Device
...
DMA IRQ I/O Ports
acpi 9
ACPI 4000-4003 4004-4005 4008-400b 4020-4021
ahci d240-d247 d248-d24b d250-d257 d258-d25b
ata_piix 14 15 0170-0177 01f0-01f7 0376-0376 03f6-03f6
....
```
Lệnh `lsblk` hiển thị thông tin về những thiết bị khối đã được cài đặt trong hệ thống.
```
$ lsblk
NAME MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
loop0 7:0 0 34.6M 1 loop /snap/gtk-common-themes/818
loop1 7:1 0 2.2M 1 loop /snap/gnome-calculator/222
loop2 7:2 0 34.8M 1 loop /snap/gtk-common-themes/1122
loop3 7:3 0 169.4M 1 loop /snap/gimp/113
...
sda 8:0 0 10G 0 disk
└─sda1 8:1 0 10G 0 part
├─ubuntu--vg-root 253:0 0 9G 0 lvm /
└─ubuntu--vg-swap_1 253:1 0 976M 0 lvm [SWAP]
sr0 11:0 1 1024M 0 rom
$
```
#### Working PCI cards
Lệnh `lspci` cho phép bạn xem những cài đặt và PCI đã được công nhận và PCIe card trong hệ thống Linux.
```
$ lspci
00:00.0 Host bridge: Intel Corporation 440FX - 82441FX PMC [Natoma] (rev 02) 
00:01.0ISAbridge:IntelCorporation82371SBPIIX3ISA[Natoma/TritonII] 
00:01.1 IDE interface: Intel Corporation 82371AB/EB/MB PIIX4 IDE (rev 01)
00:02.0 VGA compatible controller: InnoTek Systemberatung GmbH VirtualBox Graphics Adapter 
00:03.0 Ethernet controller: Intel Corporation 82540EM Gigabit Ethernet Controller (rev 02) 
...
```
#### Working USB devices
Lệnh `lsusb`
### Hardware Modules
Nhân Linux cần driver thiết bị để kết nối với các thiết bị phần cứng đã được cài đặt trong hệ thống Linux. Tuy nhiên, biên dịch các driver thiết bị cho tất cả các thiết bị phần cứng vào nhân sữ tạo ra một tệp nhân nhị phân cực kì lớn.
Để tránh trường hợp này , nhân Linux sử dụng modules nhân, nơi cá nhân các module files có thể liên với nhân trong thời gian chạy. Bằng cách này, hệ thống có thể liên kết với những module files cần thiết cho phần cứng hiện hành của hệ thống.
Nơi lưu trữ tệp module đối tượng ở `/lib/modules`.
#### Listing Installed Modules
Lệnh `lsmod` liệt kê tất cả các modules đã được cài đặt trong hệ thống.
```
$ lsmod
Module Size Used by
vboxsf 39706 1
snd_intel8x0 38153 2
snd_ac97_codec 130285 1 snd_intel8x0
ac97_bus 12730 1 snd_ac97_codec
....
```
#### Getting Module Information
Nếu bạn cần thông tin cho một module cụ thể, lệnh `modinfo` sẽ giúp bạn.
```
$ modinfo bluetooth
filename: /lib/modules/3.13.0-63-generic/kernel/net/bluetooth/bluetooth.ko 
alias: net-pf-31
license: GPL
version: 2.17
description: Bluetooth Core ver 2.17
author: Marcel Holtmann <marcel@holtmann.org>
...
$
```
#### Installing News Modules
Nếu bạn cần cài module mới, sử dụng 2 lệnh sau:
* insmod
* modprobe
Lệnh `insmod` phổ biến nhất, yêu cầu bạn chỉ định chính xác tệp module để tải. Lưu ý rằng mỗi phiên bản nhân sẽ có thư mục modules khác nhau.File module có phần mở rộng là `.ko`.
Cách cài bằng lệnh `insmod`:
```
$ sudo insmod /lib/modules/3.13.0-49-generic/kernel/drivers/bluetooth/ 
btusb.ko
password:
$
```
Điểm hạn chế của `insmod` là nó có thể chạy vào trong modules phụ thuộc vào các module khác. Điều đó có thể thất bại nếu module đó không được cài đặt.Để việc cài đặt dễ dàng hơn, dùng lệnh `modprobe`.
```
$ sudo modprobe -iv btusb
insmod /lib/modules/3.13.0-63-generic/kernel/drivers/bluetooth/btusb.ko
$
```
#### Removing Modules
Lệnh `rmmod` sẽ xoá các modules bạn cảm thấy không cần thiết. Bên cạnh đó lệnh `modprobe` kết hợp với option `r` cũng giúp bạn thực hiện điều đó.
```
$ sudo modprobe -rv btusb
rmmod btusb
$
```
## Storage Basics
### Type of Drives
Có nhiều kiểu kết nối ổ đĩa dùng để chạy với hệ thống Linux:
* Parallel Advanced Technology Attachment(PATA) kết nối ổ đĩa đang sử dụng giao tiếp song song,nó yêu cầu 1 cáp rộng. PATA hỗ trợ 2 thiết bị trên 1 adapter.
* Serial Advanced Technology Attachment(SATA) kết nối với ổ cứng đang sử dụng giao tiếp nối tiếp. Nó nhanh hơn PATA, hỗ trợ 4 thiết bị trên mỗi adapter.
* Small Computer System Interface(SCSI) kết nối với ổ đĩa đang dùng giao tiếp song song, nhưng tốc độ bằng SATA. Nó hỗ trợ 8 thiết bị trên mỗi adapter.
Mỗi khi bạn kết nối 1 ổ đĩa tớ hệ thống Linux, nhân Linux đăng kí thiết bị ổ đĩa trong 1 file ở thư mục /dev.File này được gọi là 1 file thô(raw file), bởi vì nó cung cấp 1 đường dẫn trực tiếp tới ổ đĩa từ hệ thống Linux. Bất kì data được viết tới file nghĩa là được viết tới ổ đĩa và đọc dữ liệu file cũng đọc trực tiếp từ ổ đĩa.
Với thiết bị PATA, file này được đặt tên /dev/hdx,nơi   `x`  là một kí tự đại diện cho một ổ đĩa cá nhân, bắt đầu với kí tự `a`.VỚi thiết bị SATA và SCSI, Linux sử dụng /dev/sdx, với `x` đại diện cho một ổ đĩa cá nhân và cũng bắt đầu từ `a`.
### Drive Partitions
Hầu hết hệ điều hành, bao gồm cả Linux, cho phép bạn phân chia 1 ổ đĩa thành nhiều khu.Một phân vùng là một phần độc lập trong ổ đĩa mà hệ điều hành coi nó như một không gian lưu trữ riêng biệt.
Phân vùng ổ đĩa giúp bạn tổ chức dữ liệu tốt hơn, cũng như phân dữ liệu hệ thống từ dữ liệu người dùng. Nếu một người dùng giả mạo lấp đầu dung lượng ổ đĩa bằng dữ liệu, hệ điều hành sẽ vẫn có chỗ trống để tổ chức trên phần vùng riêng biệt.
Phân vùng phải được theo dõi bởi một số hệ thống chỉ mục trên ổ đĩa. Hệ thống này sử dụng phương pháp khởi động cũ BIOS sử dụng phương pháp MBR cho các phân vùng ổ đĩa đang quản lý. Phương pháp này chỉ hỗ trợ tối đa 4 phân vùng chính cho mỗi ổ đĩa.Mỗi phân bùng chính có thể chia ra thành nhiều phân vùng mở rộng.
Hệ thống sử dụng boot khởi động UEFI sử dụng phương pháp cải tiến GUID Partition Table(GPT) cho việc quản lý phân vùng, nơi hỗ trợ tới 128 phân vùng trên mỗi ổ đĩa. Linux đăng kí số hiệu phân vùng với mỗi phân vùng xuất hiện trên ổ đĩa, bắt đầu với 1.
Linux tạo file /dev cho mỗi phân vùng ổ đĩa riêng biệt.Nó đính kèm số hiệu phân vùng đến tận tên thiết bị và đánh số phân vùng chính bắt đầu từ 1, nên phân vùng đầu tiên trong SATA đầu tiên sẽ có dạng /dev/sda1. Phân vùng mở rộng MBR được đánh số bắt đàu từ 5, ví dụ như /dev/sda5.
### Automatic Drive Detection
Hệ thống phát hiện ổ cứng và phân vùng ở thời gian khởi động và đăng kí cho mỗi thiết bị một filename riêng.Hầu hết hệ thống Linux ngày nay sử dụng ứng dụng `udev `. Chương trình `udev` chạy  trong nền tại tất cả các thời điểm và tự động phát hiện phần cứng mới đã được kết nối với hệ thống Linux đang chạy.Khi bạn kết nối với ổ cứng mới, USB,..., `udev` sẽ phát hiện chúng và đăng kí mỗi thiết bị mộit filename riêng trong thư múc /dev.
Các tính năng khác của ứng dụng `udev` là nó tạo `persisten device files` cho thiết bị lưu trữ. KHi bạn thêm hoặc xoá thiết bị lưu trữ di động, tên /dev được đăng kí cho nó có thể thay đổi, phụ thuộc vào thiết bị được kết nối vào bất kì thời điểm nào. Điều này có thể khiến các ứng dụng mỗi lần khó tìm thấy cùng một thiết bị lưu trữ .
Để giải quyết vấn đề này, `udev` sử dụng /dev/disk để tạo liên kết với /dev file thiết bị lưu trữ dựa trên tính duy nhất của mỗi ổ đĩa. `udev` tạo 4 thư mục cho liên kết lưu trữ:
* /dev/disk/by-id: Liên kết các thiết bị lưu trữ bằng tên nhà sản xuất, model, số serial.
* /dev/disk/by-label: Liên kết các thiết bị lưu trữ bằng tên thương hiện đã đăng kí.
* /dev/disk/by-path: Liên kết các thiết bị lưu trữ bằng cổng phần cứng vật lý mà nó kết nối tới.
* /dev/disk/by-uuid: Liên kết các thiết bị lưu trữ bằng mã định danh duy nhất trên toàn cầu 128bit(UUID).
## Storage Alternatives
### Multipath
Nhân Linux hỗ trợ đa phương pháp Device Mapper(DM) , cho phép bạn cấu hình nhiều đường dẫn giữa hệ thống Linux và các thiết bị lưu trữ mang. 
Công cụ DM multipathing trên Linux bao gồm:
* dm-multipath: Đây là module nhân hỗ trợ multipath
* multipath: Dòng lệnh để xem các thiết bị nhiều đường dẫn
* multipahtd: Chương trình chạy ẩn giúp theo dõi và kích hoạt / tắt các đường dẫn
* kpartx: Công cụ dòng lệnh cho việc tạo các mục nhập thiết bị cho thiết bị lưu trữ đa đường dẫn.
### Logical Volume Manager
Logical Volume Manage(LMV) cũng sử dụng công cụ /dev/mapper để cho phép bạn tạo cái thiết bị ổ đĩa ảo.Bạn có thể tổng hợp nhiều phân vùng ổ đĩa vật lý lý thành các ổ đĩa ảo, nơi bạn sau đó dùng nó như một phân vùng duy nhất của hệ thống.
Lợi ích của LVM là bạn có thể thêm hoặc xoá phân vùng vật lý khi cần thiết, mở rộng và thu nhỏ logical volume khi cần.
Sử dụng LVM khá là phức tạp.

![Screenshot_2](https://i.imgur.com/FkCty6c.png)

Trong hình trên có 3 ổ đĩa vật lý mỗi ổ đĩa chứa 3 phân vùng. Logical Volume đầu tiên chứ 2 phân vùng trong ổ đĩa đầu tiên. Logical volume thứ hai kéo dài qua nhiều ổ đĩa, bao gồm phân vùng thứ 3 của ổ đĩa thứ nhất và 2 phân vùng của ổ đĩa thứ 2.Ổ đĩa cuối cùng chưa phân vùng thứ 3 của ổ đĩa thứ 2 và 2 phân vùng đầu tiên của ổ đĩa thứ 3.Phân vùng thứ 3 của ổ đĩa thứ 3 không được đăng kí, nó có thể thêm vào sau cho bất kì logical volume nào cần .
Với mỗi phân vùng vật lý,bạn cần phải đánh dấu kiểu phân vùng giống như kiểu file hệ thống Linux LVM trong fdisk hoặc gdisk.Sau đó bạn phải sử dụng một vài công cụ LVM để tạo và quản lý logical volume:
* pvcreate: tạo ổ cứng vật lý
* vgcreate: nhóm nhiều ổ cứng vật lý thành một ổ đĩa ảo.
* lvcreate: tạo một logical volume từ nhiều phân vùng trong từng ổ đĩa vật lý.
Logical volume tạo các mục nhập trong thư mục /dev/mapper, cái đại diện thiết bị LVM bạn có thể định dạng với 1 file hệ thống và dùng nó như một phân vùng thông thường
Trong khi cài đặt quan trọng của LVM khá là phức tạp, nó cung cấp rất nhiều lợi ích. Nếu bạn chạy bên ngoài không gian của 1 logical volume,chỉ cần thêm phân vùng đĩa mới vào volume.
### Using RAID Technology
Công nghệ Redundant Array of Inexpensive Disks (RAID) thay đổi môi trường lưu trữ dữ liệu . Công nghệ RAID cho phép bạn cải thiện hiệu suất và độ tin cậy truy cập dữ liệu , cũng như thực hiện dự phòng dữ liệu cho khả năng chịu lỗi bằng cách kết hợp nhiều ổ đĩa thành một ổ đĩa ảo.Một vài phiên bải RAID hay dùng:
* RAID 0: Dải đĩa, phân tán dữ liệu để truy cập nhanh hơn.
* RAID 1: Sao chép đĩa, nó sao chép dữ liệu qua hai ổ đĩa.
* RAID 10: Sao chép và dải đĩa, nó cung cấp khả năng phâi dải cho hiệu suất và sao chép cho khả năng chịu lỗi
* RAID 4: Dải đĩa bổ sung tính chẵn lẻ, nó thêm 1 bit chẵn lẻ được lưu trữ trên một ổ đĩa riêng biệt để dữ liệu trên đĩa bị hư hỏng có thể khôi phục được.
* RAID 5: Dải đĩa với tính chẵn lẻ phân tán, nó thêm 1 bit chẵn lẻ bào dữ liệu sọc để nó xuất hiện trên mọi đĩa để đảm bảo rằng khi xuất hiện lỗi thì có thể khôi phục.
* RAID 6: Dải đĩa với tính chẵn lẻ kép, làm sọc cả đĩa dữ liệu và cả bít chẵn lẻ để có thể khôi phục khi ổ đĩa lỗi.
Hạn chế của thiết bị lưu trữ phần cứng RAID là giá cả khá đắt.
## Partition Tools
Sau khi bạn kết nối 1 ổ đĩa với hệ thống Linux bạn sẽ cần tạo phân vùng cho nó. Linux cung cấp nhiều công cụ làm việc với thiết bị lưu trữ thô để tạo phân cùng.
### Working with fdisk
Để sử dụng `fdisk`, bạn cần phải chỉ định tên ổ đĩa bạn muốn làm việc
```
$ sudo fdisk /dev/sda
...
Command (m for help): p
Disk /dev/sda: 10.7 GB, 10737418240 bytes, 20971520 sectors 
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes 
I/O size (minimum/optimal): 512 bytes / 512 bytes 
...
Device Boot    Start    End    Blocks    Id    System
/dev/sda1 *   2048  2099199   1048576    83    Linux
/dev/sda2  2099200 20971519   9436160    83    Linux
Command (m for help)
```
Ví dụ, ổ đĩa /dev/sda được chia thành 2 phân vùng :sda1 và sda2. 
Cột `Id` và `System` liên qua tới kiểu của file hệ thống mà phân vùng được định dạng để xử lý.Cả hai phân vùng được định dạng để hỗ trợ hệ thống tệp Linux.
`fdisk` hơi thô sơ ổ chỗ nó không cho phép bạn thay đổi kích thước phân vùng hiện có.Bạn chỉ có thể xoá phân vùng hiện có vào tạo nó lại từ đầu.
### Working with gdisk
Nếu bạn đang làm việc với ổ đĩa sử dụng phương thức GPT index, bạn sẽ cần sử dụng  `gdisk`
```
$ sudo gdisk /dev/sda
```
### The GNU parted Command
GNU parted command cung cấp giao diện khác với hai công cụu trên. Nó cho phép bạn chỉnh sửa kích thước phân vùng đã tồn tại.
### Graphical Tools
## Understanding Filesystems
### The Virtual Directory
Cấu trúc thư mục ảo Linux bao gồm một thư mục gốc duy nhất, gọi là thư mục `root`. Thư mục root liệu kê tất cả các file và thư mục nằm dưới nó dựa trên đường dẫn thư mục để tiếp cận chúng.
Lưu ý rằng đường dẫn Linux dùng `/` thay cho `\`.Và đường dẫn không có kí tự ổ đĩa.
Địa chỉ thiết bị ổ đĩa trong thư mục ảo sử dụng `mount point`. Một `mount point` là một điểm giữ chỗ thư mục trong thư mục ảo để trỏ đến một thiết bị vật lý.
Linux FileSystem Hierachy Standard(FHS) định nghĩa vị trí và mục đích chính của thư mục .
| Directory  |Description   |
|---|---|
|/boot   |Chứa các file khởi động dùng để khởi động hệ thống   |
|/etc   | Chứa file hệ thống và file cấu hình ứng dụng   |
|/home   |Chứa dữ liệu người dùng   |
|/media   |dùng như một mount point cho thiết bị di động   |
|/mnt   |Cũng được dùng như một mount point cho thiết bị di động   |
|/opt   |Chứa dữ liệu về chương trình thứ ba tuỳ chọn   |
|/tmp   |Chứa các file tam thời được tạo bởi người dùng hệ thống   |
|/usr   |Chứa dữ liệu cho chương trình chuẩn Linux   |
|/usr/bin   |Chứa dữ liệu và chương trình của người dùng nội bộ   |
|/usr/local   |Chứa dữ liệu cho chương trình duy nhất cho cài đặt cục bộ    |
|/usr/sbin     |Chứa dữ liệu về dữ liệu và chương trình hệ thống     |
|/var     |Chứa các dữ liệu giá trị, bao gồm bản ghi hệ thống và chương trình     |

### Maneuvering Around the FileSystem
SỬ dụng thư mục ảo giúp dễ dàng di chuyển tệp thiết bị vật lý này sang cái khác.
```
$ cp /home/rich/Documents/myfile.txt /media/usb
```
Đường dẫn đầy đủ của file liệt kê mỗi thư mục trong cấu trúc thư mục ảo giúp bạn đi tới file cần tìm. Nó gọi là `absolute path`.Nó luôn luôn bắt đầu từ thư mục root `/` và bao gồm mọi thư mục ảo dọc theo cây thư mục.
Thay vào đó, bạn có thể dùng `relative path` để chỉ định vị trí file. Relative path đến một file biểu thị vị trí của một file trong cấu trúc cây thư mục. Nếu chúng ta ở thư mục Documents, ta chỉ cần

```
$ cp myfile.txt /media/usb
```
## Formatting  FileSystems
### Commom Filesystem Types
#### Linux Filesystems
Khi bạn tạo một file hệ thống chuyên biệt để sử dụng trong 1 hệ thống Linux, bạn có thể chọn 1 trong 4 file hệ thống chính sau:
* `btrfs`: Hệ thống file hiệu suất cao , hỗ trợ file lên đến 16 exbibytes.
* `ecryptfs`: The Enterprise Cryptographic Filesystem(eCryptfs) áp dụng Portable Operating System Interface(POSIX). Nó cung cấp một layer để bảo vệ dữ liệu trên thiết bị. Chỉ hệ điều hành đã tạo file hệ thống này mới có thể đọc dữ liệu
* `ext3`: Hỗ trợ tệp lên đến 2TB với tổng kích thước hệ thống tệp là 16TB




















 