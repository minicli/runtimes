# minicli/php81-curl

Distroless Alpine-based PHP 8.1 image optimized to run Minicli applications that make API requests using [minicli/curly](https://github.com/minicli/curly) (or other Curl wrappers).

This image is automatically built and published to [minicli/php81-curl](https://hub.docker.com/repository/docker/minicli/php81-curl) on Docker Hub via GitHub Actions. Every image includes attestation signatures created with [Sigstore](https://docs.sigstore.dev). With the [Cosign](https://docs.sigstore.dev/cosign/overview) client installed, you can check this image signature with:

```shell
COSIGN_EXPERIMENTAL=1 cosign verify minicli/php81-curl:latest | jq
```

You'll get output that tells details about the image signature and should have the `Issuer` and `Subject` fields pointing to GitHub (Actions) URLs.

## Usage

Use it directly with `docker run` to execute PHP:

```shell
docker run --rm minicli/php81-curl -v
```

Or extend it from your Dockerfile to create a custom image based on it. This will allow you to install Composer and get your application dependencies installed as well. 

Example Dockerfile that uses a multi-stage build to first set up the app and then copies it to the php81-curl runtime:

```Dockerfile
FROM minicli/php81-dev:latest AS builder

COPY . /home/minicli/
RUN cd /home/minicli && \
    composer install --no-progress --no-dev --prefer-dist

FROM minicli/php81-curl:latest
COPY --from=builder /home/minicli /home/minicli

ENTRYPOINT [ "php81", "/home/minicli/minicli" ]
CMD ["update-contributors"]

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
- php81
- php81-curl
- php81-mbstring
- php81-phar
- php81-openssl
- php81-pcntl
