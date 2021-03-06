# Get Readings from an Airthings Wave and publish to MQTT server

[Airthings](http://airthings.com) makes a BTLE Radon detector called "Wave". This is an executable intended to be called periodically from Cron or some other scheduler to publish readings to an MQTT server.

## Limitations

This application doesn't implement 'find' as provided in the example at https://airthings.com/raspberry-pi/

This is just a python API with a main loop that I happen to use in my own Home-Assistant setup. If you're looking for a plug and play solution, consider [balena-airthingswave](https://github.com/renemarc/balena-airthingswave) - @renemarc has created his appliance package using airthingswave-mqtt.

## API

```Python
class AirthingsWave:
    def __init__(self, config_file):
```

Class instantiation requires a path to a config file in YAML format.

```
mqtt:
  broker: 192.168.30.18
  port: 1883
  username: 
  password: 

waves:
  - name: "basement-radon"
    addr: 98:07:2d:43:4d:ff
```

Before taking a reading, you should:

```
def ble_connect(self, addr):
```

Then you can:

```
def get_readings(self, p):
def publish_readings(self, name, readings):
```

## Example

From \__main\__.py:
```python
c = sys.argv[1]

atw = airthingswave.AirthingsWave_mqtt(c)

count = len(atw.waves)
if count > 0:
    i = 0
    while i < count:
        handle = atw.ble_connect(atw.waves[i]["addr"])
        r = atw.get_readings(handle)
        atw.ble_disconnect(handle)
        atw.publish_readings(atw.waves[i]["name"], r)
        i = i+1

return True
```
