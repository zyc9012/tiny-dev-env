FROM alpine:3.5

ENV PGDATA=/var/lib/postgresql/data

RUN apk add --no-cache \
      s6 \
      su-exec \
      openssh \
      openssl \
      postgresql \
      nodejs && \
    mkdir -p /code && \
    mkdir -p $PGDATA && chmod 0755 $PGDATA && \
    mkdir -p /run/postgresql && chmod g+s /run/postgresql && \
    ssh-keygen -A && \
    rm -f /var/cache/apk/*

WORKDIR /code

COPY run.sh /usr/local/bin/run.sh
COPY s6.d /etc/s6.d
COPY index.js /code/index.js
COPY package.json /code/package.json

RUN chmod +x /usr/local/bin/run.sh /etc/s6.d/*/* /etc/s6.d/.s6-svscan/*

EXPOSE 8080

CMD ["run.sh"]
