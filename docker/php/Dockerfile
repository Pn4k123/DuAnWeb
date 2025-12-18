FROM php:8.4-apache

# 1. Cài đặt các thư viện hệ thống cần thiết
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    git \
    curl

# 2. Cài đặt PHP extensions cho Laravel & MySQL
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

# 3. Kích hoạt mod_rewrite của Apache (để chạy được các route của Laravel)
RUN a2enmod rewrite

# 4. Cài đặt Composer từ image chính thức
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# 5. Thiết lập thư mục làm việc
WORKDIR /var/www/html

# 6. COPY FILE CẤU HÌNH APACHE VÀO ĐÂY (Vị trí đúng)
# File này sẽ ghi đè cấu hình mặc định của Apache để trỏ vào thư mục /public
COPY ./docker/apache/vhost.conf /etc/apache2/sites-available/000-default.conf

# 7. Phân quyền (Tùy chọn nhưng nên có để tránh lỗi ghi file log/cache)
RUN chown -R www-data:www-data /var/www/html