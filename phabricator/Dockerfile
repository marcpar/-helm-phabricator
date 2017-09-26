FROM phusion/baseimage

RUN add-apt-repository -y ppa:ondrej/php
RUN apt-get update && apt-get install -y \
  mercurial \
  subversion \
  python-pygments \
  sendmail \
  imagemagick \
  git \
  wget \
  php7.1 \
  php7.1-cli \
  php7.1-mysql \
  php7.1-fpm \
  php7.1-dom \
  php7.1-ctype \
  php7.1-curl \
  php7.1-fpm \
  php7.1-gd \
  php7.1-intl \
  php7.1-json \
  php7.1-mbstring \
  php7.1-mcrypt \
  php7.1-mysqlnd \
  php7.1-opcache \
  php7.1-openssl \
  php7.1-pcntl \
  php7.1-pdo \
  php7.1-pdo_mysql \
  php7.1-posix \
  php7.1-session \
  php7.1-tidy \
  php7.1-xml \
  php7.1-zip \
  && rm -rf /var/lib/apt/lists/*
  
## change default port to port 24
RUN echo "" >> /etc/ssh/sshd_config
RUN echo "Port 24" >> /etc/ssh/sshd_config

RUN adduser phd --home /home/phd
RUN adduser phd sudo
RUN adduser git

RUN mkdir /srv/phd
RUN chown -R phd /srv/phd
RUN chown -R phd /var/log

COPY php.ini         /etc/php7.1/php.ini
COPY php-fpm.conf    /etc/php7.1/php-fpm.conf
COPY local.json      /local.json
COPY entrypoint.sh   /

USER phd

RUN git clone https://www.github.com/phacility/libphutil.git /srv/phd/libphutil
RUN git clone https://www.github.com/phacility/arcanist.git /srv/phd/arcanist
RUN git clone https://www.github.com/phacility/phabricator.git /srv/phd/phabricator
RUN git clone https://www.github.com/PHPOffice/PHPExcel.git /srv/phd/PHPExcel
ENV PATH=$PATH:/srv/phd/phabricator/bin

USER root
ATTACH ["/bin/bash"]

EXPOSE 9000

ENTRYPOINT ["/entrypoint.sh"]

TAG marcpar/phabricator
