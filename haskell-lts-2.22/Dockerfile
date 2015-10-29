FROM phadej/ghc:7.8.4-ubuntu
MAINTAINER Oleg Grenrus <oleg.grenrus@iki.fi>

RUN apt-get -yq update && apt-get -yq --no-install-suggests --no-install-recommends --force-yes install \
    ca-certificates \
    curl \
    git \
    libpq-dev \
  && rm -rf /var/lib/apt/lists/*

# Set timezone to Europe/Helsinki
RUN echo 'Europe/Helsinki' > /etc/timezone && rm /etc/localtime && ln -s /usr/share/zoneinfo/Europe/Helsinki /etc/localtime

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# pre build some packages
# not the whole Stackage though.
RUN stack update
RUN stack --resolver=lts-2.22 build --only-snapshot \
  HUnit \
  JuicyPixels \
  MonadRandom \
  SHA \
  StateVar \
  aeson \
  ansi-terminal \
  ansi-wl-pprint \
  appar \
  array \
  asn1-encoding \
  asn1-parse \
  asn1-types \
  async \
  attoparsec \
  auto-update \
  base-compat \
  base-prelude \
  base16-bytestring \
  base64-bytestring \
  bifunctors \
  binary \
  blaze-builder \
  blaze-html \
  blaze-markup \
  byteable \
  byteorder \
  bytestring \
  bytestring-builder \
  bytestring-conversion \
  case-insensitive \
  cereal \
  cipher-aes \
  cipher-des \
  cipher-rc4 \
  comonad \
  conduit \
  conduit-extra \
  connection \
  containers \
  contravariant \
  convertible \
  cookie \
  crypto-cipher-types \
  crypto-numbers \
  crypto-pubkey \
  crypto-pubkey-types \
  crypto-random \
  cryptohash \
  cryptohash-conduit \
  data-default \
  data-default-class \
  data-default-instances-base \
  data-default-instances-containers \
  data-default-instances-dlist \
  data-default-instances-old-locale \
  deepseq \
  directory \
  distributive \
  dlist \
  double-conversion \
  easy-file \
  either \
  exceptions \
  extensible-exceptions \
  fast-logger \
  filepath \
  focus \
  free \
  generics-sop \
  hashable \
  hourglass \
  http-client \
  http-client-tls \
  http-conduit \
  http-date \
  http-media \
  http-types \
  iproute \
  lens \
  lifted-base \
  list-t \
  loch-th \
  lucid \
  memory \
  mime-types \
  mmorph \
  monad-control \
  mtl \
  nats \
  network \
  network-uri \
  old-locale \
  old-time \
  optparse-applicative \
  parallel \
  parallel-io \
  parsec \
  pem \
  placeholders \
  prelude-extras \
  pretty \
  primitive \
  process \
  profunctors \
  random \
  reflection \
  resourcet \
  safe \
  scientific \
  securemem \
  semigroupoids \
  semigroups \
  setenv \
  simple-sendfile \
  singletons \
  socks \
  split \
  stm \
  stm-containers \
  streaming-commons \
  string-conversions \
  stringsearch \
  syb \
  system-fileio \
  system-filepath \
  tagged \
  text \
  text-binary \
  th-desugar \
  th-expand-syns \
  th-lift \
  th-orphans \
  th-reify-many \
  time \
  tls \
  transformers \
  transformers-base \
  transformers-compat \
  unix \
  unix-compat \
  unix-time \
  unordered-containers \
  utf8-string \
  vault \
  vector \
  vector-binary-instances \
  void \
  wai \
  wai-app-static \
  wai-extra \
  wai-logger \
  warp \
  word8 \
  x509 \
  x509-store \
  x509-system \
  x509-validation \
  zlib \
 && echo "DONE!"
