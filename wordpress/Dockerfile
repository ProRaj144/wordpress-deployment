
FROM wordpress:php8.3-fpm


WORKDIR /var/www/html


RUN apt-get update && apt-get install -y zip unzip git && rm -rf /var/lib/apt/lists/*

EXPOSE 9000
CMD ["php-fpm"]
