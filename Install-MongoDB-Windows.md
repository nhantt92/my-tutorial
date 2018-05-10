# Install MongoDB on Windows10

1. Download MongoDB Community Server
https://www.mongodb.com/download-center?_ga=2.127252933.955389107.1525826444-890511087.1525826444#production

2. Install 

Select Custom Change PATH install

C:\MongoDB\3.6\

3. mkdir C:\MongoDB\Data
	mkdir C:\MongoDB\Data\db

4. cd C:\MongoDB\Server\3.6\bin

	mongod --dbpatch C:\MongoDB\data

5. Test connect with app Robomongo

Close Command Line -> Exit Mongod

Muon chay lai server mongod phai thuc hien
ReOpen server Mongod: open command Line with administator 

cd C:\MongoDB\Server\3.6\bin
mongod --dbpath C:\MongoDB\data

6. Tao cau hinh de mo may len tu dong start server Mongo

6.1	Tao thu muc Log va mongod.log chua log khi chay 
	 mkdir C:\MongoDB\Log
	cd MongoDB\log	touch mongod.log
6.2 Toa file cau hinh mongod.cfg trong C:\MongoDB\Server
	Copy doan ma sau vao file mongod.cfg

systemLog:
    destination: file
    path: c:\MongoDB\data\log\mongod.log
storage:
    dbPath: c:\MongoDB\data\db

Save lai
7. Di vao thu muc C:\MongoDB\Server\3.6\bin
mongod --config "C:\MongoDB\Server\3.6\mongod.cfg" --install

8. Mo Command Line with administrator 

chay ngam MongoDB

net start MongoDB

server thong bao thanh cong
The MongoDB service is starting.
The MongoDB service was started successfully.

- Dung ROBOT3T kiem tra lai

De dung lai 

net stop MongoDB

dung server

9 Muon remove

C:\MongoDB\Server\3.6\bin
mongod --remove // Loai bo nhung phan config, mongo k chay nua

remove config

net start MongoDB se k chay


10. Muon chay lai phai chay config

mongod --config "C:\MongoDB\Server\3.6\mongod.cfg" --install

11. Khi vua khoi dong windows chay lun Mongo

msconfig vao service kiem tra xem co MongoDB chua

Chay lenh sau tren command Line with administrator
sc.exe create MongoDB binPath= "\"C:\MongoDB\Server\3.6\bin\mongod.exe\" --service --config=\"C:\MongoDB\Server\3.6\mongod.cfg\"" DisplayName= "MongoDB" start= "auto"

"[SC] CreateService SUCCESS" bao thanh cong

msconfig vao service kiem tra lai

net start MongoDB de chay server MongoDB

start thanh cong: [initandlisten] waiting for connections on port 27017

De stop MongoDB service:

net stop MongoDB

De remove MongoDB service:

sc.exe delete MongoDB
se khong chay tu dong nua

De start va Stop phai dung quyen administator