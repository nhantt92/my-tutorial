# Một số Command shell thao tác với MongoDB

1. **show dbs** : hiển thị các database đang có
2. **use ten_db** :  chuyển đổi database đang có, nếu không có tạo mới database
3. **db** : xem hiện đang chọn sử dụng database nào
4. **db.dropDatabase()** : xóa một database đang chọn
5. **db.createCollection("name_Collection")** : tạo mới một collection
6. **db.createCollection("mycol", {capped: true, autoIndexID: true, size: 6142800, max: 1000})** : tạo mới một collection với một số option quan trọng
7. **db.collection_name.drop()**: xóa một collection
8. **db.collection_name.insert({username: "nhantt", pass: "123456", status: true})** : insert một document
9. ```
    var user = {};
    user.username = "admin";
    user.pass = "admin";
    user.status = false;
  ```
 **db.collection_name.save(user)**: insert save một document mới từ một object

10. **db.collection_name.find()** : truy vấn tất cả các document không có cấu trúc hiển thị ở trong collection
11. **db.collection_name.find().pretty()** : truy vấn tất cả các document hiển thị có cấu trúc trong collection

12. **export collection -> file.json:**

 `mongoexport --db ten_db --collection ten_collection --out  "PATH\ten.json"`

 Hoặc

 `mongoexport -d ten_db -c ten_collection -o "Path\ten.json"``

13. **import collection from file.json:**

  `mongoimport -d ten_db -c ten_collection --file "PATH\file.json"`

14. **export collection -> file.csv:**

  `mongoexport -d ten_db -c ten_collection --type=csv -o "PATH\ten_file.csv" -f id,user_name,password,skill,status
  `

  -f : định nghĩa các field

15. **import collection from file.csv:**

  `mongoimport -d ten_db -c ten_collection --type=csv --file "PATH\ten_file.csv" --headerline`
