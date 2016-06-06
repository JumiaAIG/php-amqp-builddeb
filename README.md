# Buildtask for AMQP driver for PHP

Task to build Debian packages of AMQP driver for PHP.


## Dependencies

* librabbitmq1


## Usage

```sh
$ cd (version)
$ docker-compose build
$ docker-compose run --rm builder
$ ls -1 pkg/
```
