FROM vuilendi/ubuntu16_nodejs
MAINTAINER vuilendi@gmail.com

WORKDIR /var/code

# Setup socketcluster FW
RUN npm install -g socketcluster \
	&& socketcluster create socketcluster

# Expose Port.
EXPOSE 3001
EXPOSE 3002