## 1. Quyền Superuser (Root Privileges)
* Trong Linux:
    * User thường: `$`
    * Superuser (root): `#`

    👉 Để cài phần mềm, bạn cần quyền **superuser**

#### Cách 1: Dùng sudo

```sh
sudo <command>
```
#### Cách 2: Chuyển sang root
```sh
sudo su -
```

## 2. Install MySQL

* Sau khi đã thêm MySQL repository, chạy lệnh:

```sh
sudo yum install mysql-community-server.x86_64
```

* Quá trình cài đặt
    * Hệ thống sẽ:
        * Hiển thị package cần cài
        * Hiển thị dependencies
    * Bạn cần:
        * Confirm (yes)
        * Import GPG key (bảo mật package)

## 3. Mysqld là gì?

👉 mysqld = MySQL Daemon

    * Là tiến trình chạy MySQL server
    * Chạy nền (background service)

## 4. Enable MySQL Service

```sh
sudo systemctl enable mysqld.service
```

* Ý nghĩa:
* Khi reboot server → MySQL tự động chạy

👉 Đây là cấu hình production bắt buộc

## 5. Start MySQL Service

```sh
sudo systemctl start mysqld.service
```

## 6. Kiểm tra trạng thái MySQL

```sh
systemctl status mysqld
```

* Kết quả mong đợi:
    * active (running)
    * Có PID (Process ID)
    * Có thông tin CPU / RAM usage

## 7. Kiểm tra package MySQL

```sh
rpm -qa | grep -i mysql
```

* Ý nghĩa:
    * Liệt kê tất cả package liên quan đến MySQL

    * Ví dụ:
        * mysql-server
        * mysql-client
        * mysql-common

## 8. Kiểm tra process MySQL

```sh
    pidof mysqld
```
* Ý nghĩa:
    * Lấy Process ID của MySQL

## 9. Kiểm tra port MySQL

```sh
netstat -ntlp | grep 3306
```

* Ý nghĩa:
    * Kiểm tra MySQL có đang listen port 3306 không

👉 Port mặc định của MySQL: 3306

## 10. Kiểm tra file MySQL đang mở

```sh
    sudo lsof -u mysql
```

* Ý nghĩa:
    * Liệt kê các file đang được MySQL sử dụng

## 11. Thư mục quan trọng của MySQL

#### Data directory:
```sh
/var/lib/mysql
```
* Chứa:
    * Database files
    * Table data
    * Index
#### Socket file:
```sh
    /var/run/mysqld/mysqld.sock
```
* Dùng để:
    * Kết nối local (localhost)
    * Root login không cần TCP

## 12. Quyền truy cập

* MySQL chạy dưới user: mysql
* Không thể truy cập file nếu không có quyền root