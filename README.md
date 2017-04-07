# docker-test-fs-privileges

A test with Docker I did to see how I can change file permissions of files created by Docker.

## Problem

After installing the composer dependencies, the `vendor` folder will 
be created but it will be owned by root. This is the problem.

## Build

```bash
docker-compose up -d
```

This will setup the containers:

```
Creating dockertestfsprivileges_webserver_1
Creating dockertestfsprivileges_composer_1
```

Now install the composer dependencies:

```bash
docker-compose run --rm composer install
```

## Run

Open the container in your browser. You might consider applying this 
article: https://www.polderknowledge.nl/2017/02/16/docker-dns/

This makes it possible to browse to: 
http://dockertestfsprivileges_webserver_1.docker
