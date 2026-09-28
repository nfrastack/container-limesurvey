# nfrastack/container-limesurvey

## About

This repository will build a conatiner image for running [LimeSurvey](https://www.limesurvey.org/) - A Surveying Platform.


## Maintainer

* [Nfrastack](https://www.nfrastack.com)

## Table of Contents

* [About](#about)
* [Maintainer](#maintainer)
* [Table of Contents](#table-of-contents)
* [Installation](#installation)
  * [Prebuilt Images](#prebuilt-images)
  * [Quick Start](#quick-start)
  * [Persistent Storage](#persistent-storage)
* [Configuration](#configuration)
  * [Environment Variables](#environment-variables)
    * [Base Images used](#base-images-used)
    * [Core Configuration](#core-configuration)
  * [Users and Groups](#users-and-groups)
  * [Networking](#networking)
* [Maintenance](#maintenance)
  * [Shell Access](#shell-access)
* [Support & Maintenance](#support--maintenance)
* [License](#license)
* [References](#references)

## Installation

### Prebuilt Images

Feature limited builds of the image are available on the [Github Container Registry](https://github.com/nfrastack/container-limesurvey/pkgs/container/container-limesurvey) and [Docker Hub](https://hub.docker.com/r/nfrastack/limesurvey).

To unlock advanced features, one must provide a code to be able to change specific environment variables from defaults. Support the development to gain access to a code.

To get access to the image use your container orchestrator to pull from the following locations:

```
ghcr.io/nfrastack/container-limesurvey:(image_tag)
docker.io/nfrastack/limesurvey:(image_tag)
```

Image tag syntax is:

`<image>:<branch>-<optional tag>-<optional phpversion>`

Example:

`docker.io/nfrastack/container-limesurvey:latest` or

`ghcr.io/nfrastack/container-limesurvey:6-1.0` or

`ghcr.io/nfrastack/container-limesurvey:6-2.0-php84`



* `latest` will be the most recent commit

* `branch` will be the repositories branch, typically matching with the major version of LimeSurvey eg `6`

* An optional `tag` may exist that matches the [CHANGELOG](CHANGELOG.md) - These are the safest

* An optional `phpversion` may exist like `php84` or `php83`

Have a look at the container registries and see what tags are available.

#### Multi-Architecture Support

Images are built for `amd64` by default, with optional support for `arm64` and other architectures.

### Quick Start

* The quickest way to get started is using [docker-compose](https://docs.docker.com/compose/). See the examples folder for a working [compose.yml](examples/compose.yml) that can be modified for your use.

* Map [persistent storage](#persistent-storage) for access to configuration and data files for backup.
* Set various [environment variables](#environment-variables) to understand the capabilities of this image.


### Easypanel

[Easypanel](https://easypanel.io) is a self-hosted Docker deployment platform, and it maintains a one-click deployment template for LimeSurvey built on this image:

[![Deploy on Easypanel](https://easypanel.io/img/deploy-on-easypanel-40.svg)](https://easypanel.io/templates/limesurvey)

### Persistent Storage

The following directories/files should be mapped for persistent storage in order to utilize the container effectively.

| Directory   | Description             |
| ----------- | ----------------------- |
| `/logs`     | Nginx and PHP Log files |
| `/www/html` | Limesurvey sourcecode   |


### Environment Variables

#### Base Images used

This image relies on a customized base image in order to work.
Be sure to view the following repositories to understand all the customizable options:

| Image                                                                 | Description         |
| --------------------------------------------------------------------- | ------------------- |
| [OS Base](https://github.com/nfrastack/container-base/)               | Base Image          |
| [Nginx](https://github.com/nfrastack/container-nginx/)                | Nginx Webserver     |
| [Nginx PHP-FPM](https://github.com/nfrastack/container-nginx-php-fpm) | PHP-FPM Interpreter |

Below is the complete list of available options that can be used to customize your installation.

* Variables showing an 'x' under the `Advanced` column can only be set if the containers advanced functionality is enabled.

#### Core Configuration

| Parameter         | Description                                                   | Default             | `_FILE` |
| ----------------- | ------------------------------------------------------------- | ------------------- | ------- |
| `ADMIN_USER`      | Username of Administrator Account                             | `admin`             | x       |
| `ADMIN_NAME`      | Full name of Administrator Account                            |                     | `Admin` | x |
| `ADMIN_PASS`      | Password of Administrator account                             |                     | x       | x |
| `ADMIN_EMAIL`     | Email address of Administrator Account                        | `admin@example.com` | x       |
| `DB_HOST`         | Host or container name of MariaDB Server e.g. `limesurvey-db` |                     | x       |
| `DB_NAME`         | MariaDB Database name e.g. `limesurvey`                       |                     | x       |
| `DB_PASS`         | MariaDB Password for above Database e.g. `password`           |                     | x       |
| `DB_PORT`         | MariaDB Port                                                  | `3306`              | x       |
| `DB_USER`         | MariaDB Username for above Database e.g. `limesurvey`         |                     | x       |
| `DB_CHARSET`      | MariaDB Character Set                                         | `utf8mb4`           | x       |
| `DB_TABLE_PREFIX` | Database Table Prefix                                         | `lime_`             | x       |
| `URL_FORMAT`      | URL Format                                                    | `path`              |         |
| `PUBLIC_URL`      | Public URL to adverstise application                          |                     |

* * *

## Maintenance

### Shell Access

For debugging and maintenance, `bash` and `sh` are available in the container.

## Support & Maintenance

* For community help, tips, and community discussions, visit the [Discussions board](/discussions).
* For personalized support or a support agreement, see [Nfrastack Support](https://nfrastack.com/).
* To report bugs, submit a [Bug Report](issues/new). Usage questions will be closed as not-a-bug.
* Feature requests are welcome, but not guaranteed. For prioritized development, consider a support agreement.
* Updates are best-effort, with priority given to active production use and support agreements.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

