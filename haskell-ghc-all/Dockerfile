FROM ubuntu:jammy
LABEL org.opencontainers.image.authors="Toni Okuogume <toni.okuogume@futurice.com>,Jorge Rodriguez <jorge.rodriguez@futurice.com>"

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
  libffi-dev \
  libffi8ubuntu1 \
  libfftw3-bin \
  libfftw3-dev \
  libgmp-dev \
  libgmp10 \
  libgts-bin \
  liblapack-dev \
  liblzma-dev \
  libncurses-dev \
  libncurses5 \
  libnuma-dev \
  libpango1.0 \
  libpq-dev \
  libpq5 \
  libtinfo5 \
  libyaml-dev \
  llvm \
  locales \
  netbase \
  openssh-client \
  pkg-config \
  python3-dev \
  zip \
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
RUN echo 'Europe/Helsinki' > /etc/timezone && rm /etc/localtime || true && ln -s /usr/share/zoneinfo/Europe/Helsinki /etc/localtime

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

RUN cabal new-update
RUN cabal new-install -j cabal-plan --constraint=cabal-plan==0.7.2.1 --constraint='cabal-plan +exe' --installdir=/root/.cabal/bin
RUN cp /root/.cabal/bin/$(readlink /root/.cabal/bin/cabal-plan) /root/cabal-plan
RUN rm -rf /root/.cabal /root/.ghc
RUN mkdir -p /root/.cabal/bin
RUN mv /root/cabal-plan /root/.cabal/bin
RUN ls -l /root/.cabal/bin
RUN echo "cabal-plan installed"
