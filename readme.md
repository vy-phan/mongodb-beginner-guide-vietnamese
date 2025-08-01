# MongoDB Database Tools - Hướng Dẫn Tải Và Sử Dụng Cơ Bản (Windows)

## 1. Giới thiệu

Bộ công cụ **MongoDB Database Tools** hỗ trợ thao tác với cơ sở dữ liệu MongoDB qua dòng lệnh.  
Các lệnh thường dùng gồm:
- **mongodump**: Sao lưu (backup) dữ liệu MongoDB
- **mongorestore**: Phục hồi (restore) dữ liệu từ file backup
- **mongoexport**: Xuất dữ liệu collection ra file CSV/JSON
- **mongoimport**: Nhập dữ liệu từ file CSV/JSON vào MongoDB

---

## 2. Hướng dẫn tải & cài đặt MongoDB Database Tools trên Windows

### Bước 1: Truy cập trang tải chính thức

- Vào link: [https://www.mongodb.com/try/download/database-tools](https://www.mongodb.com/try/download/database-tools)

### Bước 2: Lựa chọn phiên bản phù hợp

- Ở mục **Platform** chọn `Windows x86_64`
- Ở mục **Package** chọn `zip`
- Ấn **Download**

### Bước 3: Giải nén và sử dụng

- Sau khi tải về, giải nén file zip, bạn sẽ thấy các file như:  
  `mongodump.exe`, `mongorestore.exe`, `mongoexport.exe`, `mongoimport.exe`, v.v...
![ảnh minh họa cấu trúc thư mục ](./assets//Screenshot%202025-08-01%20174518.png)
- Bên trong thư mục Bin có  
![ảnh minh họa cấu trúc thư mục bin ](./assets//Screenshot%202025-08-01%20174537.png)


- Di chuyển thư mục giải nén (ví dụ: `C:\mongodb-database-tools\`) vào nơi bạn dễ thao tác.

### Bước 4: Thêm đường dẫn vào biến môi trường PATH (giúp chạy lệnh ở bất cứ đâu, tùy chọn)

1. Copy đường dẫn tới thư mục chứa các file `.exe` vừa giải nén (ví dụ: `C:\mongodb-database-tools\`)
2. Chuột phải **This PC** > **Properties** > **Advanced system settings**
3. Chọn **Environment Variables...**
4. Tại **System variables** tìm đến biến `Path` > ấn **Edit**
5. Ấn **New**, dán đường dẫn vừa copy vào, ấn **OK** để lưu lại.

## HOẶC XEM HƯỚNG DẪN VỚI :     

[Video hướng dẫn tải Mongo Database Tools ( docker setup )](https://youtu.be/C5WB0X8Udt8?si=Nl3Lq61cquGzJiso)

[Video hướng dẫn tải Mongo Database Tools Windown thuần ](https://youtu.be/7-R-f1WgMd0?si=-lExT9wjbCDo-SgO)




---

## 3. Các lệnh cơ bản thường dùng ( quan trọng )

### 3.1. Hướng dẫn lấy URI kết nối từ MongoDB Atlas

- Truy cập [https://cloud.mongodb.com/](https://cloud.mongodb.com/), đăng nhập vào tài khoản Atlas.
- Chọn **Project** chứa database cần thao tác.
- Ở bảng điều khiển bên trái, chọn **Database** > chọn **Connect** với cluster cần sử dụng.
- Chọn **Connect your application**.
- Copy dòng URI, ví dụ:

    ```
    mongodb+srv://<username>:<password>@cluster0.lsdffsafasss.mongodb.net/<databaseName>
    ```

- Thay `<username>`, `<password>` và `<databaseName>` bằng thông tin thực tế của bạn.
- Ví dụ:
  ```
  mongodb+srv://vyphandev:123456@cluster0.lsdffsafasss.mongodb.net/mydb
  ```


---




### 3.2. Backup (sao lưu) toàn bộ cơ sở dữ liệu

#### Lấy dữ liệu từ Mongo Atlas lưu về máy cục bộ trả các file .bson và .json 

```bash
mongodump --uri="mongodb+srv://username:password@cluster0.lsdffsafasss.mongodb.net/databasename" --out="D:\BackupMongo"
```

- Thay `<username>`, `<password>` và `<databaseName>` bằng thông tin thực tế của bạn.
- Sau khi chạy xong, thư mục `<D:\BackupMongo>` sẽ có dữ liệu backup.



#### Sau khi chạy thành công:

- Một thư mục (ở ví dụ trên là D:\BackupMongo) sẽ được tạo ra.

- Bên trong có thư mục con theo tên database, mỗi collection sẽ có file .bson và .json (metadata).
![ảnh minh họa](./assets/Screenshot%202025-08-01%20174341.png)

- CMD sẽ trả về log cho biết đã backup thành công các collection nào, số lượng bản ghi v.v...


---



### 3.3. Restore (khôi phục) dữ liệu từ backup

#### Ngược lại với 3.2 : gửi dữ liệu từ máy cục bộ đã sao lưu file trước đó gửi về cho Mongo Atlas 

```bash 
mongorestore --uri="mongodb+srv://username:password@cluster0.lsdffsafasss.mongodb.net/databasename" "D:\BackupMongo\databasename"
```

- Lệnh này sẽ phục hồi toàn bộ dữ liệu từ thư mục backup vào database tương ứng.

#### Sau khi chạy thành công:

- Toàn bộ dữ liệu trong thư mục backup sẽ được phục hồi vào database đã chỉ định (ghi đè lên dữ liệu cũ nếu cùng tên collection).

- CMD sẽ báo tổng số document đã xuất.




---
### 3.4. Xuất dữ liệu một collection ra file JSON

#### Lấy dữ liệu từ Mongo Atlas lưu về máy cục bộ trả file JSON 


```bash 
mongoexport --uri="mongodb+srv://username:password@cluster0.lsdffsafasss.mongodb.net/databasename" --collection=tenCollection --out="tenfile.json"
```

#### Sau khi chạy thành công:

- Một file tenfile.json sẽ được tạo ở thư mục hiện tại (hoặc theo đường dẫn bạn chỉ định).

- File này chứa toàn bộ dữ liệu collection dưới dạng JSON, mỗi document trên một dòng.

- CMD sẽ báo tổng số document đã xuất.





---
### 3.5. Nhập dữ liệu từ file JSON vào collection

#### Ngược lại với 3.4 : Lấy dữ liệu từ máy cục bộ với các file JSON để gửi dữ liệu tới Mongo Altas 

```bash 
mongoimport --uri="mongodb+srv://username:password@cluster0.lsdffsafasss.mongodb.net/databasename" --collection=tenCollection --file="tenfile.json"
```

#### Sau khi chạy thành công:

- Dữ liệu từ file tenfile.json sẽ được import vào collection tương ứng trong database chỉ định.

- Nếu collection chưa tồn tại, sẽ được tạo mới.

- CMD sẽ trả về log, thông báo số document đã nhập thành công, báo lỗi (nếu có dòng sai format).


# HƯỚNG DẪN IMPORT FILE ĐÃ BACKUP GỬI ĐẾN MONGO COMPASS 
[bài hướng dẫn tiếp theo ](./restore.md)