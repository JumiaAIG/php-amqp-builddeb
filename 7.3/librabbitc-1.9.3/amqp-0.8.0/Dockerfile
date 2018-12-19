FROM marceloalmeida/php-docker:7.2

MAINTAINER Marcelo Almeida <marcelo.almeida@jumia.com>

WORKDIR "/root"

ENV DEBIAN_FRONTEND noninteractive

# INSTALL BUILDER DEPENDENCIES
RUN apt-get update && apt-get install -y --no-install-recommends \
  apt-utils \
  build-essential \
  ca-certificates \
  checkinstall \
  libc6-dev \
  libssl-dev \
  lsb-release \
  make \
  git \
  php7.3-dev \
  re2c \
  runawk \
  wget

COPY src /src

# INSTALL PACKAGES DEPENDENCIES
ENV VERSION=1.9.3 \
    LIBRABBITC_VERSION=0.8.0


RUN mkdir /pkg
RUN apt-get install -y libcurl4-openssl-dev pkg-config && \
  wget --quiet https://github.com/alanxz/rabbitmq-c/releases/download/v${LIBRABBITC_VERSION}/rabbitmq-c-${LIBRABBITC_VERSION}.tar.gz && \
  tar -zxvf rabbitmq-c-${LIBRABBITC_VERSION}.tar.gz && \
  cd rabbitmq-c-${LIBRABBITC_VERSION} && \
  ./configure --prefix=/usr && \
  make && \
  make install

# CREATE PACKAGE
RUN git clone https://github.com/pdezwart/php-amqp.git /root/amqp-${VERSION} 
RUN cp -r /src/* /root/amqp-${VERSION}/. && \
  cd /root/amqp-${VERSION}/ && \
  phpize && \
  ./configure LIBS=/usr/lib/librabbitmq.so.4 ;\
  checkinstall -y --install=no --pkgname='php7.3-amqp' --pkgversion='$VERSION' --pkggroup='php' --pkgsource='https://github.com/pdezwart/php-amqp' --maintainer='Jumia TechOps \<techops@jumia.com\>' --requires='php7.3-common \(\>= 7.3.0\), librabbitmq1 \(\>= $LIBRABBITC_VERSION\)' --include=include_etc

#RUN wget -q https://pecl.php.net/get/amqp-${VERSION}.tgz && \
#  tar -zxvf amqp-${VERSION}.tgz && \
#  cd amqp-${VERSION} && \
#  cp -r /src/* /root/amqp-${VERSION}/. && \
#  phpize && \
#  ./configure LIBS=/usr/lib/librabbitmq.so.4 ;\
#  checkinstall -y --install=no --pkgname='php7.3-amqp' --pkgversion='$VERSION' --pkggroup='php' --pkgsource='https://github.com/pdezwart/php-amqp' --maintainer='Jumia TechOps \<techops@jumia.com\>' --requires='php7.3-common \(\>= 7.3.0\), librabbitmq1 \(\>= $LIBRABBITC_VERSION\)' --include=include_etc

VOLUME ["/pkg"]
