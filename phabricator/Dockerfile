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
  php7.0 \
  php7.0-mysql \
  && rm -rf /var/lib/apt/lists/*
  
## change default port to port 24
RUN echo "" >> /etc/ssh/sshd_config
RUN echo "Port 24" >> /etc/ssh/sshd_config

RUN adduser phd --home /home/phd
RUN adduser phd sudo
RUN adduser git

RUN mkdir /srv/phd
RUN chown -R phd /srv/phd

USER phd

RUN git clone https://www.github.com/phacility/libphutil.git /srv/phd/libphutil
RUN git clone https://www.github.com/phacility/arcanist.git /srv/phd/arcanist
RUN git clone https://www.github.com/phacility/phabricator.git /srv/phd/phabricator
RUN git clone https://www.github.com/PHPOffice/PHPExcel.git /srv/phd/PHPExcel
ENV PATH=$PATH:/srv/phd/phabricator/bin
ATTACH ["/bin/bash"]

TAG marcpar/phabricator
