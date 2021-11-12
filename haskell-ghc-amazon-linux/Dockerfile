FROM amazonlinux:2.0.20210219.0

# dependencies
RUN yum -y install tar xz perl gcc make gmp gmp-devel zlib zlib-devel pkgconfig git redhat-lsb-core nss

# GHC
RUN mkdir -p /usr/src/ghc
WORKDIR /usr/src/ghc

ENV GHCVER="8.10.7"
ENV GHC_TGZ="ghc-8.10.7-x86_64-fedora27-linux.tar.xz"

RUN curl --silent -O https://downloads.haskell.org/~ghc/$GHCVER/$GHC_TGZ \
  && echo "b6ed67049a23054a8042e65c9976d5e196e5ee4e83b29b2ee35c8a22ab1e5b73 $GHC_TGZ" | sha256sum -c - \
  && tar --strip-components=1 -xf $GHC_TGZ \
  && rm $GHC_TGZ \
  && ./configure --prefix=/opt/ghc \
  && make install \
  && rm -rf /usr/src/ghc \
  && /opt/ghc/bin/ghc --version

# Cabal
RUN mkdir -p /usr/src/cabal
WORKDIR /usr/src/cabal

ENV CABAL_VERSION="3.4.1.0"
ENV CABAL_TGZ="cabal-install-3.4.1.0-x86_64-linux.tar.xz"

RUN curl --silent -O http://downloads.haskell.org/cabal/cabal-install-$CABAL_VERSION/$CABAL_TGZ \
  && tar -xf $CABAL_TGZ \
  && rm $CABAL_TGZ \
  && cp /usr/src/cabal/cabal /opt/ghc/bin \
  && rm -rf /usr/src/cabal \
  && /opt/ghc/bin/cabal --version

RUN yum -y update && yum -y install fftw-devel \
        libstdc++-devel \
        xz-devel \
        postgresql-devel \
        glibc-locale-source \
        development

ENV PATH=/root/.cabal/bin:/opt/ghc/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# Set the locale
RUN localedef -i en_US -f UTF-8 en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en
ENV LC_ALL=en_US.UTF-8

# Install cabal-plan
#
# - cabal update, new-install cabal-plan
# - new-install creates symbolic link: copy over
# - wipe all of ~/.cabal & ~/.ghc
# - profit!

RUN true \
    && cabal v2-update \
    && cabal v2-install cabal-plan --constraint=cabal-plan==0.7.2.1 --constraint='cabal-plan +exe' --installdir=/root/.cabal/bin \
    && cp /root/.cabal/bin/$(readlink /root/.cabal/bin/cabal-plan) /root/cabal-plan \
    && rm -rf /root/.cabal /root/.ghc \
    && mkdir -p /root/.cabal/bin \
    && mv /root/cabal-plan /root/.cabal/bin \
    && ls -l /root/.cabal/bin \
    && echo "cabal-plan installed"

RUN ghc --version
RUN cabal --version
RUN cabal-plan --version
