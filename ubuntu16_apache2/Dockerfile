FROM ubuntu
MAINTAINER minh.tran@harveynash.vn

# Setup apache2
RUN apt-get update && apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install \
	apache2 \
	php7.0 \
	php7.0-common \
	php7.0-gd \
	php7.0-mysql \
	php7.0-mcrypt \
	php7.0-curl \
	php7.0-intl \
	php7.0-xsl \
	php7.0-mbstring \
	php7.0-zip \
	php7.0-bcmath \
	php7.0-iconv \
	libapache2-mod-php7.0 \
	curl \
	lynx-cur \
	git \
	unzip \
	npm
	
	
# Enable apache mods.
RUN a2enmod php7.0
RUN a2enmod rewrite

COPY info.php /var/www/html

# Update composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install gulp
RUN npm install --global gulp-cli

# node and nodejs
RUN ln -s /usr/bin/nodejs /usr/bin/node

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

# Expose apache.
EXPOSE 80

COPY apache2-foreground /usr/local/bin/

# By default start up apache in the foreground, override with /bin/bash for interative.
CMD ["apache2-foreground"]