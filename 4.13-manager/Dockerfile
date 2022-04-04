# derived from https://github.com/hojak/docker_contao/tree/master/4.4-manager
FROM php:7.4-apache

LABEL version="0.1.4" \
	description="Docker Image for a contao installation version 4.13" \
	maintainer="Werner Joss <w.joss@lpc.de>"

# install the PHP extensions we need
# new for contao 4.13: libonig-dev
RUN set -ex; \
	\
	apt-get update; \
	apt-get install -y \
		libicu-dev \
		libjpeg-dev \
		libpng-dev \
		libgmp-dev \
		libmcrypt-dev \
		libxml2-dev \
		mysql-common \
		libbz2-dev \
		zlib1g-dev \
		libzip4 \
		libzip-dev \
		unzip \
		vim \
		libonig-dev \
		&& docker-php-ext-install zip \
    ; \
	apt-get clean; \
	rm -rf /var/lib/apt/lists/*; \
	\
	#	changes from contao 4.9 version:
	#	docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr; \
	#	does not work anymore ! 04/2022
	pecl install mcrypt; \
	ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/local/include/; \
	export CFLAGS="-I/usr/src/php" ;\
	docker-php-ext-configure gd --with-jpeg; \
	docker-php-ext-install pdo pdo_mysql gd mysqli gmp bcmath zip xmlwriter xmlreader iconv bz2 mbstring soap intl 
	
RUN a2enmod rewrite expires

RUN set -ex; \
	# set the correct document root
	perl -pi -e "s#/var/www/html#/var/www/html/web#" /etc/apache2/sites-available/000-default.conf ; \
	perl -pi -e "s#/var/www/html#/var/www/html/web#" /etc/apache2/sites-available/default-ssl.conf ;\
	# set php timezone
	echo "date.timezone = 'Europe/Berlin'\n" >> /usr/local/etc/php/php.ini

# add composer, might be needed
RUN set -ex; \	
	curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN set -ex; \
	mkdir /var/www/html/web ;\
	curl https://download.contao.org/contao-manager.phar -o /var/www/html/web/contao-manager.phar.php ;\
	chown -R www-data:www-data  /var/www/html
	 
VOLUME /var/www/html

CMD ["apache2-foreground"]
