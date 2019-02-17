# Dockerfiles for Lucee application servers

**This is a FORK of the official LAS Lucee Docker images.**

## Lucee Base Images

Lucee provides a number of different base images for your Lucee project.

### Lucee 5.2

- [nginx + Tomcat 8.0.53-JRE8](./lucee-nginx/5.2/) &nbsp; &nbsp;
  [![docker pulls](https://img.shields.io/docker/pulls/dcepler/lucee52-nginx.svg?label=docker+pulls)](https://hub.docker.com/r/dcepler/lucee52-nginx/)
  [![](https://images.microbadger.com/badges/image/dcepler/lucee52-nginx.svg)](https://microbadger.com/images/dcepler/lucee52-nginx)
- [nginx + Tomcat 8.0.53-JRE8-slim](./lucee-nginx/5.2-slim/) &nbsp; &nbsp;
  [![docker pulls](https://img.shields.io/docker/pulls/dcepler/lucee52-nginx-slim.svg?label=docker+pulls)](https://hub.docker.com/r/dcepler/lucee52-nginx-slim/)
  [![](https://images.microbadger.com/badges/image/dcepler/lucee52-nginx-slim.svg)](https://microbadger.com/images/dcepler/lucee52-nginx-slim)
- [nginx + Tomcat 8.0.53-JRE8-alpine](./lucee-nginx/5.2-alpine/) &nbsp; &nbsp;
  [![docker pulls](https://img.shields.io/docker/pulls/dcepler/lucee52-nginx-alpine.svg?label=docker+pulls)](https://hub.docker.com/r/dcepler/lucee52-nginx-alpine/)
  [![](https://images.microbadger.com/badges/image/dcepler/lucee52-nginx-alpine.svg)](https://microbadger.com/images/dcepler/lucee52-nginx-alpine)
- [Tomcat 8.0.53-JRE8](./5.2/) &nbsp; &nbsp;
  [![docker pulls](https://img.shields.io/docker/pulls/dcepler/lucee52.svg?label=docker+pulls)](https://hub.docker.com/r/dcepler/lucee52/)
  [![](https://images.microbadger.com/badges/image/dcepler/lucee52.svg)](https://microbadger.com/images/dcepler/lucee52)
- [Tomcat 8.0.53-JRE8-slim](./5.2-slim/) &nbsp; &nbsp;
  [![docker pulls](https://img.shields.io/docker/pulls/dcepler/lucee52-slim.svg?label=docker+pulls)](https://hub.docker.com/r/dcepler/lucee52-slim/)
  [![](https://images.microbadger.com/badges/image/dcepler/lucee52-slim.svg)](https://microbadger.com/images/dcepler/lucee52-slim)
- [Tomcat 8.0.53-JRE8-alpine](./5.2-alpine/) &nbsp; &nbsp;
  [![docker pulls](https://img.shields.io/docker/pulls/dcepler/lucee52-alpine.svg?label=docker+pulls)](https://hub.docker.com/r/dcepler/lucee52-alpine/)
  [![](https://images.microbadger.com/badges/image/dcepler/lucee52-alpine.svg)](https://microbadger.com/images/dcepler/lucee52-alpine)

## Example Project Dockerfile

```
FROM dcepler/lucee52-nginx:latest

# NGINX configs
COPY config/nginx/ /etc/nginx/
# Lucee server configs
COPY config/lucee/ /opt/lucee/web/
# Deploy codebase to container
COPY www /var/www
```

## Features

### Java optimisation tweaks

- JVM is set to [use /dev/urandom as an entropy source for secure random numbers](http://support.run.pivotal.io/entries/59869725-Java-Web-Applications-Slow-Startup-or-Failing) to avoid blocking Tomcat on startup.

- Tomcat is configured to [skip the default scanning of Jar files on startup](http://www.gpickin.com/index.cfm/blog/how-to-get-your-tomcat-to-pounce-on-startup-not-crawl), significantly improving startup time.

### Optimised for single-site application

The default configuration serves a single application for any hostname on the listening port. Multiple applications can be supported by editing the `server.xml` in the Tomcat config.


## Contributing to this Project

The Lucee Dockerfiles project is maintained by the community. Chief protagonist is @modius ([Geoff Bowers](https://github.com/modius) of [Daemon](http://www.daemon.com.au)). Bug reports and pull requests are most welcome.

### Spinning things up locally

Using the [Daemon Docker Workbench](https://github.com/justincarter/docker-workbench) provided, or using your own Docker tooling.

These instructions assume you have the parent Workbench up and running:
```
git clone git@github.com:lucee/lucee-dockerfiles.git
cd lucee-dockerfiles
docker-compose up
```

Containers are forwarded onto the following addresses:
```
lucee45 -> $ open http://lucee-dockerfiles.192.168.99.100.nip.io:8045
lucee50 -> $ open http://lucee-dockerfiles.192.168.99.100.nip.io:8050
lucee51 -> $ open http://lucee-dockerfiles.192.168.99.100.nip.io:8051
lucee52 -> $ open http://lucee-dockerfiles.192.168.99.100.nip.io:8052
nginx45 -> $ open http://nginx45.192.168.99.100.nip.io
nginx50 -> $ open http://nginx50.192.168.99.100.nip.io
nginx51 -> $ open http://nginx51.192.168.99.100.nip.io
nginx52 -> $ open http://nginx52.192.168.99.100.nip.io
```

## License

The Docker files and config files are available under the [MIT License](LICENSE). The Lucee engine, Tomcat, NGINX and any other softwares are available under their respective licenses.
