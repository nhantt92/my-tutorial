# Command shell MongoDB

## show dbs : hien thi cac database dang co
## use ten_db :  chuyen doi database dang co, neu khong co tao moi database
## db : xem hien dang chon su dung database nao
## db.dropDatabase() : xoa mot database dang chon
## db.createCollection("name_Collection") : tao moi mot collection moi
## db.createCollection("mycol", {capped: true, autoIndexID: true, size: 6142800, max: 1000}) : tao moi mot collection voi mot so option quan trong
## db.collection_name.drop() xoa 1 collection
## db.collection_name.insert({username: "nhantt", pass: "123456", status: true}) : insert 1 document
## var user = {}; user.username = "admin"; user.pass = "admin"; user.status = false;
 db.collection_name.save(user): insert save 1 document moi tu mot object

## db.collection_name.find() : truy van tat ca cac document khong co cau truc hien thi o trong collection
## db.collection_name.find().pretty() : truy van tat ca cac document hien thi co cau truc o collection
 
## export collection -> file.json:

 mongoexport --db ten_db --collection ten_collection --out  "PATH\ten.json"

 hoac

 mongoexport -d ten_db -c ten_collection -o "Path\ten.json"

## import collection from file.json

mongoimport -d ten_db -c ten_collection --file "PATH\file.json"

## export collection -> file.csv

mongoexport -d ten_db -c ten_collection --type=csv -o "PATH\ten_file.csv" -f id,user_name,password,skill,status

-f : dinh nghia cac field

## import collection from file.csv

mongoimport -d ten_db -c ten_collection --type=csv --file "PATH\ten_file.csv" --headerline

