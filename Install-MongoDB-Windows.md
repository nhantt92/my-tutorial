# Install MongoDB trên Windows10

1. Download MongoDB Community Server
	Vào CLI gõ lệnh

	`wmic os get caption`

	`wmic os get osarchitecture`

	để kiểm tra phiên bản hệ điều hành đang sử dụng

	Vào Link sau download bản cài đặt MongoDB Community Server
[MongoDB](https://www.mongodb.com/download-center?_ga=2.127252933.955389107.1525826444-890511087.1525826444#production)

2. Install

	Select Custom Change PATH install

	` C:\MongoDB\3.6\ `

3. Tạo các thư mục mới lưu trữ database

	`mkdir C:\MongoDB\Data`

	`mkdir C:\MongoDB\Data\db`


4. Vào đường dẫn cài đặt mongodb

	`cd C:\MongoDB\Server\3.6\bin`

	Chạy lệnh sau để run mongo Server

	`mongod --dbpatch C:\MongoDB\data`

5. Test connect with app Robomongo

	>Note: Đóng Command Line Mongod sẽ stop

	Muốn chạy lại server mongod phải thực hiện
mở lại server Mongod:

	Mở command Line quyền administator

	Đi vào thư mục cài đặt Mongo

	`cd C:\MongoDB\Server\3.6\bin`

	Chạy lệnh:

	`mongod --dbpath C:\MongoDB\data`

6. Tạo cấu hình để mở máy lên tự động start server Mongo

	* Tạo thư mục Log và mongod.log lưu log khi chạy:

	 `mkdir C:\MongoDB\Log`

	 `cd MongoDB\log	touch mongod.log`

 	* Tạo file cấu hình mongod.cfg theo đường dẫn

		`C:\MongoDB\Server`

	 **Copy đoạn mã sau vào file mongod.cfg**

	 ```
		systemLog:
    		destination: file
    		path: c:\MongoDB\data\log\mongod.log
		storage:
    		dbPath: c:\MongoDB\data\db```

	Save lại

7. Đi vào thư mục:

 `cd C:\MongoDB\Server\3.6\bin`

 Chạy lệnh:

	`mongod --config "C:\MongoDB\Server\3.6\mongod.cfg" --install`

	để install config

8. Mở Command Line quyền administrator

	chạy ngầm MongoDB

	`net start MongoDB`

	Cli hiện thông báo

	>The MongoDB service is starting.
	The MongoDB service was started successfully.

	Server start thành công

	Dùng ROBOT3T kiểm tra kết nối

	**Để stop server MongoDB** chạy lệnh

	`net stop MongoDB`

	server stop

9. Remove không chạy serverss

	`C:\MongoDB\Server\3.6\bin
mongod --remove`

	Loại bỏ những phần config, remove config, `net start MongoDB` sẽ không start được MongoDB

	Muốn start lại Mông phải config lại

	`mongod --config "C:\MongoDB\Server\3.6\mongod.cfg" --install`

10. Cấu hình khi vừa khởi động windows chạy luôn MongoDBs

	Start -> run -> gõ msconfig vào service kiểm tra xem có MongoDB chưa?

	Chạy lệnh sau trên Command Line quyền administrator:

	`sc.exe create MongoDB binPath= "\"C:\MongoDB\Server\3.6\bin\mongod.exe\" --service --config=\"C:\MongoDB\Server\3.6\mongod.cfg\"" DisplayName= "MongoDB" start= "auto"``

	CLI thông báo:

	[SC] CreateService SUCCESS

	Start-> Run -> gõ msconfig vào service kiểm tra lại

	`net start MongoDB` để chạy server MongoDB

	CLI thông báo:

		[initandlisten] waiting for connections on port 27017

	start thành công

	Để stop MongoDB service:

	`net stop MongoDB`

	Để remove MongoDB service:

	`sc.exe delete MongoDB`

	MongoDB sẽ không chạy tự động nữa

>Note: Để start và stop Mongo phải chạy với quyền administator
