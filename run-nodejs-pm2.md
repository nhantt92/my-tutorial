# PM2

## PM2 là ứng dụng Nodejs giúp quản lý tiến trình ứng dụng Nodejs trên môi trường sản phẩm (production). Nó giữ cho ứng dụng luôn luôn sống.

## Cài đặt pm2: `npm install pm2-g`

## Các lệnh cơ bản làm việc với pm2

* `pm2 start <name_app>` : khởi động app, <name_app> có thể là tên file khởi chạy ứng dụng hoặc id app xem bằng pm2 list

* `pm2 start <name_app>-i<number_cpu>`: number_cpu là số nhân cpu, để all thì sẽ start toàn bộ trên các nhân (hay còn gọi là cluster, load balance) tận dụng tối đa nhân xử lý

* `pm2 list` : liệt kê danh sách các ứng dụng đang khởi chạy.

* `pm2 restart <id_app>`: Khỏi động lại app dựa vào id của app, nếu để là pm2 restart all => khởi động lại toàn bộ app đang chạy

* `pm2 reload <id_app>`:  Nạp lại toàn bộ app dựa vào các thông số như của restart app

* `pm2 delete <id_app>`: delete app dựa theo id và nếu để là pm2 delete all => delete toàn bộ các app đang run

* `Pm2 describe <id_app>`: Xem thông tin chi tiết app đang chạy

* `pm2 monit`: hiển thị giao diện điều khiển xem chi tiết của tất cả các app

* `Pm2 logs`:
```
pm2 logs : hiển thị tất cả các lịch sử
pm2 logs api: hiển thị ra các api request dưới định dạng json (log có kết quả trả ra json)
pm2 flush : Xóa tất cả các log```

## Kịch bản khởi động tự động
  PM2 cung cấp 1 cách tự động để giữ cho các ứng dụng Node còn sống. PM2 sẵn có các kịch bản khởi động và cấu hình, nó đủ thông minh để lưu toàn bộ các danh sách ứng dụng và khởi chạy chúng khi hệ thống restart.

  * Chạy lệnh sau để PM2 sinh ra kịch bản khởi động trên hệ thống (chọn os bạn đang sử dụng tương ứng với các tham số)
          sudo pm2 startup [ubuntu|centos|gentoo|systemd]
Sau khi bạn đã start toàn bộ các ứng dụng Node lên, thì hãy chạy lệnh sau để đảm bảo chúng được chạy sau khi hệ thống khởi động lại.
                      sudo pm2 save
Đăng ký khởi động PM2 với hệ thống bằng lệnh sau:

        sudo -c "chmod +x /etc/init.d/pm2-init.sh; chkconfig --add pm2-init.sh"
Để đảm bảo PM2 được đăng ký khởi động thành công hãy dùng lệnh sau để kiểm tra
                               sudo chkconfig --list pm2-init.sh
