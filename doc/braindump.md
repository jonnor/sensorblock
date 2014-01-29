
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

Size should ideally be 40x40x10mm (or smaller), 50x50x15mm acceptable?

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
* Pressure?
* Weight?

Radiocomm
-----------
* IR receive. TSOP382/TSOP85/SEN-00241. 1/2 - 2 USD
* 433Mhz. 
* 2.4 Ghz. NRF24+, BT classic, BT low-energy

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
