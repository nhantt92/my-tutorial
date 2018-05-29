# Install MongoDB on Ubuntu 16.04

## Add MongoDB vào Repository

        sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927

    Sau khi chạy xong sẽ hiển thị:

    ```
    Output
    gpg: Total number processed: 1
    gpg:               imported: 1  (RSA: 1)```

    Tiếp theo, thêm các chi tiết về MongoDB cho reposity để apt biết nơi tải xuống

        echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list

    Cập nhật lại danh sách các packages

        sudo apt-get update

## Cài đặt và xác nhận MongoDB

        sudo apt-get install -y mongodb-org

    Start MongoDB với systemctl

        sudo systemctl start mongod

    Kiểm tra xem dịch vụ Mongo chạy đúng chưa

        sudo systemctl status mongod

    ```
    Output
● mongodb.service - High-performance, schema-free document-oriented database
   Loaded: loaded (/etc/systemd/system/mongodb.service; enabled; vendor preset: enabled)
   Active: active (running) since Mon 2016-04-25 14:57:20 EDT; 1min 30s ago
 Main PID: 4093 (mongod)
    Tasks: 16 (limit: 512)
   Memory: 47.1M
      CPU: 1.224s
   CGroup: /system.slice/mongodb.service
           └─4093 /usr/bin/mongod --quiet --config /etc/mongod.conf```

    Kích hoạt tự động khởi động MongoDB khi hệ thống khởi động

        sudo systemctl enable mongod
    
    Quản lý MongoDB service bằng các lệnh sau:

        sudo systemctl stop mongod
        sudo systemctl start mongod

## Điều chỉnh Firewall 
    
    nếu MongoDB server không truy cập được từ internet cần điều chỉnh Firewall

    nếu sử dụng MongoDB chỉ ở local với các ứng dụng chạy cùng local, thì thiết lập firewall này an toàn.

    nếu muốn kết nối MongoDB server từ xa qua internet, chúng ta phải cho phép các kết nối đến trong ufw

    Để cho phép truy câp MongoDB trên cổng mặc định 27017 từ mọi nơi:

        ```sudo ufw allow 27017```
        Tuy nhiên cho phép này sẽ mặc định cho phép truy cập không giới hạn vào toàn bộ database server.

    Trong một số trường hợp, MongoDB chỉ nên được tuỷ cập từ các vị trí tin cậy nhất đinh, chẳng hạng như một server khác lưu trữ ứng dụng. Để thực hiện tác vụ này, có thế cho phép truy cập vào cổng mặc định của MongoDB trong khi chỉ định địa chỉ IP của một server khác được cho phép kết nối một cách rõ ràng.

        `sudo ufw allow from your_other_server_ip/32 to any port 27017`

    có thể xem status trong firewall

        `sudo ufw status`



