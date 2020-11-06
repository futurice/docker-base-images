FROM ubuntu:bionic
MAINTAINER Toni Okuogume <toni.okuogume@futurice.com>

# hvr-ppa
RUN apt-get -yq update && apt-get -yq --no-install-suggests --no-install-recommends install \
    software-properties-common \
    apt-utils \
  && apt-add-repository -y "ppa:hvr/ghc" \
  && rm -rf /var/lib/apt/lists/*

# Dependencies
RUN apt-get -yq update && apt-get -yq --no-install-suggests --no-install-recommends install \
    cabal-install-3.2 \
    ghc-8.8.4 \
    ghc-8.6.5 \
    ghc-8.4.3 \
    git \
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
  && rm -rf /var/lib/apt/lists/*

# Set timezone to Europe/Helsinki
RUN echo 'Europe/Helsinki' > /etc/timezone && rm /etc/localtime && ln -s /usr/share/zoneinfo/Europe/Helsinki /etc/localtime

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en
ENV LC_ALL=en_US.UTF-8

# Use cabal
ENV PATH=/root/.local/bin:/opt/ghc/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

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
    && echo 'cabal-version: 2.2'      > z.cabal \
    && echo 'name: z'                >> z.cabal \
    && echo 'version: 0'             >> z.cabal \
    && echo 'library'                >> z.cabal \
    && echo '  build-depends: aeson' >> z.cabal \
    && cat z.cabal \
    && (cabal new-build || true) \
    && rm -f z.cabal \
    && cabal new-install cabal-plan --constraint=cabal-plan==0.6.2.0 --constraint='cabal-plan +exe' --installdir=$HOME/.local/bin \
    && cp $HOME/.local/bin/$(readlink $HOME/.local/bin/cabal-plan) $HOME/cabal-plan \
    && mv $HOME/cabal-plan $HOME/.local/bin \
    && ls -l $HOME/.local/bin \
    && rm -rf $HOME/.cabal $HOME/.ghc \
    && echo "cabal-plan installed"
