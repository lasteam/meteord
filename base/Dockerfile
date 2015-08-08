FROM debian:wheezy
MAINTAINER MeteorHacks Pvt Ltd.

ENV METEORD_DIR /opt/meteord
ENV PHANTOMJS_VERSION 1.9.7
COPY scripts $METEORD_DIR

RUN bash $METEORD_DIR/init.sh

# Install phantomjs for spiderable.
RUN \
  apt-get update && \
  apt-get upgrade -y && \
  apt-get install -y git wget libfreetype6 libfontconfig && \
  mkdir -p /srv/var && \
  wget -q --no-check-certificate -O /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 && \
  tar -xjf /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 -C /tmp && \
  rm -f /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 && \
  mv /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64/ /srv/var/phantomjs && \
  ln -s /srv/var/phantomjs/bin/phantomjs /usr/bin/phantomjs && \
  apt-get autoremove -y && \
  apt-get clean all


EXPOSE 80
ENTRYPOINT bash $METEORD_DIR/run_app.sh
