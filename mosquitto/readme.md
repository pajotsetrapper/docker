# Docker compose file for running an MQTT broker, with persistence & authentication.
Based on eclipse-mosquitto

Config file & black passwd file are in the config subfolder.
After starting the container (sudo docker compose up -d), you need to add credentials for a user that can be used to register / publish updates (authentication).
To do so, connect to the Docker container and run:

connect to the docker image & add credentials (will be stored in /mosquitto/config/passwd, which is mapped to the local volume)

mosquitto_passwd -b /mosquitto/config/passwd guest guest 
Warning: File /mosquitto/config/passwd has world readable permissions. Future versions will refuse to load this file.
To fix this, use `chmod 0700 /mosquitto/config/passwd`.Warning: File /mosquitto/config/passwd owner is not root. Future versions will refuse to load this file.To fix this, use `chown root /mosquitto/config/passwd`.Warning: File /mosquitto/config/passwd group is not root. Future versions will refuse to load this file./ # chown ^C
/ # chown root /mosquitto/config/passwd
/ # chmod 0700 /mosquitto/config/passwd
