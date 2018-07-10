FROM ubuntu:16.04
MAINTAINER minh.tran@nashtechglobal.com

# Setup apache2
RUN apt-get update && apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install \
	apt-utils \
	software-properties-common \
	&& LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php \
	&& apt-get update && apt-get -y install \
	nano \
	apache2 \
	
	php5.6 \
	php5.6-common \
	php5.6-gd \
	php5.6-mysql \
	php5.6-mcrypt \
	php5.6-curl \
	php5.6-intl \
	php5.6-xsl \
	php5.6-mbstring \
	php5.6-zip \
	php5.6-bcmath \
	php5.6-iconv \
	php5.6-tidy \
	libapache2-mod-php5.6 \
		
	curl \
	lynx-cur \
	git \
	unzip \
	python
	
# Alway get new node
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y nodejs

# Install bower
RUN npm install -g bower
	
# Enable apache mods.
RUN a2enmod php5.6 \
	&& a2enmod rewrite

COPY info.php /var/www/html

# Update composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
	# Install gulp
	&& npm install --global gulp-cli

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data \
	APACHE_RUN_GROUP www-data \
	APACHE_LOG_DIR /var/log/apache2 \
	APACHE_LOCK_DIR /var/lock/apache2 \
	APACHE_PID_FILE /var/run/apache2.pid

# Expose apache.
EXPOSE 80

COPY apache2-foreground /usr/local/bin/

# By default start up apache in the foreground, override with /bin/bash for interative.
CMD ["apache2-foreground"]