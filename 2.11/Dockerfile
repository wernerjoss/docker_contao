FROM php:5.4-apache

LABEL version="0.1.0" \
	description="Docker Image for a contao installation version 2.11.17" \
	maintainer="Werner Joss <w.joss@lpc.de>"
	
# Build command:
# docker build -t contao-2.11:latest .	

# install the PHP extensions we need
RUN set -ex; \
	\
	apt-get update; \
	apt-get install -y \
		libicu-dev \
		libjpeg-dev \
		libpng-dev \
		libgmp-dev \
		libxml2-dev \
		mysql-common \
		libbz2-dev \
		zlib1g-dev \
		vim \
		nano \
		mmv \
	; \
	apt-get clean; \
	rm -rf /var/lib/apt/lists/*; \
	\
	ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/local/include/; \
	export CFLAGS="-I/usr/src/php" ;\
	docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr; \
	docker-php-ext-install pdo pdo_mysql gd mysqli gmp bcmath zip xmlwriter xmlreader iconv bz2 mbstring soap intl

RUN a2enmod rewrite expires

ENV VERSION 2.11.17

RUN set -ex; \
	curl -o contao.tar.gz -fSL "https://github.com/wernerjoss/docker_contao/raw/master/2.11/contao-2.11.17.tar.gz"
	
RUN set -ex; \
	tar -xzf contao.tar.gz -C /var/www/html; \
	rm contao.tar.gz; \
	chown -R www-data:www-data /var/www/html; \
	mv /var/www/html/contao-${VERSION}/* /var/www/html/; \
	mv /var/www/html/contao-${VERSION}/.htaccess* /var/www/html/; # hier muss das \	weg, da letzter Befehl in RUN 03.11.20 WJ
	
    # enable url rewriting - NO !
	# cp -p /var/www/html/.htaccess.default .htaccess; \	

VOLUME /var/www/html

CMD ["apache2-foreground"]
