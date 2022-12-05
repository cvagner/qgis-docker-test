# Tests QGIS Docker : Server & Desktop

Cf. [Official website](https://github.com/camptocamp/docker-qgis-server).

## Server

**Run a QGIS Server from docker** from next command. I tries to load any project present in data directory :
```sh
# From the root directory of the project (or set another volume bind mount)
docker run --rm \
  --publish=8380:80 \
  --volume=$(pwd)/data:/etc/qgisserver \
  -eQGIS_SERVER_LANDING_PAGE_PROJECTS_DIRECTORIES=/etc/qgisserver \
  camptocamp/qgis-server
```

Open http://localhost:8380/

## Desktop

You can **share X11 display to run desktop from docker** (here with home mounted) :
```sh
# From any directory
docker run --rm -ti \
  --env=DISPLAY=unix${DISPLAY} --volume=/tmp/.X11-unix:/tmp/.X11-unix \
  --volume=${HOME}:${HOME} \
  camptocamp/qgis-server:master-desktop
```

The `data/alaska.qgs` QGIS project has been included here with two layers loaded from `data/shapefiles` directory.
