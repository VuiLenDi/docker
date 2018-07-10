FROM ubuntu:16.04
MAINTAINER vuilendi@gmail.com

# Update some needed package
RUN apt-get update && apt-get -y upgrade \
	apt-utils \
	software-properties-common \	
	&& apt-get update \
	&& LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php \
	&& apt-get update
	
# Install postfix, that's required
RUN echo "postfix postfix/mailname string tranminh.vuilendi.com" | debconf-set-selections \
	&& echo "postfix postfix/main_mailer_type string 'Local Only'" | debconf-set-selections \
	&& DEBIAN_FRONTEND=noninteractive apt-get -y install \
	python-software-properties \
	nano \
	putty \
	apache2 \	
	php7.2 \
	php7.2-cli \
	php7.2-common \
	php7.2-gd \
	php7.2-mysql \	
	php7.2-curl \
	php7.2-intl \
	php7.2-xsl \
	php7.2-mbstring \
	php7.2-zip \
	php7.2-bcmath \
	php7.2-tidy \
	libapache2-mod-php7.2 \
	libapache2-modsecurity \
	libapache2-mod-evasive \
	gcc \
	g++ \
	make \
	curl \
	lynx-cur \
	git \
	unzip \
	python \
	wget
	
# Copy Owasp Security
RUN wget -O /tmp/master https://github.com/SpiderLabs/owasp-modsecurity-crs/tarball/master
RUN tar -xvf /tmp/master -C /tmp \
	&& cp /tmp/SpiderLabs-owasp-modsecurity-crs-56cad3a/modsecurity_crs_10_setup.conf.example /etc/modsecurity/modsecurity_crs_10_setup.conf \
	# Configure mod security
	&& cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf
	
COPY security.conf /etc/apache2/conf-available/security.conf

# Alway get new node
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs

# Install node gyp
RUN apt-get install -y node-gyp

# Enable apache mods.
RUN a2enmod php7.2 \
	&& a2enmod rewrite \
	&& a2enmod headers

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