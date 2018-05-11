# Một số Command shell thao tác với MongoDB

1. **show dbs** : hiển thị các database đang có
2. **use ten_db** :  chuyển đổi database đang có, nếu không có tạo mới database
3. **db** : xem hiện đang chọn sử dụng database nào
4. **db.dropDatabase()** : xóa một database đang chọn
5. **db.createCollection("name_Collection")** : tạo mới một collection
6. **db.createCollection("mycol", {capped: true, autoIndexID: true, size: 6142800, max: 1000})** : tạo mới một collection với một số option quan trọng
7. **db.collection_name.drop()**: xóa một collection
8. **db.collection_name.insert({username: "nhantt", pass: "123456", status: true})** : insert một document

9. Khai báo một Object

  ```
    var user = {};
    user.username = "admin";
    user.pass = "admin"
    user.status = false
  ```

 **db.collection_name.save(user)** : insert save một document mới từ một object

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

16. **Thêm một Document bằng javascript:**

  Tạo một tập tin javascript: name.js

  ex:

  ```
    db.users.insert({
        user_name: "nhantt",
        password: "123456",
        email: "nhantt@gmail.com",
        age: 26,
        skills: ["Node", "ReactJS", "MongoDB"],
        status: "active"
      });
  ```

  Sử dụng phương thức load:

  `load("C:/MongoDB/js/name.js")`

17. **Thêm một mảng document bằng jacvascript:**

  Tạo một tập tin javascript: name_array.js

  ex:

  ```
   var usersArray = [
    {
      user_name: "Ti",
      password: "1234568",
      email: "ti123@gmail.com",
      age: 26,
      skills: ["PHP", "AngularJS", "MySQL"],
      status: "active"
    },
    {
      user_name: "teo",
      password: "9876543",
      email: "teo@gmail.com",
      age: 20,
      skills: ["NodeJS", "ReactJS", "MySQL"],
      status: "disable"
    },
    {
      user_name: "tun",
      password: "123abc",
      email: "tun9x@gmail.com",
      age: 22,
      skills: ["ReactNative", "Node"],
      status: "active"
    }
   ];
  db.users.insert(usersArray);
  ```
  Sử dụng phương thức load

18. **Query và toán tử chiếu (Projection Operators)**

    Phép so sánh các loại dữ liệu trong BSON

    | Name | Description |
    |------| ----------- |
    | $eq  | so sánh bằng giá trị chỉ định |
    | $gt  | so sánh lớn hơn giá trị chỉ định |
    | $gte | so sánh >= giá trị chỉ định |
    | $in  | lấy phù hợp với bất kỳ giá trị nào trong mảng |
    | $lt  | so sánh nhỏ hơn giá trị chỉ định |
    | $lte | so sánh nhỏ hơn bằng giá trị chỉ định |
    | $ne  | lấy tất cả giá trị không bằng với giá trị chỉ định |
    | $nin | lấy các giá trị không có trong mảng chỉ định |

    Phép toán luận lý

    | Name | Mô tả |
    | -----| ------ |
    | $and | Ghép biểu thức truy vấn and |
    | $not | đảo giá trị biểu thức truy vấn |
    | $nor |             nor   |
    | $or  |          or |


19. **Update document**

  `db.collection_name.update(
    <query>,
    <update>,
    {
    upsert: <boolean>,
    multi: <boolean>,
    writeConcern: <document>
  })`

  Ex:

  `db.users.update({},{$set:{}})`
