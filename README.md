# docker-desktop-vnc-knime

*******************************

*THIS REPO IS DEPRECATED, PLEASE CHECK HERE:*
https://github.com/elestio-examples/knime

*******************************

docker-desktop-vnc-knime is a Docker image to provide web VNC interface to KNIME

<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=2 orderedList=false} -->

<!-- code_chunk_output -->

- [Quick Start](#quick-start)
- [VNC Viewer](#vnc-viewer)
- [HTTP Base Authentication](#http-base-authentication)
- [SSL](#ssl)
- [Screen Resolution](#screen-resolution)
- [Default Desktop User](#default-desktop-user)

<!-- /code_chunk_output -->

## Quick Start

Run the docker container and access with port `6080`

```shell
docker run -p 6080:80 -v /dev/shm:/dev/shm -v ${PWD}/storage:/root elestio/docker-desktop-vnc
```

Browse http://your_ip:6080/

<img src="https://raw.githubusercontent.com/elestio/docker-desktop-vnc/main/screenshots/lxde.png" width=700/>


## Persistence

user profile: /root
Knime app: /opt/knime


## VNC Viewer

Forward VNC service port 5900 to host by

```shell
<<<<<<< HEAD
docker run -p 6080:80 -p 5900:5900 -v /dev/shm:/dev/shm -v ${PWD}/storage:/root elestio/docker-desktop-vnc
=======
docker run -p 6080:80 -p 5900:5900 -v /dev/shm:/dev/shm -v ${PWD}/knime-workspace:/root/knime-workspace elestio/docker-desktop-vnc-knime
>>>>>>> f6590a4ff663a626c31b70f8348638bad227a87c
```

Now, open the vnc viewer and connect to port 5900. If you would like to protect vnc service by password, set environment variable `VNC_PASSWORD`, for example

```shell
<<<<<<< HEAD
docker run -p 6080:80 -p 5900:5900 -e VNC_PASSWORD=mypassword -v ${PWD}/storage:/root elestio/docker-desktop-vnc
=======
docker run -p 6080:80 -p 5900:5900 -e VNC_PASSWORD=mypassword -v ${PWD}/knime-workspace:/root/knime-workspace elestio/docker-desktop-vnc-knime
>>>>>>> f6590a4ff663a626c31b70f8348638bad227a87c
```

A prompt will ask password either in the browser or vnc viewer.

## HTTP Base Authentication

This image provides base access authentication of HTTP via `HTTP_PASSWORD`

```shell
<<<<<<< HEAD
docker run -p 6080:80 -e HTTP_PASSWORD=mypassword -v ${PWD}/storage:/root elestio/docker-desktop-vnc
=======
docker run -p 6080:80 -e HTTP_PASSWORD=mypassword -v ${PWD}/knime-workspace:/root/knime-workspace elestio/docker-desktop-vnc-knime
>>>>>>> f6590a4ff663a626c31b70f8348638bad227a87c
```

## SSL

To connect with SSL, generate self signed SSL certificate first if you don't have it

```shell
mkdir -p ssl
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ssl/nginx.key -out ssl/nginx.crt
```

Specify SSL port by `SSL_PORT`, certificate path to `/etc/nginx/ssl`, and forward it to 6081

```shell
<<<<<<< HEAD
docker run -p 6081:443 -e SSL_PORT=443 -v ${PWD}/ssl:/etc/nginx/ssl -v ${PWD}/storage:/root elestio/docker-desktop-vnc
=======
docker run -p 6081:443 -e SSL_PORT=443 -v ${PWD}/ssl:/etc/nginx/ssl -v ${PWD}/knime-workspace:/root/knime-workspace elestio/docker-desktop-vnc-knime
>>>>>>> f6590a4ff663a626c31b70f8348638bad227a87c
```

## Screen Resolution

The Resolution of virtual desktop adapts browser window size when first connecting the server. You may choose a fixed resolution by passing `RESOLUTION` environment variable, for example

```shell
<<<<<<< HEAD
docker run -p 6080:80 -e RESOLUTION=1920x1080 -v ${PWD}/storage:/root elestio/docker-desktop-vnc
=======
docker run -p 6080:80 -e RESOLUTION=1920x1080 -v ${PWD}/knime-workspace:/root/knime-workspace elestio/docker-desktop-vnc-knime
>>>>>>> f6590a4ff663a626c31b70f8348638bad227a87c
```

## Default Desktop User

The default user is `root`. You may change the user and password respectively by `USER` and `PASSWORD` environment variable, for example,

```shell
<<<<<<< HEAD
docker run -p 6080:80 -e USER=doro -e PASSWORD=password -v ${PWD}/storage:/root elestio/docker-desktop-vnc
=======
docker run -p 6080:80 -e USER=doro -e PASSWORD=password -v ${PWD}/knime-workspace:/root/knime-workspace elestio/docker-desktop-vnc-knime
>>>>>>> f6590a4ff663a626c31b70f8348638bad227a87c
```



# Credits
This is a fork from: https://github.com/fcwu/docker-ubuntu-vnc-desktop
