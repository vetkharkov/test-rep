FROM php:7.4-fpm

# Set working directory
WORKDIR /var/www

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    curl \
    nano \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip

RUN apt-get install -y cron && \
	apt-get install -y supervisor

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Add user for laravel application
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

# Copy existing application directory contents
COPY . /var/www

RUN (crontab -l ; echo "* * * * * /usr/bin/php /var/www/artisan schedule:run >>/dev/null 2>&1") | crontab

# Copy existing application directory permissions
#COPY --chown=www:www . /var/www
COPY . /var/www
RUN chown -R www:www /var/www

# Expose port 9000 and start php-fpm server
EXPOSE 9000
#CMD ["php-fpm"]
CMD  service supervisor start; php-fpm
