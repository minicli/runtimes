# minicli/runtimes

Minimalist / distroless OCI images for running Minicli with PHP on cloud-native environments. 

## Nightly Builds
Images are built every night and published to [Docker Hub](https://hub.docker.com/u/minicli) via GitHub Actions.

## Available Images
The following images are currently available. You can find more information and usage instructions on the README file that is included within each image folder in this repository.

- [php81](/php81) - The `php81` image is a distroless, Alpine-based image with several PHP extensions, including full GD support. It doesn't come with Composer or apk. Used to run Minicli apps on production.
  - Total size: 48MB
  - Available as: [minicli/php81](https://hub.docker.com/repository/docker/minicli/php81)
- [php81-dev](/php81-dev) - The `php81-dev` image is a minimalist development image that includes all packages from `php81` and also `apk-tools`, Composer, and `vim`. Used to develop and debug Minicli apps.
  - Total size: 79.5MB
  - Available as: [minicli/php81-dev](https://hub.docker.com/repository/docker/minicli/php81-dev)
- [php81-curl](/php81-curl) - The `php81-curl` image is tailored for running API requests with Curl, ideal for bots and crawlers using [minicli/curly](https://github.com/minicli/curly). This image doesn't include GD.
  - Total size: 30MB
  - Available as: [minicli/php81-curl](https://hub.docker.com/repository/docker/minicli/php81-curl)