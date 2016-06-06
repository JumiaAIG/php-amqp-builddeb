FROM php:7.0.7-cli

MAINTAINER Marcelo Almeida <marcelo.almeida@jumia.com>

WORKDIR "/root"

ENV DEBIAN_FRONTEND noninteractive
ENV VERSION 1.7.0

# INSTALL BUILDER DEPENDENCIES
RUN apt-get update && apt-get install -y --no-install-recommends \
  apt-utils \
  build-essential \
  checkinstall \
  lsb-release \
  make \
  wget

COPY src /src

# INSTALL PACKAGES DEPENDENCIES
RUN mkdir /pkg
RUN apt-get install -y librabbitmq-dev librabbitmq1

# CREATE PACKAGE
RUN pecl download amqp ;\
  tar -zxvf amqp-$VERSION.tgz ;\
  cd amqp-$VERSION ;\
  cp -r /src/* /root/amqp-$VERSION/. ;\
  phpize ;\
  ./configure ;\
  checkinstall -y --install=no --pkgname='php7.0-amqp' --pkgversion='$VERSION-aig' --pkggroup='php' --pkgsource='https://github.com/pdezwart/php-amqp' --maintainer='Marcelo Almeida \<marcelo.almeida@jumia.com\>' --requires='php7.0-common \(\>= 7.0.7\), librabbitmq1 \(\>= 0.5.2\)' --include=include_etc

VOLUME ["/pkg"]
