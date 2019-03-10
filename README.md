# MPU6050_ESP8266_MQTT

A project to send acceleration (vibration) values from a MPU6050 sensor as MQTT messages through a ESP8266 module.

The project consists of these parts:
1.  Circuit diagram showing MPU6050 connected to a ESP8266 based nodeMCU module.
2.  Arduino sketch for the ESP8266.
3.  Steps to install and configure a MQTT broker on a Windows computer.
4.  Steps to capture the values and store in a file in CSV format along with timestamp.
5.  Steps to visualize the data in a chart in real time using MQTT-Spy.

## Hardware
nodeMCU (ESP8266) module
MPU6050 sensor
Cell phone charger or powerbank
Windows laptop
WiFi router

## Connections
![alt tag](https://github.com/tangophi/MPU6050_ESP8266_MQTT/blob/master/MPU6050_ESP8266.PNG)

## Power
The circuit can be powered either by a cell phone charger (5V) or a power bank.

## Arduino Sketch
The Arduino sketch to upload to the nodeMCU module is available in the MPU6050_DMP6_ESP8266_MQTT folder.

### Pre-requisites:
1. Arduino is needed to program the nodeMCU module.  Download and install Arduino from https://www.arduino.cc/
2. ESP8266 support must be configured in the Arduino environment.  For steps to configure ESP8266, follow this link: https://github.com/esp8266/Arduino
3. MPU6050 library must be installed in the Arduino.  To install the library, in Arduino, goto Sketch->Include library->Library Manager.  In Library manager, search for "MPU6050" and the install library made by Jeff Rowberg.



## MQTT broker

## Capture data and store in a file

## Visualize real time data in MQTT-Spy
