FROM ubuntu:jammy
MAINTAINER Toni Okuogume <toni.okuogume@futurice.com>

RUN apt-get -yq update && apt-get -yq --no-install-suggests --no-install-recommends install \
    software-properties-common \
    apt-utils \
  && rm -rf /var/lib/apt/lists/*

# More deps
RUN apt-get -yq update && apt-get -y upgrade && apt-get -yq --no-install-suggests --no-install-recommends install \
    build-essential \
    ca-certificates \
    curl \
    git \
    graphviz \
    libcairo2 \
    libfftw3-bin \
    libfftw3-dev \
    libgmp10 \
    libgts-bin \
    liblapack-dev \
    liblzma-dev \
    libpango1.0 \
    libpq-dev \
    libpq5 \
    libyaml-dev \
    locales \
    netbase \
    openssh-client \
    pkg-config \
    python-dev \
    zip \
    llvm \
    libnuma-dev \
    libffi-dev libffi7 libgmp-dev libncurses-dev libncurses5 libtinfo5 \
  && rm -rf /var/lib/apt/lists/*

# ghcup for GHC, Cabal
RUN curl --proto '=https' --tlsv1.2 -sSf https://get-ghcup.haskell.org | \
    BOOTSTRAP_HASKELL_NONINTERACTIVE=1 \
    BOOTSTRAP_HASKELL_GHC_VERSION=9.0.2 \
    BOOTSTRAP_HASKELL_CABAL_VERSION=3.6.2.0 \
    sh
ENV PATH=/root/.cabal/bin:/root/.ghcup/bin:/root/.local/bin:$PATH
ENV GHCVER="9.0.2"

# Set timezone to Europe/Helsinki
RUN echo 'Europe/Helsinki' > /etc/timezone && rm /etc/localtime && ln -s /usr/share/zoneinfo/Europe/Helsinki /etc/localtime

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en
ENV LC_ALL=en_US.UTF-8

# Install cabal-plan -- sanity build check
#
# - cabal update, new-install cabal-plan
# - new-install creates symbolic link: copy over
# - wipe all of ~/.cabal & ~/.ghc
# - profit!

RUN true \
    && cabal new-update \
    && cabal new-install cabal-plan --constraint=cabal-plan==0.7.2.1 --constraint='cabal-plan +exe' --installdir=/root/.cabal/bin \
    && cp /root/.cabal/bin/$(readlink /root/.cabal/bin/cabal-plan) /root/cabal-plan \
    && rm -rf /root/.cabal /root/.ghc \
    && mkdir -p /root/.cabal/bin \
    && mv /root/cabal-plan /root/.cabal/bin \
    && ls -l /root/.cabal/bin \
    && echo "cabal-plan installed"
