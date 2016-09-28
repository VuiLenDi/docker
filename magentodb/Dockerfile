FROM vuilendi/magentodb

COPY docker-entrypoint.sh /usr/local/bin/
COPY magentodb.sql /tmp/magentodb.sql

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["docker-entrypoint.sh"]