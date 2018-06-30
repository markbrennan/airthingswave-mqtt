# Get Readings from an Airthings Wave and publish to MQTT server

[Airthings](http://airthings.com) makes a BTLE Radon detector called "Wave". This is an executable intended to be called periodically from Cron or some other scheduler to publish readings to an MQTT server.

## Limitations
## API

This application doesn't implement 'find' as provided in the example at https://airthings.com/raspberry-pi/

## API

```Python
class AirthingsWave:
    def __init__(self, config_file):
```

Class instantiation requires a path to a config file in YAML format.
<<<<<<< Updated upstream
=======


```
mqtt:
  broker: 192.168.30.18
  port: 1883

waves:
  - name: "basement-radon"
    addr: 98:07:2d:43:4d:ff
```
>>>>>>> Stashed changes
