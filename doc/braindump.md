
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

Components
==============

Sensors
-----------
Prices from Farnell for small quantities.

* Temperature. 1/2 - 1 USD.
* Moisture. 1-4 USD
* Proximity. Hall effect sensor=1/3 USD, switch= 1 USD.
* Distance. Ultrasound = 3-5USD. IR=10 USD?
* Light. Ambient. 1 USD.
* Accelerometer. 1-2 USD
* Touch. Can be done in uC SW, using a piece of chassis as plates. Dedicated circuit= ? USD
* Motion. PIR= 5 USD
* Sound. SPL= ? USD, audio-recording= ?
* RFID. Tag= 1/2 USD?, reader= ? USD
* Pressure?
* Weight?

Communication
-----------
Devices should be able to communicate directly with eachother, to collaborate as
equals on tasks. But, it should also be possible for them to take part in a centrally
controlled network, and act as a slave of a host.

* IR receive. TSOP382/TSOP85/SEN-00241. 1/2 - 2 USD
* 433Mhz. 
* 2.4 Ghz. NRF24+, BT classic, BT 4.0/low-energy?

Want to communicate with:
* Keyboards/mice. 
* Weather stations, alarm clocks.
* TV/HiFi remotes
* Systems sending RTC
* Home-electronics switches

Battery
-----------
LiPoly probably. Standard JST connector.
Built-in charging, via USB?
Wireless charging? QI-standard

Storage
-----------
16 MB FLASH = 1 USD
X GB microSD = 4-5USD. Holder = 1-2USD…


Actuators
-----------
Actuation is almost by necessity specific to the device one wants to control..
And will in most cases require physical contact, challenging to weather proof.
Communicate with existing systems to actuate?


Microcontroller
---------------
Arduino-compatible is nice. Use an OSHW as base for PCB layout.
AtMega 32u4 / Leonardo?
If we want to enable all the sensors above, might need to step up to a ARM Cortex M0+


Misc
-------
USB connectivity for flashing. Just use PCB directly for this?


Software
=========

Key areas
* Statistics
* Visualization
* Event-detection

Enable
* Combine data from different sensors, and other data sources
* Create event triggers from one-or-more conditions on data, both real-time and after-the-fact
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



