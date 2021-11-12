# Futurice base docker images

## Supported tags and respective Dockerfile links

- [`haskell-ghc-all(few latest major ghc releases)` (haskell-ghc-all/Dockerfile)](https://github.com/futurice/docker-base-images/blob/master/haskell-ghc-all/Dockerfile)
- [`haskell-ghc-amazon-linux` (haskell-ghc-amazon-linux/Dockerfile)](https://github.com/futurice/docker-base-images/blob/master/haskell-ghc-amazon-linux/Dockerfile)

## What is Futurice?

![logo](https://raw.githubusercontent.com/futurice/docker-base-images/master/logo.png)

## Build for production

Multiarch builds for Docker Hub.

```sh
docker buildx build \
    --push \
    --platform linux/arm64,linux/amd64 \
    --tag futurice/base-images:haskell-ghc-all-$(date +"%Y%m%d") .
```

## Bbuild images locally

```
docker build --no-cache -t haskell-ghc-all:$(date +"%Y%m%d") haskell-ghc-all
```
