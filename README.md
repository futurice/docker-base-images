# Futurice base docker images

## Supported tags and respective Dockerfile links

- [`haskell-ghc-all(few latest major ghc releases)` (haskell-ghc-all/Dockerfile)](https://github.com/futurice/docker-base-images/blob/master/haskell-ghc-all/Dockerfile)

## What is Futurice?

![logo](https://raw.githubusercontent.com/futurice/docker-base-images/master/logo.png)

## To build images locally

Build locally base image for haskell-mega-repo and push it to repository

```sh
docker build --no-cache -t haskell-ghc-all:$(date +"%Y%m%d") haskell-ghc-all
docker tag haskell-ghc-all:$(date +"%Y%m%d") futurice/base-images:haskell-ghc-all-$(date +"%Y%m%d")
docker push futurice/base-images:haskell-ghc-all-$(date +"%Y%m%d")
```
