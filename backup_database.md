# Hướng dẫn Auto Backup database MongoDB

## File script save trong ổ Backup

  ```
  @echo off

  E:

  cd backup

  set filename=database %date% %time%
  set filename=%filename:/=-%
  set filename=%filename: =__%
  set filename=%filename:.=_%
  set filename=%filename::=-%

  echo Running backup "%filename"

  mongodump --db ph --out %filename%

  echo Running backup "%filename%/"
  "C:\Program Files\7-Zip\7z.exe" a -tzip "%filename%.zip" "%filename%"

  echo Deleting original backup directory "%filename%"
  rmdir "%filename%" /s /q

  echo BACKUP COMPLETE
  ```


## Schedule
  1. Mở Computer Management
  2. Chọn Task Scheduler và Create Ták
  3. Tab Gerneral lựa chọn run phù hợp yêu cầu
  4. Tab Triggers, chọn task run như thế nào: vd mỗi ngày vào lúc mấy giờ / lúc mở máy lên / login, ...
  5. Tab Actions, tạo action mới chọn đường dẫn tới script

## Restore
  Dùng các lệnh trong mongo shell để restore:

      mongorestore --gzip --db test
      mongorestore --archive=test.20150715.archive --db test
