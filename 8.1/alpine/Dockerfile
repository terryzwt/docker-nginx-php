FROM tiredofit/nginx-php-fpm:alpine-8.1
ENV TIMEZONE=Asia/Shanghai
ENV VIRTUAL_PORT=80
ENV NGINX_WEBROOT=/var/www/html 
ENV CONTAINER_PROCESS_RUNAWAY_LIMIT=5
ENV LOGROTATE_COMPRESSION_TYPE=NONE
ENV LOGROTATE_RETAIN_DAYS=60
#ENV PHP_WEBROOT=docroot
ENV DRUSH_VERSION 8.4.11
ENV DRUSH_LAUCHER 0.10.1
ENV COLUMNS 0
ENV DRUSH_LAUNCHER_FALLBACK=/usr/local/bin/drush8
ENV NGINX_SITE_ENABLED=drupal
ENV CONTAINER_ENABLE_MONITORING=FALSE
ENV PHP_ENABLE_IMAGICK=TRUE
ENV PHP_MEMORY_LIMIT=1024M
ENV PHP_ENABLE_PGSQL=TRUE
ENV PHP_ENABLE_PDO_PGSQL=TRUE
ENV PHP_ENABLE_REDIS=TRUE
ENV PHP_ENABLE_MEMCACHED=TRUE
ENV PHP_ENABLE_BZ2=TRUE
ENV PHP_FPM_MAX_CHILDREN=300
ENV PHP_FPM_START_SERVERS=10
ENV PHP_FPM_MIN_SPARE_SERVERS=5
ENV PHP_FPM_MAX_SPARE_SERVERS=30
ENV NGINX_ENABLE_COMPRESSION_BROTLI=FALSE
ENV HTTP_HEADER_X_CONTENT_SECURITY_POLICY="default-src 'self' data: 'unsafe-inline' 'unsafe-eval' *.google.com *.baidu.com unpkg.com *.gstatic.com *.googleapis.com *.jsdelivr.net *.cloudflare.com d3js.org *.cookielaw.org *.youtube.com youtu.be *.youtu.be *.googleusercontent.com *.bootstrapcdn.com *.googletagmanager.com;"

RUN php-ext enable zip && \
    curl -fsSL -o /usr/local/bin/drush8 https://github.com/drush-ops/drush/releases/download/$DRUSH_VERSION/drush.phar | sh && \
    chmod +x /usr/local/bin/drush8 && \
    drush8 core-status && \
    ###### install drush laucher ######
    wget -O drush.phar https://github.com/drush-ops/drush-launcher/releases/download/$DRUSH_LAUCHER/drush.phar && \
    chmod +x drush.phar && \
    mv drush.phar /usr/local/bin/drush && \
    ##install composer
    php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer
ADD https://raw.githubusercontent.com/sparkpos/docker-nginx-php/master/conf/nginx/drupal.conf /etc/nginx/sites.available/drupal.conf
ADD https://raw.githubusercontent.com/sparkpos/docker-nginx-php/master/conf/nginx/laravel.conf /etc/nginx/sites.available/laravel.conf
ADD install /
WORKDIR /var/www/html
EXPOSE 80
