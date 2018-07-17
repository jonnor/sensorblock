
Usecases
===========
* Interactive installation.
* Ad-hoc home automation
* Ad-hoc construction machines
* Environmental monitoring
* Conducting physics experiments/demonstrations
* Human interface device for computer

Physical requirements
=======================
Quite informal specs...

Should be able to:
* Hold someone standing on it
* Lie out in the rain for a day
* Be dropped from 1-2 meter dozens of times
* Be mounted on vibrating motor/chassis for a day

* Be small enough to put in your trouser pocket
* Easy to mount on any flat surface, floor, walls, ceiling
* Be able to disassemble and reassemble with minimal tools in a couple of minutes
* Have a usable battery lifetime of 30 days

Similar devices
==============

* [Bosch XDK](https://xdk.bosch-connectivity.com).
8 different sensors, mostly environmental.
WiFi+BT connectivity. Integrated battery.
Cost: 180 EUR/unit.

* [z2amiller/sensorboard](https://github.com/z2amiller/sensorboard).
ESP8266 with various environmental sensors, available via OSHPark.

* [CMU Synthetic Sensor](https://www.cmu.edu/news/stories/archives/2017/may/internet-of-things-sensors.html).
[Website](http://www.gierad.com/projects/supersensor/).
Concept of integrated sensor-package, analyzed together using machine learning to detect events in a household,
one sensor covering one room.
"high-speed sensing is a big win for instantaneous environmental events"
"programming by demonstration." for end-user programming.

* [STM32 SensorTile](https://hackaday.io/project/19649-stm32l4-sensor-tile).
Very low power design, 1mA average. Bluetooth LE via external chip.

Components
==============

Sensors
-----------
Prices from Farnell for small quantities.

* Temperature. 1/2 - 1 USD.
* Moisture. 1-4 USD
* Proximity. Hall effect sensor=1/3 USD, switch= 1 USD.
* Distance. Ultrasound = 1-2USD. IR=6 USD?
[Sharp IR distance](http://www.banggood.com/3pcs-IR-Infrared-Ranging-Sensor-Distance-Detector-20-150CM-With-Matching-Cable-p-1123630.html?rmmds=search).
* Light. Ambient. 1 USD.
* Accelerometer. 1-2 USD
* Gyro.
* IMU. 6DOF=accel+gyro. 9DOF=accel+gyro+magnetometer. 10DOF=+bariometer. MPU-9250,
[MPU-9250 breakout](http://www.banggood.com/GY-9250-MPU-9250-Module-9-Axis-Sensor-Module-I2C-SPI-Communication-p-1059005.html?rmmds=search)
[Adafruit 9DOF](https://www.adafruit.com/products/3387)
* Touch. Can be done in uC SW, using a piece of chassis as plates. Dedicated circuit= ? USD
* Motion. PIR= 5 USD
* Sound. SPL= ? USD, audio-recording= ?
* RFID. Tag= 1/2 USD?, reader= ? USD
* Laser. Send/receive
* Ir/opto trans/recv, for beam crossing/object detection
* Pressure?
* Weight?

Communication
-----------
the Sensorblock primarily act as a pure sensors device, that is it:
senses and transmits the information to a central message broker (MQTT).

Application/business logic should subscribe to the messages at the broker,
process, store, and make the decisions.

These can then be sent to actuators, either:
* over the same message broker,
* via a gateway device,
* or another protocol

Gateway device(s) can enable the

* IR receive. TSOP382/TSOP85/SEN-00241. 1/2 - 2 USD
* 433Mhz. 
* 2.4 Ghz. NRF24+, BT, BTLE4.0

Want to communicate with:

* Weather stations, alarm clocks. 433Mhz
* TV/HiFi remotes. IR
* Keyboards/mice. USB/BT
* Systems sending RTC. 433Mhz? LF?
* Home-electronics switches. 433Mhz

This should be done preferably with standalone MsgFlo participant

Battery
-----------
LiPoly probably. Standard JST connector.
Built-in charging, via USB?
Wireless charging? QI-standard

Maybe skip internal battery in first version, instead allow USB battery to be used when needed.
And have a wide-range input power connector, 5-19V. Barrel jack

## Actuators

2-3 general-purposw power-outputs using H-bridges?
Can then be used for driving motors, speakers, solenoid/relays.

[H-bridge driver ICs](http://no.farnell.com/w/c/semiconductors-ics/power-management-ics-pmic/drivers-controllers/mosfet-drivers?driver-configuration=3-phase-bridge|full-bridge|half-bridge|half-bridgefull-bridge&range=exc-obs|inc-in-stock|exc-direct-ship&sort=P_PRICE)


Storage
-----------
16 MB FLASH = 1 USD
X GB microSD = 4-5USD. Holder = 1-2USD…


Microcontroller
---------------
Arduino-compatible is very nice to have. 
Integrated connectivity preferred, like WiFi or BT.

Adafruit makes a nice board which integrates USB+LiPo power,
the [Feather Huzzah ESP8266](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266).

In the same "Feather" series, they also have microcontrollers with LoRa, Bluetooth LE and GSM connectivity.
They have a "FeatherWing" extension board concept.
Could be a good first target to create a compatible board.

WiFi-capable

* ESP8266. Really cheap, widely available
* ESP32. WiFi+BLE4.0. Powerful, nice pheripherals (captouch,hallsense,analogamps)
* [EMW3165](https://www.seeedstudio.com/EMW3165-Cortex-M4-based-WiFi-SoC-Module-p-2488.html)
* [RTL8710](https://www.banggood.com/search/rtl8710.html)

Misc
-------
USB connectivity for flashing/charging. MicroUSB is the standard.
Alt lowcost, use PCB directly to make dongle? Impractical in that a connector has to stick out.


# First-run experience

Preconfigured to talk to a cloud-hosted MQTT broker.
Have to input connection details so it can get online.
Includes a Flowhub IoT basic/trial subscription.
Click live-URL to connects to a hosted MsgFlo instance for that broker.
Can see sensor data, add adapters, send data back to device.
Some example flows should be ready, just plug in to see demo.

# Firmware

Implemented with MicroFlo, components/graphs doing the configurable sensor processing. 
In advanced mode, allows uploading new/custom graphs.

Sensor processing params should be adjustable over MQTT (in additon to webui).

## Webinterface

Webinterface allows configuring:
1) Connection details. WiFi SSID/password/mode, MQTT server/username/password/certs, Flowhub IDE url
2) Parameters for the on-edge algorithms. Readout-rate, filter frequencies, trigger thresholds, ...
3) If a kit/extensible, pin mappings for added hardware

Button needed to enter/enable editing-mode?
At least for critical things like connection info.
Can also enable full reflashing (OTA/USB).
Physical security...

Firmware should be based on MicroFlo. 

# Tooling

Key areas
* Statistics
* Visualization
* Event-detection

Enable
* Combine data from different sensors, and other data sources
* Create event triggers from one-or-more conditions on data
* Viewing multiple data streams


Device handover/substitutions
=============================
Idea: swapping a Sensorblock should be as simple as changing a lightbulb or battery!

For devices which are in continious operation, but are battery powered - there
will be at some point be a need to replace it. If battery times are short, which might make
the system simpler and cheaper, replacements would need to happen fairly often.
If an existing device could, upon the arrival of a new potential replacement device, hand over
its job with minimal user involvement - this would perhaps make this acceptable.

Couple with wireless charging of blocks when they are not in use.

There would of course be a need for a device to notify when it is in need of a replacement.


Relationship with Arduino-like devices
===============================
Arduino provides cheap, standardized microcontroller boards which are programmable
- but they do not include any sensor or actuator pheriperals, and does not solve any
of the mechanical challenges faced when making a thing.
Also, it is conceived as "the" controller of a project, not so much geared towards collaboration in larger systems.


Documentation & Artifacts
========================
Needs to cover the entire process of making a Sensorblock.

* Purchase: Bill-of-materials, sourcing info/tips
* Electronics prod: PCB schematics, layout, milling toolpaths
* Enclosure prod: CAD files, CNC/3d toolpaths, tips
* Assembly: instructions
* Software: Toolchain install, bootloader, firmware install
* QA: Testing process(es)

Use a build-process, like one would do with software.
Do continious integration and testing, using Travis CI.
Do releases with all of the artifacts.

Question: how can we automatically verify non-software components, continiously?

