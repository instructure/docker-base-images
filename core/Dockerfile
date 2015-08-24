FROM ubuntu:trusty
MAINTAINER Instructure

## Create a 'docker' user
RUN  addgroup --gid 9999 docker \
  && adduser --uid 9999 --gid 9999 --disabled-password --gecos "Docker User" docker \
  && usermod -L docker

## APT setup
## Upgrade all packages
## Install common tools
ENV DEBIAN_FRONTEND=noninteractive
RUN  apt-get update \
  && apt-get install -y --no-install-recommends \
	     apt-transport-https \
	     ca-certificates \
	     software-properties-common \
	     language-pack-en \
	     locales \
  && apt-get install -y --no-install-recommends \
	     curl \
	     psmisc \
	     git \
	     build-essential \
             python

#Install passenger and nginx
RUN  apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 561F9B9CAC40B2F7 \
  && apt-get install -y apt-transport-https ca-certificates \
  && sh -c 'echo deb https://oss-binaries.phusionpassenger.com/apt/passenger trusty main > /etc/apt/sources.list.d/passenger.list' \
  && apt-get update \
  && apt-get upgrade -y --no-install-recommends \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

## Ensure UTF-8 locale
RUN locale-gen en_US.UTF-8
ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8
RUN dpkg-reconfigure locales
USER docker
