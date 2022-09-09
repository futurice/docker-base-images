FROM amazonlinux:2.0.20220805.0

ENV TZ=Europe/Helsinki

# dependencies
RUN yum -y update && yum -y install ncurses-compat-libs gmp gmp-devel zlib-devel fftw3-devel postgresql-devel xz-devel libssl3 nss nss-devel openssl-devel openldp strip git gcc g++ make

RUN curl https://downloads.haskell.org/~ghcup/x86_64-linux-ghcup > /usr/bin/ghcup && chmod +x /usr/bin/ghcup

RUN ghcup install ghc 9.0.2 && ghcup install cabal recommended && ghcup set ghc 9.0.2 && ghcup set cabal recommended
