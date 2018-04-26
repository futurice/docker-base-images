FROM phadej/ghc:8.2.2-ubuntu
MAINTAINER Oleg Grenrus <oleg.grenrus@iki.fi>

RUN apt-get -yq update && apt-get -y upgrade && apt-get -yq --no-install-suggests --no-install-recommends install \
    build-essential \
    ca-certificates \
    curl \
    git \
    libfftw3-dev \
    liblapack-dev \
    liblzma-dev \
    libpq-dev \
    libyaml-dev \
    locales \
    openssh-client \
    pkg-config \
  && rm -rf /var/lib/apt/lists/*

# Set timezone to Europe/Helsinki
RUN echo 'Europe/Helsinki' > /etc/timezone && rm /etc/localtime && ln -s /usr/share/zoneinfo/Europe/Helsinki /etc/localtime

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en
ENV LC_ALL=en_US.UTF-8

# Use cabal
ENV PATH=/root/.local/bin:/opt/ghc/8.2.2/bin:/opt/cabal/head/bin:/opt/happy/1.19.5/bin:/opt/alex/3.1.7/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# Install cabal-plan
#
# - make directory to store binaries (it's already in the PATH)
# - cabal update, new-install cabal-plan
# - new-install creates symbolic link: copy over
# - store 01-index.tar.gz, and wipe all of ~/.cabal & ~/.ghc
# - profit!
RUN true \
    && mkdir -p $HOME/.local/bin \
    && cabal update \
    && cabal new-install cabal-plan --constraint=cabal-plan==0.3.0.0 --constraint='cabal-plan +exe' --symlink-bindir=$HOME/.local/bin \
    && cp $HOME/.local/bin/$(readlink $HOME/.local/bin/cabal-plan) $HOME/cabal-plan \
    && mv $HOME/cabal-plan $HOME/.local/bin \
    && ls -l $HOME/.local/bin \
    && cp $HOME/.cabal/packages/hackage.haskell.org/01-index.tar.gz $HOME/ \
    && rm -rf $HOME/.cabal $HOME/.ghc \
    && echo "cabal-plan installed"
