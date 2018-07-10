FROM ubuntu:16.04
MAINTAINER vuilendi@gmail.com

RUN apt-get update && apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install \
	apt-utils \
	nano \
	curl \
	lynx-cur \
	git \
	unzip \
	python \
	default-jre \
	build-essential \
	lsof \
	vsftpd
	
COPY vsftpd.conf /etc/vsftpd

RUN /etc/init.d/vsftpd restart

# Alway get new node
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y nodejs

# Create code folder
RUN mkdir -p /var/code

# Install gulp
RUN npm install --global gulp-cli \
	&& npm install pm2 -g

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*




# Expose apache.
EXPOSE 3000