FROM alpine
MAINTAINER Roger Stark <rho.ajax@gmail.com>

ENV DANTE_VER 1.4.1
ENV DANTE_URL https://www.inet.no/dante/files/dante-$DANTE_VER.tar.gz
ENV DANTE_MD5 68c2ce12119e12cea11a90c7a80efa8f
ENV DANTE_FILE dante.tar.gz
ENV DANTE_TEMP dante
ENV DANTE_DEPS build-base curl

RUN set -x \
    && apk update \
    && apk add $DANTE_DEPS

RUN mkdir $DANTE_TEMP \
    && cd $DANTE_TEMP \
    && curl -sSL $DANTE_URL -o $DANTE_FILE \
    # && echo "$DANTE_MD5 $DANTE_FILE" | md5sum -c \
    && tar xzf $DANTE_FILE \
    && cd dante-$DANTE_VER \
    && ac_cv_func_sched_setscheduler=no ./configure \
    && make install \
    && cd .. \
    && rm -rf $DANTE_TEMP

RUN apk del $DANTE_DEPS \
    && rm -rf /var/cache/apk/*

ADD sockd.conf /etc/sockd.conf

ENV CFGFILE /etc/sockd.conf
ENV PIDFILE /tmp/sockd.pid
ENV WORKERS 10

EXPOSE 1080

CMD sockd -f $CFGFILE -p $PIDFILE -N $WORKERS
