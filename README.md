# Futurice base docker images

## Supported tags and respective Dockerfile links

- [`haskell-ghc-8.0.2-1` (haskell-ghc-8.0.2/Dockerfile)](https://github.com/futurice/docker-base-images/blob/master/haskell-ghc-8.0.2/Dockerfile)
- [`haskell-lts-6-2` (haskell-lts-6/Dockerfile)](https://github.com/futurice/docker-base-images/blob/master/haskell-lts-6/Dockerfile)
- [`nodejs` (nodejs/Dockerfile)](https://github.com/futurice/docker-base-images/blob/master/nodejs/Dockerfile)

## What is Futurice?

![logo](https://raw.githubusercontent.com/futurice/docker-base-images/master/logo.png)

## To build images locally

```sh
docker build -t futurice/base-images:haskell-lts-6-2 haskell-lts-6
docker build -t futurice/base-images:haskell-ghc-8.0.2-1 haskell-ghc-8.0.2
```
