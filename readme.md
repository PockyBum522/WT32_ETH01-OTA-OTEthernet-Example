## Prerequisites

All of this is done with Arduino IDE 2.0.0-rc9.4 or later

## How to connect FTDI and upload

Short GPIO 0 to GND any time you are about to upload.

Set FTDI board to 5v and not 3.3v

FTDI > WT32-ETH01

RX   - TX0
TX   - RX0
GND  - GND
VCC  - 5V

Select ESP32 Dev Module in Arduino IDE

When done programming, unshort GPIO 0 and GND and repower to actually run sketch

## Getting Ethernet example running

Install the latest ESP32 board using the instructions and stable release link at https://docs.espressif.com/projects/arduino-esp32/en/latest/installing.html

Install https://github.com/khoih-prog/WebServer_WT32_ETH01/releases/tag/v1.5.0 or newer

Open File > Examples > WebServer_WT32_ETH01 > HelloServer

Update myIP and myGW (Gateway) at top of code.

Once uploaded, pull the GPIO0 short to GND and reboot the board. 

Navigate from a web browser to http://192.168.1.232/ (Or whatever you change myIP to)

You should see "Hello from HelloServer running on WT32-ETH01" in your browser

## Getting basic MQTT example working:

Install https://github.com/plapointe6/EspMQTTClient and its dependency, PubSubClient

Open File > Examples > WebServer_WT32_ETH01 > 

Update myIP, myGW, const char* mqttServer, const char *ID, const char *TOPIC, and const char *subTopic

Also change line 76 to: if (client.connect("arduino", "[YOURUSERNAMEHERE]", "[MQTTPASSWORDGOESHERE]"))

Upload, run

## Getting OTA over Ethernet working

Install https://github.com/ayushsharma82/AsyncElegantOTA

Install https://github.com/me-no-dev/ESPAsyncWebServer

Install https://github.com/me-no-dev/AsyncTCP

Open MQTT_And_OTEthernet_Example.ino

Upload, run. Take note of what IP the board is on, you should be able to see this both in the serial monitor and in the MQTT messages when the board first starts.

You should see some test MQTT messages on *TOPIC

Now, change something in the sketch, such as the vXX number down in data

Save the sketch

Go to Sketch > Export compiled binary

You should now see a build folder next to the MQTT_And_OTEthernet_Example.ino file

Go into build\esp32.esp32.esp32

The file you will be uploading to do an OTA update is MQTT_And_OTEthernet_Example.ino.bin in that folder

