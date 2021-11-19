 # Đổi IP trên Centos bằng lệnh `nmcli`
  [I. Topo Lab](#i-topo-lab)

  [II. Mô hình](#ii-mô-hình)

  [III. Cách thực hiện](#iii-cách-thực-hiện)

## I. Topo Lab
- Giả lập trên VMware Workstation
- Centos 7

## II. Mô hình

![Screenshot_7](https://i.imgur.com/M3r3ioz.png)

## III. Cách thực hiện

Bước 1:  Kiểm tra các card mạng đang có và xác định tên card cần đặt IP tĩnh
```
nmcli c
```

![Screenshot_8](https://i.imgur.com/k0cd3ID.png)

Bước 2: Đặt IP với card mạng tương ứng

```
[root@localhost hoanganh]# nmcli c m eth0 ipv4.address 192.168.219.150/24
```

Bước 3: Đặt IP gateway

```
[root@localhost hoanganh]# nmcli c m eth0 ipv4.gateway 192.168.219.2

```

Bước 4: Đặt mode static

```
[root@localhost hoanganh]# nmcli c m eth0 ipv4.method manual
```

Bước 5: Đặt IP DNS

```
[root@localhost hoanganh]# nmcli c m eth0 ipv4.dns "8.8.8.8"
```

Bước 6: Up card mạng

```
[root@localhost hoanganh]# nmcl c up eth0
```
Bước 7: Kiểm tra

![Screenshot_10](https://i.imgur.com/znBmH4E.png)