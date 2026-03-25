## 1. Kiểm tra OS
SSH vào server, chạy lệnh

```sh
cat /etc/os-release
```

* File  /etc/os-release chứa :
    * Tên OS
    * Version
    * Base distro

* Amazon Linux 2023 KHÔNG phải Red Hat
* Nó:
    * Based on Fedora
    * Nhưng tương thích với Red Hat ecosystem

## 2. Vì sao phải quan tâm đến Red Hat?
* Vì MySQL không phát hành package riêng cho Amazon Linux
* Nó phát hành cho:
    * Red Hat Enterprise Linux (RHEL)

* Để cài MySQL, Bạn phải:
    * Xác định OS của mình
    * Tìm RHEL version tương thích
    * Dùng repo của RHEL đó

## 3. Mapping: Amazon Linux ↔ RHEL
* Amazon Linux 2023 → RHEL 9
* Nghĩa là:
    * Nếu bạn dùng Amazon Linux 2023
    * → Bạn phải dùng repo của RHEL 9

## 4. MySQL Repository là gì?
MySQL repo là:
    Nơi chứa package MySQL
    Dùng để:
        search
        install
        update

#### Quy trình chuẩn:

1. Download repo (file .rpm)

```sh
wget https://repo.mysql.com/mysql80-community-release-el9-5.noarch.rpm
```

2. Install repo vào hệ thống

```sh
sudo yum localinstall mysql80-community-release-el9-5.noarch.rpm
```

3. Tìm kiếm, xem thông tin package
```sh
sudo yum search mysql-community-server
```
```sh
sudo yum info mysql-community-server.x86_64
```

4. Dùng package manager để cài MySQL

## 5. Chọn đúng repo MySQL
* Bạn vào: [repo.mysql.com](http://url)

* Tìm repo phù hợp
    * Cần tìm MySQL 8.0 (community)
    * Dành cho Enterprise Linux 9

    * Bạn sẽ thấy nhiều file kiểu:
        * el7
        * el8
        * el9 ✅
        * 👉 Phải chọn:
        * el9 (Enterprise Linux 9)
        * Vd: mysql80-community-release-el9-5.noarch.rpm
            | Phần    | Ý nghĩa |
            |---------|---------|
            | mysql80 | MySQL 8.0 |
            | el9     | Enterprise Linux9 |
            | noarch  | No architecture, không phụ thuộc CPU (x86, ARM), dùng được cho mọi CPU |

## 6. Dependency Matching
* Database không chạy độc lập
    * Nó phụ thuộc vào:
        * OS
        * Library
        * Kernel

        👉 Sai version → lỗi ngay

* Junior thường: copy lệnh install trên mạng → chạy
* Senior DBA: kiểm tra OS → chọn đúng repo → rồi mới cài
## 7. Repository = nguồn sự thật
* Khi bạn cài repo:
    * Bạn không cần tải MySQL thủ công
    * Chỉ cần:

    ```sh
    dnf install mysql-server
    ```

    👉 System sẽ tự resolve dependency