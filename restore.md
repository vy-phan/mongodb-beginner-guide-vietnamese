# Hướng Dẫn Cài Đặt MongoDB Compass & MongoDB Community Server 
# => Để Import Dữ Liệu vào Mongo trên Local ( Mongo Compass ) hay vì Mongo Atlas

## 1. Mục tiêu

- Cài đặt **MongoDB Compass** để quản lý, xem, chỉnh sửa dữ liệu database local một cách trực quan.
- Cài đặt **MongoDB Community Server** để tạo và chạy MongoDB local, đồng thời có thể dùng lệnh import dữ liệu từ file có sẵn (file JSON hoặc file backup dạng BSON) .
- Sau khi hoàn thành, bạn có thể phục hồi data từ file có sẵn vào database local rồi mở bằng Compass.

## YÊU CẦU CẦN CÓ ĐỦ **MongoDB Compass** VÀ **MongoDB Community Server** VÀ **MongoDB Database Tools**

---

## 2. Tải và cài đặt MongoDB Compass

### 2.1. Tải Compass

- Truy cập: [https://www.mongodb.com/try/download/compass](https://www.mongodb.com/try/download/compass)
- Chọn bản phù hợp với hệ điều hành của bạn (thường là **Windows x64**).
- Tải về và chạy file cài đặt (`.exe`), bấm Next liên tục để cài đặt mặc định.

### 2.2. Mở MongoDB Compass

- Sau khi cài xong, mở ứng dụng **MongoDB Compass**.
- Để kết nối với server local mặc định, điền:
    ```
    mongodb://localhost:27017
    ```
  rồi bấm **Connect**.

---

## 3. Tải và cài đặt MongoDB Community Server

### 3.1. Tải Community Server

- Truy cập: [https://www.mongodb.com/try/download/community](https://www.mongodb.com/try/download/community)
- Chọn hệ điều hành **Windows**, Package là **MSI**.
- Tải về và chạy file cài đặt (`.msi`), chọn **Complete** hoặc **Custom** (nếu muốn thay đổi đường dẫn cài đặt).
- Để mặc định tất cả, nhấn **Next** liên tục đến khi cài xong.

### 3.2. Kiểm tra đã cài đặt thành công

- Mở **Command Prompt (CMD)**, gõ:
    ```bash
    mongod --version
    ```
- Nếu hiển thị ra phiên bản, bạn đã cài thành công.
- Nếu không hiển thị mặc dù đẫ tải thành công . Hãy tìm tới thư mục lưu MongoDB Community Server thường sẽ là : 
    ```bash 
    C:\Program Files\MongoDB\Server\6.0\bin
    ```
    
Tùy chỉnh dựa theo của bạn . Sau đó mở cmd gõ 
    ```bash 
    cd C:\Program Files\MongoDB\Server\8.0\bin>
    ```

Sau đó 
    ```bash
    mongod --version
    ```

### 3.3. Đảm bảo MongoDB server đã chạy

- Thường sau khi cài, MongoDB sẽ tự động chạy dưới dạng Windows Service.
- Để kiểm tra:
    - Nhấn `Windows + R`, gõ `services.msc`, Enter.
    - Tìm dòng **MongoDB Server** → trạng thái **Running**.
    - Nếu chưa chạy, chuột phải chọn **Start**.

---

## 4. Import dữ liệu vào MongoDB local

### 4.1. Trường hợp **import file JSON** (1 collection)

- Mở **MongoDB Compass**, connect với `mongodb://localhost:27017`
- Tạo database/collection mới (nếu chưa có)
- Vào collection cần import → bấm **Add Data** → **Import File**
- Chọn file `.json` và định dạng là JSON
- Nhấn **Import**, dữ liệu sẽ xuất hiện trong collection

### 4.2. Trường hợp **import file backup BSON** (nhiều collection, nhiều database) ( THƯỜNG DÙNG )

- Mở **Command Prompt của mongodb-database-tools-windows-x86_64-100.12.2/bin**, chạy lệnh:
    ```bash
    mongorestore --uri="mongodb://localhost:27017/tendatabase" "D:\BackupMongo\tendatabase"
    ```
    ![Vào đúng terminal đường dẫn tới mongodb-database-tools-windows-x86_64-100.12.2/bin ](./assets/Screenshot%202025-08-01%20191001.png)

    - Thay `tendatabase` và đường dẫn cho đúng tên database/folder backup của bạn.
    ![Tạo conntect mới và đặt tên trên Compass](./assets/Screenshot%202025-08-01%20191028.png)

- Sau khi chạy xong, mở lại Compass → F5 sẽ thấy database và các collection với đầy đủ dữ liệu đã phục hồi.

    ![F5 lại đúng cái Database và hiển thị ra được cơ sở dữ liệu như hình ](./assets/Screenshot%202025-08-01%20191055.png)



---

## 5. Một số lệnh cơ bản

- Kiểm tra phiên bản:
    ```bash
    mongod --version
    mongo --version
    ```
- Restore database từ backup:
    ```bash
    mongorestore --uri="mongodb://localhost:27017/tendatabase" "D:\BackupMongo\tendatabase"
    ```

---

## 6. Tài liệu tham khảo

- [Tải MongoDB Community Server](https://www.mongodb.com/try/download/community)
- [Tải MongoDB Compass](https://www.mongodb.com/try/download/compass)
- [Import/Export Data — MongoDB Docs](https://www.mongodb.com/docs/manual/core/import-export/)

---