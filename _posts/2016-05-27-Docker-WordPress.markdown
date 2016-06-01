---
layout:     post
title:      "Docker Wordpress"
date:       2016-05-27 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---



## Enter docker container

> docker exec -it 4acaacf968b0 bash


###Exit
> Ctrl + P + Q

## Copy files From/To image
> docker cp /root/wordpress/enfold/ wordpress_wordpress_1:/var/www/html/wp-content/themes

 docker cp /root/wordpress/sitepress-multilingual-cms/ wordpress_wordpress_1:/var/www/html/wp-content/plugins

## Remove docker images 

>docker rm

## To view stopped and running containers

>docker ps -a

# Docker Compose 


>docker-compose ps


##Top process running on the container

>docker top 4acaacf968b0

Limite Container Resorse Usage 
> docker run --cup-shares=256
>docker run memory=1g

# Export Docker

Image location
/var/lib/docker/aufs/layers

Create a copy called "fridge"

>docker commit 4acaacf968b0 fridge

Command used to create this image

>docker history fridge

>docker save -o /root/temp/fridge.tar fridge


>docker load -i /root/temp/fridge.tar

# Create Image

## Using Docker Commit

1 Create docker container

>$ sudo docker run -i -t ubuntu /bin/bash
>root@4aab3ce3cb76:/#

2 Install Apache

>root@4aab3ce3cb76:/# apt-get -yqq update

>root@4aab3ce3cb76:/# apt-get -y install apache2

3 Exit from container

>root@4aab3ce3cb76:/# exit

4 Commit change

>$ sudo docker commit 4aab3ce3cb76 jamtur01/apache2

5 Check new image

>$ sudo docker images jamtur01/apache2

You can also add commit msg like this:

>$ sudo docker commit -m="A new custom image" --author="James Turnbull" 4aab3ce3cb76 jamtur01/apache2:webserver

You can check the image detail using:

>$ sudo docker inspect jamtur01/apache2:webserver

6 Run docker from an image

>$ sudo docker run -t -i jamtur01/apache2:webserver /bin/bash




### Run apache
>docker run -d -p 8080:80 shic/apache2 /usr/sbin/apache2ctl -D FOREGROUND



## Using Dockerfile

### 1 Create dockerfile

>$ mkdir static_web

>$ cd static_web

>$ touch Dockerfile

Note: this folder is the Build Environment

Dockerfile:

```
# Version: 0.0.1
FROM ubuntu:14.04
MAINTAINER James Turnbull "james@example.com"
RUN apt-get update
RUN apt-get install -y nginx
RUN echo 'Hi, I am in your container' \
>/usr/share/nginx/html/index.html
EXPOSE 80

```

> FROM base iamge

>EXPOSE port number

### 2 Run Dockerfile

>$ cd static_web

add "." to search dockerfile from current folder

>$ sudo docker build -t="jamtur01/static_web" .

or from git 

> $ sudo docker build -t="jamtur01/static_web:v1" git@github.com:jamtur01/docker-static_web

You can also set a tag for image (default tag is "latest"):

>$ sudo docker build -t="jamtur01/static_web:v1" .

