# Docker compose file eclipse-mosquitto, an MQTT broker.

https://hub.docker.com/_/eclipse-mosquitto/

## Configuration

The config folder will be mapped to /mosquitto/config.
This project comes with a pre-configured mosquitto.conf file. The full man mage is available on https://mosquitto.org/man/mosquitto-conf-5.html.
It is currently configured to
- require authentication (credentials to be added using the `mosquitto_passwd` command, from the container itself)
- enable persistency & logging

## Starting & preparing the container:

- run `sudo docker compose up -d`
- connect to the docker container console: `docker exec -it <mycontainer> sh`
- add credentials to be used for subscribing / publishing event `mosquitto_passwd -b /mosquitto/config/passwd guest guest` > guest / guest being the username/password here. This will update /mosquitto/config/passwd.
- update the permissions on /mosquitto/config/passwd: `chown root /mosquitto/config/passwd && chmod 0700 /mosquitto/config/passwd`

## Testing

To see if the service runs file, subscribe to a topic with one client & publish to the topic with another (e.g. use 2 consoles):
- Subscribe to the topic with authentication: `sudo docker exec mosquitto mosquitto_sub -u guest -P guest -v -t 'home/livingroom/humidity'`
- Publish to the topic with authentication: `sudo docker exec mosquitto mosquitto_pub -u guest -P guest  -t 'home/livingroom/humidity' -m '42'`
