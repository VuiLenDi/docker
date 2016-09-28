FROM vuilendi/magento
ENTRYPOINT []

# Expose apache.
EXPOSE 80
COPY apache2-foreground /usr/local/bin/

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# By default start up apache in the foreground, override with /bin/bash for interative.
CMD ["apache2-foreground"]