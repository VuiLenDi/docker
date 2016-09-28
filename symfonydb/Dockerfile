FROM mysql

COPY docker-entrypoint.sh /usr/local/bin/
COPY symfony_generic.sql /docker-entrypoint-initdb.d

ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 3306
CMD ["mysqld"]