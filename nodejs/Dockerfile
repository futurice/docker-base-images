FROM ubuntu:trusty
MAINTAINER Oleg Grenrus <oleg.grenrus@iki.fi>

RUN apt-get -yq update && apt-get -yq --no-install-suggests --no-install-recommends --force-yes install \
    software-properties-common \
    python-software-properties \
    apt-transport-https \
  && apt-key adv --keyserver hkps.pool.sks-keyservers.net --recv-key 68576280 \
  && apt-add-repository -y 'deb https://deb.nodesource.com/node_4.x trusty main' \
  && rm -rf /var/lib/apt/lists/*

RUN apt-get -yq update && apt-get -yq --no-install-suggests --no-install-recommends --force-yes install \
    ca-certificates \
    curl \
    git \
    make \
    nodejs \
  && rm -rf /var/lib/apt/lists/*
