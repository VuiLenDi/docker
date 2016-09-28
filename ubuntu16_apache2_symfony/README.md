# Ubuntu 16 - Apache2 - Symfony
This project build environment for Symfony project. This will build based on ubuntu 16 (16.04 latest version when building)

# Detail

Build from ubuntu images latest:

	FROM ubuntu

Setup apache2 and php7.0 with some depended library:

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
		lynx-cur

Enable apache mod

	RUN a2enmod php7.0
	RUN a2enmod rewrite

Make dir for web and logs

	RUN mkdir /var/www/html/web
	RUN mkdir /var/www/html/logs

We will copy content of generic-symfony.conf to 000-default.conf

	ADD ./generic-symfony.conf /etc/apache2/sites-available/000-default.conf

Copy info.php for testing purpose
	
	COPY info.php /var/www/html/web

Manually set up the apache environment variables

	ENV APACHE_RUN_USER www-data
	ENV APACHE_RUN_GROUP www-data
	ENV APACHE_LOG_DIR /var/log/apache2
	ENV APACHE_LOCK_DIR /var/lock/apache2
	ENV APACHE_PID_FILE /var/run/apache2.pid

Expose apache.

	EXPOSE 80

By default start up apache in the foreground, override with /bin/bash for interative.

	CMD /usr/sbin/apache2ctl -D FOREGROUND

