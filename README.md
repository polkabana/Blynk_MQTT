Blynk.cc to MQTT broker bridge
=============================+

[Blynk.cc](http://blynk.cc/) nice project with nice [Android application](https://play.google.com/store/apps/details?id=cc.blynk), but uses own protocol and library not implemented on some hardware.

This is simple bridge between Blynk.cc and MQTT. Only virtual pins allowed.


Setup
-----

Setup your token and broker:
```
TOKEN = "YourAppToken"
MQTT_SERVER = "test.mosquitto.org"
MQTT_PORT = 1883
TOPIC = "/ESP009xxxxx"
```
And run ```python blynk-mqtt.py```

Requires paho-mqtt python module


MQTT Topics
-----------

Virtual pin 0 write request will be published as /ESP009xxxxx/vw/0 topic.
Virtual pin 0 read request will be published as /ESP009xxxxx/vr/0 topic and also will be send answer to Blynk.cc server - latest pin value.
Where 0 is virtual pin number.

Bridge subscribes for all /ESP009xxxxx/# topics and translate them to virtual pins according translate table
```
translate_topic = (
	('sensors/bmpt', 0),
	('sensors/bmpp', 1),
)
```

This mean that value from topic /ESP009xxxxx/sensors/bmpt will be translate to virtual pin 0, for example.

Topics like /ESP009xxxxx/vw/0 will be translate to virtual pin 0.


Copyright
---------

This work based on code blynk-library/tests/pseudo-library.py from Blynk.cc project.
