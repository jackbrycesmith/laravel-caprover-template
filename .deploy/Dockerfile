FROM php:7.4-fpm

# Set working directory
ENV LARAVEL_PATH=/srv/app
WORKDIR $LARAVEL_PATH

# Install system dependencies
RUN apt-get update && apt-get install -y build-essential cron curl locales zip unzip git

# Setup cron job
RUN (crontab -l ; echo "* * * * * /usr/local/bin/php /srv/app/artisan schedule:run >> /dev/null 2>&1") | crontab

# Install supervisord
COPY --from=ochinchina/supervisord:latest /usr/local/bin/supervisord /usr/local/bin/supervisord

# Install caddy
COPY --from=caddy:2.0.0 /usr/bin/caddy /usr/local/bin/caddy

# Install PHP extensions
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/
RUN install-php-extensions intl bcmath gd pdo_mysql pdo_pgsql opcache redis uuid exif pcntl zip
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install composer & app dependencies
COPY --from=composer:1.10.5 /usr/bin/composer /usr/local/bin/composer
COPY composer.json composer.json
COPY composer.lock composer.lock
# TODO remove prestissimo when composer hits v2
RUN composer global require hirak/prestissimo --no-plugins --no-scripts
RUN composer install --prefer-dist --no-scripts --no-dev --no-autoloader && rm -rf /root/.composer

# Copy app
COPY --chown=www-data:www-data . $LARAVEL_PATH/
COPY ./.deploy/config/php/local.ini /usr/local/etc/php/conf.d/local.ini
RUN chmod -R 775 $LARAVEL_PATH/storage

# Set any ENVs
ARG APP_KEY=${APP_KEY}
ARG APP_NAME=${APP_NAME}
ARG APP_URL=${APP_URL}
ARG APP_ENV=${APP_ENV}
ARG APP_DEBUG=${APP_DEBUG}

ARG LOG_CHANNEL=${LOG_CHANNEL}

ARG DB_CONNECTION=${DB_CONNECTION}
ARG DB_HOST=${DB_HOST}
ARG DB_PORT=${DB_PORT}
ARG DB_DATABASE=${DB_DATABASE}
ARG DB_USERNAME=${DB_USERNAME}
ARG DB_PASSWORD=${DB_PASSWORD}

ARG BROADCAST_DRIVER=${BROADCAST_DRIVER}
ARG CACHE_DRIVER=${CACHE_DRIVER}
ARG QUEUE_CONNECTION=${QUEUE_CONNECTION}
ARG SESSION_DRIVER=${SESSION_DRIVER}
ARG SESSION_LIFETIME=${SESSION_LIFETIME}

ARG REDIS_HOST=${REDIS_HOST}
ARG REDIS_PASSWORD=${REDIS_PASSWORD}
ARG REDIS_PORT=${REDIS_PORT}

ARG MAIL_MAILER=${MAIL_MAILER}
ARG MAIL_HOST=${MAIL_HOST}
ARG MAIL_PORT=${MAIL_PORT}
ARG MAIL_USERNAME=${MAIL_USERNAME}
ARG MAIL_PASSWORD=${MAIL_PASSWORD}
ARG MAIL_ENCRYPTION=${MAIL_ENCRYPTION}
ARG MAIL_FROM_ADDRESS=${MAIL_FROM_ADDRESS}
ARG MAIL_ENCRYPTION=${MAIL_ENCRYPTION}
ARG MAIL_FROM_NAME=${APP_NAME}

ARG PUSHER_APP_ID=${PUSHER_APP_ID}
ARG PUSHER_APP_KEY=${PUSHER_APP_KEY}
ARG PUSHER_APP_SECRET=${PUSHER_APP_SECRET}
ARG PUSHER_APP_CLUSTER=${PUSHER_APP_CLUSTER}

# Start app
EXPOSE 80
COPY ./.deploy/entrypoint.sh /
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/bin/bash", "/entrypoint.sh"]
