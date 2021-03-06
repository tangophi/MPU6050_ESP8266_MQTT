# MPU6050_ESP8266_MQTT

A project to send acceleration (vibration) values from a MPU6050 sensor as MQTT messages through a ESP8266 module.

The project consists of these parts:
1.  Circuit diagram showing MPU6050 connected to a ESP8266 based nodeMCU module.
2.  Arduino sketch for the ESP8266.
3.  Steps to install and configure a MQTT broker on a Windows computer.
4.  Steps to capture the values and store in a file in CSV format along with timestamp.
5.  Steps to visualize the data in a chart in real time using MQTT-Spy.

## Hardware
* nodeMCU (ESP8266) module
* MPU6050 sensor
* Cell phone charger or powerbank
* Windows laptop
* WiFi router

## Connections
![alt tag](https://github.com/tangophi/MPU6050_ESP8266_MQTT/blob/master/images/MPU6050_ESP8266.PNG)

## Power
The circuit can be powered either by a cell phone charger (5V) or a power bank.

## Arduino Sketch
The Arduino sketch to upload to the nodeMCU module is available in the MPU6050_DMP6_ESP8266_MQTT folder.

### Pre-requisites
1. Arduino is needed to program the nodeMCU module.  Download and install Arduino from https://www.arduino.cc/
2. ESP8266 support must be configured in the Arduino environment.  For steps to configure ESP8266, follow this link: https://github.com/esp8266/Arduino
3. MPU6050 library must be installed in the Arduino.  To install the library, in Arduino, goto Sketch->Include library->Library Manager.  In Library manager, search for "MPU6050" and the install library made by Jeff Rowberg.

### Modify Sketch for your environment
In the MPU6050_DMP6_ESP8266_MQTT.ino file, find these lines:

```
const char DEVICE_NAME[] = "mpu6050_1";
const char mqtt_topic_csv[] = "/mpu6050_1/csv";
const char mqtt_topic_json[] = "/mpu6050_1/json";

const char* ssid = "XXXXX";
const char* password = "YYYYYYY";

// IP address of your MQTT server
const char* mqtt_server = "192.168.0.114";
```

Update the 'ssid' to the SSID and 'password' to the password of your WiFI router.
Update the 'mqtt_server' to the IP of the computer running the MQTT broker.  More details of MQTT broker in the next section.
In case there is more than one circuit in your environment, update the 'DEVICE_NAME', 'mqtt_topic_csv' and 'mqtt_topic_json' to be unique for each circuit.

The sketch sends the same data on two different MQTT topics.  In the first topic (/mpu6050_1/csv), it is sent as a CSV (comma separated values) string.  In the second topic (/mpu6050_1/json), it is sent as a JSON string.

Upload the sketch to the nodeMCU module.  Once the sketch is uploaded, the nodeMCU will start reading vibration data from the MPU6050 sensor and start sending MQTT messages.

## MQTT broker
A MQTT broker is needed to get the MQTT messages generated by the nodeMCU module.  The simplest MQTT broker is the mosquitto broker and can be downloaded from https://mosquitto.org/download/.  Follow steps in http://www.steves-internet-guide.com/install-mosquitto-broker/ to install and configure the MQTT broker on your Windows computer.

Once the broker is installed and started, you can see the messages coming in from the nodeMCU with the following command in a 'Command prompt' window.  In the command the -h parameter (192.168.0.114) is the IP address of the computer running the MQTT broker.  In most cases, it will be the IP of your Windows computer.  This should be the IP address given as the 'mqtt_server' in the Arduino sketch.  The -t parameter (/mpu6050_1/csv) is the MQTT topic and should be the same as the 'mqtt_topic_csv' in the Arduino sketch. 

![alt tag](https://github.com/tangophi/MPU6050_ESP8266_MQTT/blob/master/images/mosquitto_sub.PNG)

In each line of the above output, the first value is the timestamp, followed by the acceleration values in X, Y and Z directions.

## Capture data and store in a file

To capture the MQTT data to a file, the following command can be used.  Once the command is issued, it will collect and save the data till the command is stopped by issuing a 'Ctrl-C'.

In case there are multiple sensors, issue a separate command to capture data from each sensor and specify different files to store the data.


![alt tag](https://github.com/tangophi/MPU6050_ESP8266_MQTT/blob/master/images/mosquitto_sub_save_to_file.PNG)

After stopping the above command by issuing a 'Ctrl-C', the text file can be opened in Notepad to see the saved data.

![alt tag](https://github.com/tangophi/MPU6050_ESP8266_MQTT/blob/master/images/sensor1.txt.PNG)

This data can then be imported into Excel as a CSV formatted input.

## Visualize real time data in MQTT-Spy

This is optional and not really needed to capture data from the sensors.  This is needed just to see how the incoming data looks like.

To visualize the data in real time, MQTT-spy software can be used.  Download a JAR file of MQTT-Spy from https://github.com/kamilfb/mqtt-spy/wiki/Downloads .

Open the JAR file.  Click on Connections->New Connections.  Enter the IP address of the MQTT broker (192.168.0.114) in the 'Server URI' field and then click on 'Open Connection'.

![alt tag](https://github.com/tangophi/MPU6050_ESP8266_MQTT/blob/master/images/mqtt-spy-new-connection.PNG)


A connection to the MQTT broker is now opened.  Subscribe to the MQTT topic by clicking on 'New' in 'Subscriptions and received messages' section.  Enter the MQTT topic, '/mpu6050_1/json', in the 'Topic filter' field and click Subscribe.

![alt tag](https://github.com/tangophi/MPU6050_ESP8266_MQTT/blob/master/images/mqtt-spy-new-connection.PNG)


Now you should be able to see the messages received from the nodeMCU containing the acceleration values in X, Y and Z directions.  To chart this data, right click on the '/mpu6050_1/json' topic in 'Received messages summary' section and click on Charts->Show payload values for this topic.  In the 'Message content chart' window, click on the 'Add' button.  Enter the values as shown.  This is for the X axis.  Add for Y and Z axes too.

![alt tag](https://github.com/tangophi/MPU6050_ESP8266_MQTT/blob/master/images/mqtt-spy-chart_configure.PNG)


Once all the axes are configured, the incoming acceleration values will be displayed in the Message Content Chart window.

![alt tag](https://github.com/tangophi/MPU6050_ESP8266_MQTT/blob/master/images/mqtt-spy-chart_display.PNG)


