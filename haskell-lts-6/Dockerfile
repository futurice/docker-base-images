FROM phadej/ghc:7.10.3-ubuntu
MAINTAINER Oleg Grenrus <oleg.grenrus@iki.fi>

RUN apt-get -yq update && apt-get -yq --no-install-suggests --no-install-recommends --force-yes install \
    ca-certificates \
    curl \
    git \
    libfftw3-dev \
    liblapack-dev \
    liblzma-dev \
    libpq-dev \
    libyaml-dev \
    pkg-config \
  && rm -rf /var/lib/apt/lists/*

# Set timezone to Europe/Helsinki
RUN echo 'Europe/Helsinki' > /etc/timezone && rm /etc/localtime && ln -s /usr/share/zoneinfo/Europe/Helsinki /etc/localtime

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Install newer stack
RUN mkdir -p $HOME/.local/bin \
  && curl -L https://www.stackage.org/stack/linux-x86_64 | tar xz --wildcards --strip-components=1 -C /usr/bin '*/stack' \
  && stack --version
