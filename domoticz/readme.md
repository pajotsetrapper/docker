# Docker-compose yml file for running the latest stable domoticz container #

Creates / re-uses a Docker volume named 'domoticz' & mounts it to /opt/domoticz/userdata in the container
As such the database, scripts, ... are persisted on container start

Run "docker-compose up -d" to run the container
