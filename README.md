# Sensor-3
Sensor 3, Water Presssure, Moisture and flow sensor. 


Version 3 rev-5b Specifications:
•	Option for  a Rockerscream Mini Ultra Pro V2 M0 CPU board with a RFM95 LoRa radio. Li-ion battery charger, EUI64 ID chip. Low Power operation, ATSAMD21G18A M0 CPU, 2MB serial flash. 

Or it can use an Adafruit Feather processor board:
o	Feather HUZZAH32 With a ESP32 WiFi, BT chip
o	Feather M0 ATSAMD21 RFM95 LoRa Radio
o	Feather M0 WiFi ATSAMD21 + ATWINC1500
o	Feather adapter for Teensy 3.2 CPU
o	MCCI Feather with  STM32L082 CPU

•	It measures soil moisture with up to 8 sensors. (not with some Feather boards)
•	External DS18B20 for soil and/or air temperature.
•	MCP9800 and/or Si7021 (+humidity) temperature.
•	BME280 and/or BME680 environmental sensors
•	Support of a water pressure sensor via an analog port.
•	Has support a flow/water meter with a pulse debouncing circuits.
•	Solar-battery Powered or via external 8 to 28v AC or DC supply.
•	Two places for FRAM, EEPROM memory, security chip or other I2C devices.
•	Connection for external I2C devices.
•	Connection for an optional daughter board
•	Fits in a Bud PN-1323-CMB or PN-1328-CMB case.
•	Software controlled power switch for external devices.
•	Added a socked for an RCR123A rechargeable Li-Ion battery.
•	Support for K – Offset style flow sensor.

Connector P2, break out serial-1 to an FTDI 6pin connector
Connector P3 breakout I2C signals for external use
Connector P4 allow for a daughter card

The details:
Power supply: 
External power is fuse by a PTC device F1, limiting the total current to about 500ma, the input power is converted to +5 by a TI LM2842, 600ma switched regulator. Input power can come from external connection via J1, or via USB or via solar-battery. . If needed, a TC1262 LDO, U15, can be added for additional power if needed at 3.3V for external devices.

If battery-solar power is used, a 6V solar panel can be connected to J2. U2, a Microchip MCP-73831-2, provide proper charging from the solar panel to an external Li-Ion or LiPo 3.7V battery that is connector to the connector on the Rocketscream or on some Feather processor board. Or to an optional RCR123A, 16340 rechargeable battery mounter on the board. Charging is for Li-Ion or Li-Po ONLY, this will not support charging of LiFePO4 battery’s. Voltage monitoring of the battery can be made via an analog channel resistor divider on the CPU module.

The board has an optional power switch U10, a Microchip MIC2019 use to power external sensors that can be control via software to reduce power when the CPU is sleeping. It also limits output current to about 500ma, but can be adjusted via R30 . R28 or R29 can be used to select 5V or 3.3V as source of power for U10.
As an option we can supply the VIN voltage via diode D12 and F2 to supply VIN to external device like K-Offset flow sensors that may require a higher voltage for operation.
Pulse Circuit:
A pulse output from a flow or water meter can be connected to J2. This connected can be condition by two optional circuits. U4, a MAX6816, digital signal debounced chip that can debounce a signal of up to about 15Hz. Or a circuit using D16, an Op-Amp used to detect the pulse from a K-Offset type flow sensor. R17 is used to bias the sensor and is voltage dependent. R37 and R38 are used to select the circuit to be use and connect it to U8 buffer, then on to the CPU. Removing U16 and selecting values as needed for resistors for R34, R31 and R38, with C10, C34, you can use the pulse-in signal direct to the CPU.
External temperature:
An DS18B20 temperature sensor, can be connected to J2, AIN-0 pin with R18 providing bias voltage, and scaled by R1, R2 and C1 as needed. 
AIN-0 can also be uses as a general purpose analog input, for used with a pressure sensor or other device. Or use as a digital in/out pin.
Sensor’s:
The board can use a number of optional sensor’s mounter on the board: U3, is a Microchip MCP9800 temperature sensor, U7, a Silicon Labs SI7021 temperature and humidity sensor, U11, a Bosch BME-680 environmental sensor with VOC gas, humidity, pressure and temperature, and U12, a Bosch BME-280, for temperature, barometric pressure and humidity.
I2C devices: 
U13 and U14 can accommodate a number of standard I2C device’s in SOIC-8 packages from FRAM’s, Ram, EEPROM, Crypto chips, etc. For general use, U13, is fitted with a FM24CL64 FRAM and U14, a 24AA025E64 EUI64 chip that can provide a unique 64bit serial number.
Analog Mux: 
An 8 channel analog mux is install at U6, it can be used to route signals to the ATD converter channels A0-A3 or as digital input. Note: In normal configuration, it is set up to provide a special AC volt meter bridge circuit for sensing water moisture on 4 of its channels, or it can be configure as an 8 Channel Analog Mux or an 8 Channel digital input Mux.  Some Feather board like the ESP32 do not have the correct pin-out option to support this function.
Notes: 
The EUI64 chip that is mounted on the Rocketscream CPU, uses address 50h57h, preventing use of FRAM or other devices that use this address space. It will be replaces in a future version of the CPU board with a 24AA025E64 device that will lock its address to 50h only. For now, you can remove the chip from the CPU board when using a FRAM and use U14, with a 24AA025E64 chip to provide the EUI64 serial number..

The 3.3V Power supply on the Rocketscream, can only source 250ma for all operations.

This board has been used with LMiC LoRaWAN and MCCI stack on the TTN network and with the MySensor software stack to a MySensor LoRa gateway.

Pinouts of Feather and MCCI board may differ from what on the schematic. 
If using ESP32 processor, there are restriction on some pins when using WiFi.


What’s different between Version 2 and 3 Boards:
Using a Feather Modules.

•	The Feathers CPU do not have a EUI64 chip. 
•	The ratio of the battery monitor resistor’s is different. 
•	No serial flash on CPU. 
•	Serial-1 is not on all feather boards. 
•	Rx and Tx LED are not connected to feathers boards.. 
•	The LoRa Feather requires an external jumper to work with LoRaWAN. (R24-zero ohms) 
•	Pin-out varies with difference Feather processors board, Use caution! 

Other changes:

•	ID0 and ID1 are not available. 
•	Pin-out are different between the feather boards and the Rocketscream CPU’s. 
•	Real Time Clock and it’s battery are no longer supported. 
•	We are using a larger Bud PN-1323-CMB or PN-1328-CMB case. 
•	J2-4 is available for general use. It is no longer a GND pin. 
•	Most parts are locate on the bottom of the board to allow for better cables access. 
•	On board RCR123A rechargeable battery.
•	Allow for connecting of K-Offset flow sensors.
•	Connectors P1 and P3 for external I2C devices or daughter board.


Changes Sensor 3, Rev-5a to Rev 5b

•	Removed Q1, was not needed
•	Added D12 and F2 to provide higher voltage bias for K-Offset flow sensor.
•	Removed D13, was not needed
•	R17 changes to 1206 package
•	Added socket for an RCR123A Li-Ion battery
•	Moved C4 to other side of F1
•	Remove pulse circuit D12, R15, C16, U8
•	U8 added to condition pulse circuit
•	R17 and R18 added to select pulse circuit 
•	C8 changed to 1206 package, C3, C27 to 1210
•	


https://www.adafruit.com/product/3405
https://www.adafruit.com/product/3178
https://www.adafruit.com/product/3010
https://www.rocketscream.com/blog/product/mini-ultra-pro-v3-with-radio/
https://www.budind.com/pdf/hbpn1323mb.pdf
https://store.mcci.com/products/catena-4612-integrated-lorawan-node 
 

Moisture Sensor’s
This controller can be use with a number of different types of moisture sensor’s…
•	Irrometer 200SS-15 Watermark Soil Moisture Sensor.
•	RF based sensor’s like the Vegetronix VH400 and Soilwatch-10
•	Low cost Capacitive Soil Moisture Sensor, like the Dfrobot SEN0193 (and many more on Ebay/Amazon)
•	Home-Made Gypsum sensors.

Watermark 200SS:
The WATERMARK Soil Moisture Sensor measures electrical resistance inside of a granular matrix similar to gypsum to determine soil water tension. 
To measure resistance inside the sensor, a voltage divider circuit is used. The circuit uses a known input voltage, output voltage, and series resistor value to calculate the value of the sensor resistor in a bridge configuration.  Once the resistance is known, the value is calibrated to soil water tension value. Measurements are made with an AC style voltmeter with an alternating polarity to prevents building of a charge which both offsets the reading and degrades the electrodes over time. 
In this controller we have a 2 section of a  4-channel analog mux’s, an 74HC4052 (U6) that is connected to 2 ATD ports and 2 digital ports on the CPU with its bias resistors R11 and R12. By manipulating these signals we can build an AC bridge to read resistance of the 4 sensors. 
Home-Made Gypsum sensors:
Delmhorst GB-1 Gypsum Sensor Blocks: 
The operate very much the same as the Watermark sensor, but may require some calibration prior to use: See these reference on how to build them: 

https://www.youtube.com/watch?v=DP38vGFx6Ns
https://hackaday.io/project/6444/logs?sort=oldest
https://hackaday.com/2010/03/15/soil-moisture-sensing/ 

RF based sensor’s or Capacitive Soil Moisture Sensor: 
These sensors product a voltage that is proportional to the soil moisture. Up to 8 of them can be connect to the same mux’s as use for the gypsum sensors, but they just provide a direct path to the ATD converters. Power for them can be sourced from the board via the U10 power switch. Note: these devices can consume about 30ma each, so one needs to be concern about total power that is available with each power supply option.
Other Sensor’s:
The circuits on the board can also be used to connect almost any type of sensor, if they have a voltage output, I2C or simple digital interface.  PH, temperature, humidity, IR, light, sound, ORP, air quality PM2.5, gas, CO, Co2, wind etc.…
This board has many option and configuration that can be selected by adding or removing components on the board as needed. Not all parts need to be installed, but selected as needed for your needs.
Some reference on moisture sensors:
https://github.com/empierre/arduino/blob/master/SoilMoistSensor.ino
https://www.irrometer.com/pdf/sensors/403%20WATERMARK%20Sensor-WEB.pdf
https://www.irrometer.com/200ss.html
https://vegetronix.com/Products/VH400/
https://www.dfrobot.com/product-1385.html
https://pino-tech.eu/soilwatch10/
Delmhorst GB-1 Gypsum Sensor Blocks
https://hackaday.io/project/6444-vinduino-a-wine-growers-water-saving-project

 
Software
Depending on the processor board used, one can select from a number of software and networks options.
•	LoRaWAN via TTN using MCCI, Semtech or IBM LoRa stack
•	WiFi with option for E-mail, TXT messages , direct to a web page or via MQTT
•	Bluetooth
•	MySensor network
•	And many others…

https://stackforce.github.io/LoRaMac-doc/index.html
https://github.com/mcci-catena
https://github.com/matthijskooijman/arduino-lmic
http://mqtt.org/

