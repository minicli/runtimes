# minicli/php81

Distroless Alpine-based PHP 8.1 image to execute Minicli applications, including full GD support. As a distroless image, it doesn't contain `apk` or `composer`. By design, this limits the attack surface and makes the runtime more hermetic, which has several benefits in terms of security. For a non-distroless alternative, check the [php81-dev](https://hub.docker.com/repository/docker/minicli/php81-dev) image. 

This image is automatically built and published to [minicli/php81](https://hub.docker.com/repository/docker/minicli/php81) on Docker Hub via GitHub Actions. Every image includes attestation signatures created with [Sigstore](https://docs.sigstore.dev). With the [Cosign](https://docs.sigstore.dev/cosign/overview) client installed, you can check this image signature with:

```shell
COSIGN_EXPERIMENTAL=1 cosign verify minicli/php81:latest | jq
```

You'll get output that tells details about the image signature and should have the `Issuer` and `Subject` fields pointing to GitHub (Actions) URLs.

## Usage

Use it directly with `docker run` to execute PHP:

```shell
docker run --rm erikaheidi/minicli:php81 --version
```

Or extend it from your Dockerfile to create a custom image based on it. This will allow you to install Composer and get your application dependencies installed as well. For instance, the following Dockerfile is used by the [Dynacover](https://github.com/erikaheidi/dynacover) GitHub Action:

```Dockerfile
FROM minicli/php81:latest

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Checkout Dynacover
RUN git clone -b 1.0.1 --depth 1 https://github.com/erikaheidi/dynacover.git && \
    cd dynacover && \
    composer install --no-progress --no-dev --prefer-dist

ENTRYPOINT [ "php81", "/dynacover/dynacover" ]
CMD ["cover", "update"]
```
## Image Details

- Workdir: `/home/minicli`
- Non-root user: `minicli`
- By default, runs commands as `root` 

## What's included:

- alpine-baselayout-data
- ca-certificates-bundle
- curl
- git
- zip
- unzip
- libxml2-dev
- freetype-dev
- libjpeg-turbo-dev
- libpng-dev
- php81
- php81-gd
- php81-curl
- php81-mbstring
- php81-phar
- php81-openssl
- php81-pcntl
