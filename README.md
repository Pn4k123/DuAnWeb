🚀 Hướng dẫn cài đặt cho Developer
Dưới đây là các bước để thiết lập môi trường phát triển cục bộ (local development environment) sử dụng Docker.

📋 Yêu cầu hệ thống
Trước khi bắt đầu, hãy đảm bảo máy tính của bạn đã cài đặt:

Git

Docker & Docker Compose

🛠 Các bước cài đặt
1. Clone project từ repository Mở terminal và chạy lệnh:

git clone <url_repo>
cd <ten_thu_muc_project>

2. Cấu hình môi trường (.env) Tạo file môi trường từ file mẫu. Đừng quên mở file .env ra để chỉnh sửa các thông số Database (DB_HOST, DB_PASSWORD,...) cho phù hợp nếu cần thiết.

cp backend/.env.example backend/.env

3. Khởi động Docker Containers Lệnh này sẽ build image và chạy các container (PHP, MySQL, Nginx...) ở chế độ chạy ngầm (detached mode).

docker compose up -d --build

4. Cài đặt các thư viện PHP (Composer) Chạy composer install bên trong container của Laravel để cài đặt các package cần thiết.

docker exec -it laravel_app composer install

5. Tạo Application Key Lệnh này giúp bảo mật ứng dụng bằng cách tạo một chuỗi mã hóa trong file .env.

docker exec -it laravel_app php artisan key:generate

6. Chạy Migration (Khởi tạo Database) Tạo các bảng dữ liệu cần thiết cho ứng dụng.

docker exec -it laravel_app php artisan migrate
💡 Lưu ý
Nếu bạn muốn chạy thêm dữ liệu mẫu, có thể sử dụng lệnh: docker exec -it laravel_app php artisan db:seed

Ứng dụng mặc định thường sẽ chạy tại: http://localhost:8000 (hoặc port bạn đã cấu hình).
