FROM ubuntu:bionic

LABEL maintainer="Phil Kulin <schors@gmail.com>"

RUN groupadd -g 107 crontab \
        && apt-get update && apt-get install -q -y --no-install-recommends \
        git \
        cron \
        ca-certificates \
        openssl libengine-gost-openssl1.1 \
        locales \
        locales-all \
        && rm -f /etc/cron.d/* \
        && install -d /var/opt/gost-ca

WORKDIR /var/opt/gost-ca

RUN git clone https://github.com/schors/gost-russian-ca.git .

COPY old.certs /var/opt/old.certs
COPY cron_entrypoint.sh /entrypoint.sh
COPY crontab /etc/crontab

VOLUME /tmp

ENTRYPOINT ["/entrypoint.sh"]

CMD [ "/usr/sbin/cron", "-f", "-L", "15"]
