FROM hypriot/rpi-alpine-scratch

MAINTAINER Roger Stark <rho.ajax@gmail.com>

RUN apk update \
    && apk add squid \
    && apk add curl \
    && rm -rf /var/cache/apk/*

COPY start-squid.sh /usr/local/bin/
ENTRYPOINT ["/usr/local/bin/start-squid.sh"]
