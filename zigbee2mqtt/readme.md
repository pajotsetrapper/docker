# Zigbee2MQTT docker container

Container for using a Zigbee (SLZB-MR2 or similar) gateway with Home Assistant, using the MQTT Protocol.


Update your settings in: zigbee2mqtt/data/configuration.yml.
Note, in this zigbee2mqtt config file, permit_join is enabled. 
In Zigbee2MQTT, the permit_join setting controls whether new devices are allowed to join your Zigbee network. Setting it to false has an important effect on network security and device management.
What permit_join: false Does
- Disables new device pairing. When permit_join is false, no new Zigbee devices can join your network. Existing devices will continue to communicate normally.
- Enhances network security. Allowing open joining (permit_join: true) can expose your network to unauthorized devices. By setting it to false, you prevent unknown devices from joining your Zigbee network.
- Typical usage scenario During normal operation, keep permit_join: false for safety. Temporarily enable permit_join: true only when adding a new device, then revert back to false.

# Allow joining temporarily via MQTT
- mosquitto_pub -t 'zigbee2mqtt/bridge/request/permit_join' -m '{"value":true}'
# After adding devices, disable again
- mosquitto_pub -t 'zigbee2mqtt/bridge/request/permit_join' -m '{"value":false}'


The service will listen on port 8090. Navigate to that port to further configure Zigbee2Mqtt
https://www.freecodecamp.org/news/how-to-set-up-zigbee2mqtt-with-docker
