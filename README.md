### Security System Alarm Monitoring with ESP8266 and MQTT

This is a hardware and software interface to monitor a GE NetworX home security system using a ESP8266 ESP-07 WiFi Module and a Raspberry Pi. The system sends a text and/or email in the event of any one of four alarm events.

The monitoring system requires Mosquitto MQTT and Node-Red software installed on a Raspberry Pi.

The ESP-07 software is written in two versions: Arduino IDE code and NodeMCU Lua code.

Alarm events are handled by publishing MQTT messages to Node-Red on a Raspberry Pi. Node-Red then sends texts and/or emails, depending on the event. In addition, Node-Red can send MQTT On/Off messages to the ESP-07 to blink the green LED, providing visual indication the system is active.

##### Arduino IDE Code Notes:
When I saw that the Arduino IDE became available to program the ESP8266, I decided to use it instead of Lua -- I find the IDE easy and familiar.

To upload code for the ESP-07, select the board "Generic ESP8266 Module" and leave all board settings as default. Select the proper port for your USB/Serial adapter. Press and hold the "Flash" pushbutton, then press and release the "Reset" pushbutton,  then release the "Flash" button. Finally, click the Upload button.

##### Lua Code Notes:
After installing the NodeMCU firmware, the ESP-07 needs to be set to connect to your wireless router. Once set, it remembers the connection. Setting can be done with a short Lua script or the LuaLoader program. Using a terminal program connected to the ESP-07, set the module to STATION mode and set the Access Point SSID and Password with the following Lua commands:
```
wifi.sta.getip()
wifi.setmode(wifi.STATION)
wifi.sta.config("SSID","password")
print(wifi.sta.getip())
```
Or, using LuaLoader, fill-in your SSID and password, then press "Set AP". Next, check that you are connected with "Get IP".
