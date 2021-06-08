FROM alpine:3
LABEL maintainer "Juan Zurano <jgzurano@gmail.com>"

RUN apk add --no-cache libcrypto1.1 libssl1.1 libstdc++ openconnect tinyproxy

RUN apk add --no-cache \
    bash ca-certificates wget curl \
    bind-tools openssh-client openresolv openssl \
    nmap nmap-scripts

RUN apk add --no-cache --virtual .build-deps gcc make musl-dev \
    && cd /tmp && wget -q -O microsocks.tar.gz https://github.com/rofl0r/microsocks/archive/v1.0.1.tar.gz \
    && tar -xzvf microsocks.tar.gz \
    && cd microsocks-* \
    && make \
    && make install

COPY tinyproxy.conf /etc/tinyproxy.conf

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

EXPOSE 8888
EXPOSE 8889

ENTRYPOINT ["/entrypoint.sh"]
