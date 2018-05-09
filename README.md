# Buildtask for AMQP driver for PHP

[![Build Status](https://travis-ci.org/marceloalmeida/php-amqp-builddeb.svg?branch=master)](https://travis-ci.org/marceloalmeida/php-amqp-builddeb)

Task to build Debian packages of AMQP driver for PHP.


## Dependencies

* [librabbitmq1](https://github.com/marceloalmeida/librabbitmq1-builddeb/releases)



## Usage

```sh
$ cd (version)
$ docker-compose build
$ docker-compose run --rm builder
$ ls -1 pkg/
```
