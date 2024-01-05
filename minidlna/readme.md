Dockerfile to build a Docker image for the minidlna service


- First container I ever built
- ... right after following a "Getting started with Docker" training on Udemy: https://www.udemy.com/course/learn-docker/
- Adding the steps to get to this image below

1. Looking for a minial Linux Docker image to start from: https://hub.docker.com/_/alpine
2. List the steps / config required to install/configure minidlna on Linux Alpine
    - Run a Docker alpine container, get access to its shell: winpty docker run -ti alpine sh
    - apk update
    - apk add minidlna

3.
to get the list of command to set up working minidlna manually

docker run


# MiniDLNA ([Dockerfile](Dockerfile))

This is MiniDLNA on top of minimal Alpine.
It can be configured with environment variables.

## Usage

Prefix any configuration directive of MiniDLNA with `MINIDLNA_`
and run your container:

```sh
docker run -d \
  --net=host \
  -v <media dir on host>:/media \
  -e MINIDLNA_MEDIA_DIR=/media \
  -e MINIDLNA_FRIENDLY_NAME=MyMini \
  vladgh/minidlna
```

Note: You need to run the container in host mode for it to be able to receive UPnP broadcast packets. The default bridge mode will not work.

Specify the user ID (UID) and group ID (GID):

```sh
docker run -d \
  --net=host \
  -v <media dir on host>:/media \
  -e PUID=1000 \
  -e PGID=1000 \
  -e MINIDLNA_MEDIA_DIR=/media \
  -e MINIDLNA_FRIENDLY_NAME=MyMini \
  vladgh/minidlna
```

Specify the timezone (defaults to UTC; <https://en.wikipedia.org/wiki/List_of_tz_database_time_zones>):

```sh
docker run -d \
  --net=host \
  -v <media dir on host>:/media \
  -e TZ=US/Central \
  -e MINIDLNA_MEDIA_DIR=/media \
  -e MINIDLNA_FRIENDLY_NAME=MyMini \
  vladgh/minidlna
```

### Multiple Media dirs

Any environment variable starting with `MINIDLNA_MEDIA_DIR` will be treated as
an additional `media_dir` directive and any suffix in the variable name will
be trimmed (ex: `MINIDLNA_MEDIA_DIR_1`). This way you can declare multiple
`media_dir` directives

```sh
docker run -d \
  --net=host \
  -v <media dir on host>:/media/audio \
  -v <media dir on host>:/media/video \
  -e MINIDLNA_MEDIA_DIR_1=A,/media/audio \
  -e MINIDLNA_MEDIA_DIR_2=V,/media/video \
  -e MINIDLNA_FRIENDLY_NAME=MyMini \
  vladgh/minidlna
```

See: <http://manpages.ubuntu.com/manpages/raring/man5/minidlna.conf.5.html>