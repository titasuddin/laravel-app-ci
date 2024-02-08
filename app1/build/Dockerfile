FROM php:8.2

RUN apt-get update -y && apt-get install -y openssl zip unzip git libonig-dev


RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer


RUN docker-php-ext-install pdo mbstring xmlrpc gd xml cli zip tokenizer json pear





# Set the working directory


WORKDIR /var/www/html


# Copy the application code


COPY app1/src .



RUN rm -rf vendor composer.lock
RUN composer install




CMD php artisan serve --host=0.0.0.0 --port=8081


EXPOSE 8081
