# About

**Deprecated**: SQLite isn't supported anymore so this repository will not longer be maintained. Please use the official [Etherpad Lite](https://github.com/ether/etherpad-lite) or my [Etherpad Lite docker image](https://hub.docker.com/r/fuerst/etherpad-lite) which is closely based on the official Etherpad Lite release but adds Libreoffice export capabilities and uses a Redis database backend.

**Old documentation:**

Run [Etherpad Lite](https://github.com/ether/etherpad-lite) inside a Docker container.
This variant of an Etherpad Docker container is characterized by:

At run time:

* Using SQLite as data backend.
* Allow using persistent volumes for data, plugins and settings.
* Create administration user with configurable password.
* Choose between _develop_ or _stable_ version.
* Using Abiword for import/export of DOC or PDF. ODF is not supported yet - it just crashes the abiword binary for unknown reason.

At image build time:

* By default it uses the latest Etherpad Lite _develop_ version.
* Allows to install another Etherpad Lite version (by Git tag or branch).

# Usage

**Start an Etherpad Lite instance listening on TCP port 9001**

```
docker run -p 9001:9001 fuerst/etherpad-docker
```

**Set password for administration user named _admin_**

```
docker run -p 9001:9001 \
  -e ETHERPAD_ADMIN_PASSWORD='my-secret-password' \
  fuerst/etherpad-docker
```

**Make plugins, database and settings persistent**

```
docker run -p 9001:9001 \
  -v /opt/etherpad-lite/var:/opt/etherpad-lite/var \
  -v /opt/etherpad-lite/node_modules:/opt/etherpad-lite/node_modules \
  fuerst/etherpad-docker
```

**Run Etherpad Lite stable version (1.7.5)**

At the time of writing _stable_ means 1.7.5.

```
docker run -p 9001:9001 \
  fuerst/etherpad-docker:stable
```

**Build another version**

Only latest stable release (1.7.5) and _develop_ are available from hub.docker.com. You may build any other release you want by specifying an etherpad-lite branch or tag when building your own image:

```
docker build -e ETHERPAD_VERSION='1.5.5' .
```

**Example Docker Compose file**

```
version: "2"

services:
  server:
    image: fuerst/etherpad-docker:stable
    restart: always
    volumes:
      - /opt/etherpad-lite/var:/opt/etherpad-lite/var
      - /opt/etherpad-lite/node_modules:/opt/etherpad-lite/node_modules
    ports:
      - "9001:9001"
    environment:
    - ETHERPAD_ADMIN_PASSWORD=my-secret-password
```

# Documentation

See: https://github.com/ether/etherpad-lite/wiki
