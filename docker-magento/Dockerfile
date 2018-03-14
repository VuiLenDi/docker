FROM vuilendi/ubuntu16_apache2
MAINTAINER minh.tran@nashtechglobal.com


RUN apt-get update && apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install \
	nano \
	wget \
	php-imagick
	
# RUN git config --global http.proxy 'socks5://127.0.0.1:12345'
# RUN git config --global https.proxy 'socks5://127.0.0.1:12345'

# Use composer to download new source code of magento
COPY auth.json /root/.composer/

WORKDIR /var/www/html

RUN rm -fr *

RUN composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .

RUN rm ~/.composer/auth.json

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*