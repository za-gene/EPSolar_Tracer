# EPSolar_Tracer
This repo has a few different implementations and tools for communicating with EP Solar Tracer charge controllers.
This has been tested with Tracer model 3210A, but should work with any EP Solar Tracer model that uses Modbus RS485 and MT50 displays.

There are 2 different Modbus libraries for Python that work well, pymodbus and minimalmodbus. libmodbus is a library for C that others have used with Raspberry Pis.

## Raspberry Pi Mobel 3 B+

### Via USB port
This uses a USB to RS485 converter. This does not work with the manufacturer's recommended cable (Model: CC-USB-RS485-150U) but I did get it to work easily with a ch340T chip model.

### wiring
RJ45 blue => b
RJ45 green => a

#### ch340T specs
* https://hackaday.com/tag/ch340/
* http://fobit.blogspot.com/2014/11/ch340g-in-eagle.html
<!--
#### install steps
* sudo apt-get install git
* sudo apt-get install python-pip
* pip install pymodbus
* pip install serial
-->
### Via GPIO
This method uses a Max485 and a 5v to 3.3v level shifter. I have not realized this version, but it should be doable if you need to free up USB port for whatever reason.

Some GPIO resources
* https://learn.sparkfun.com/tutorials/txb0104-level-shifter-hookup-guide?_ga=2.223672476.663927220.1545672234-707983221.1543353897
* https://spellfoundry.com/2016/05/29/configuring-gpio-serial-port-raspbian-jessie-including-pi-3/
* https://www.instructables.com/id/How-to-Use-Modbus-With-Raspberry-Pi/
* https://doc.homegear.eu/data/homegear-homematicwired/configuration.html#config-rs485-serial
* https://www.raspberrypi-spy.co.uk/2018/09/using-a-level-shifter-with-the-raspberry-pi-gpio/

## Arduino Uno & Max485
This works well. It's a pretty easy implementation. I'm using software serial to free up the USB port for serial communication with a computer or whatever you want. In the future I may build it out as a library.

![arduino max485](https://github.com/alexnathanson/EPSolar_Tracer/blob/master/images/arduino_Max485_wiring.jpg)


You can monitor the serial port from the Arduino IDE or serialTest.py (serialTest.py is a simple alternative if you can't get the Tracer to communicate directly with the Raspberry Pi)

This uses the Modbus Master library. https://github.com/4-20ma/ModbusMaster

## Win 10 PC
This is the simplest implementation. Uses the manufacturer recommended RS485 to USB cable (Model: CC-USB-RS485-150U).

In device manager right-click on the port and select properties. In the port settings tab make sure RS-485 is checked and the BPS is set to 115200. The other settings I used were databits = 8, parity= None, stopbits = 1

Both minimalmodbus and pymodbus libraries work well with my PC.

## Resources & Prior Work
https://github.com/kasbert/epsolar-tracer <br>
http://www.solarpoweredhome.co.uk/

## Links
Tracer charge controller
https://www.epsolarpv.com/product/3.html

Tracer Modbus Protocol
http://www.solar-elektro.cz/data/dokumenty/1733_modbus_protocol.pdf

