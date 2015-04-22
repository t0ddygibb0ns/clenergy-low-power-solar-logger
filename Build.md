So here is my bare board mounted in the enclosure with double sided tape.

![http://clenergy-low-power-solar-logger.googlecode.com/files/image001.jpg](http://clenergy-low-power-solar-logger.googlecode.com/files/image001.jpg)

(If you look closely I have added a retaining clip for the battery in the Real time clock - I broke it when I tried (badly) to remove the battery.  If you treat it right, you should need to anything like my paperclip fix).

I wanted my build to be neat and easily to assemble / disassemble, so I bought a small freetronics prototype board, (also sourced from Jaycar), made for the EtherTen.  I also bought a few connectors and some LEDs to show status.  I have seen other builds that use small LCD shields to provide status messages, but my approach is simple and effective, and can be implemented with little code.

## Wiring Diagram ##

Here is a basic diagram of connections (External reset switch is not shown)

![http://clenergy-low-power-solar-logger.googlecode.com/files/Circuit.jpg](http://clenergy-low-power-solar-logger.googlecode.com/files/Circuit.jpg)


## Layout ##

![http://clenergy-low-power-solar-logger.googlecode.com/files/image010.jpg](http://clenergy-low-power-solar-logger.googlecode.com/files/image010.jpg)

Note that I use the softserial connectors (pins 2 & 3) rather than using the hardware serial.  This is so that I can use a serial monitor available from the Arduino software development tool to monitor what is going on.  With the board connected to either a test rig or the real inverter, a PC connected to the miniUSB at the front of the board, activate the serial monitor to see a trace from the loaded program.

The underside of the prototype board
![http://clenergy-low-power-solar-logger.googlecode.com/files/image002.jpg](http://clenergy-low-power-solar-logger.googlecode.com/files/image002.jpg)

MAX232 and RTC connected
![http://clenergy-low-power-solar-logger.googlecode.com/files/image006.jpg](http://clenergy-low-power-solar-logger.googlecode.com/files/image006.jpg)

LEDs and front faceplate, with external reset switch also connected:
![http://clenergy-low-power-solar-logger.googlecode.com/files/image007.jpg](http://clenergy-low-power-solar-logger.googlecode.com/files/image007.jpg)

The final product assembled:
![http://clenergy-low-power-solar-logger.googlecode.com/files/image009.jpg](http://clenergy-low-power-solar-logger.googlecode.com/files/image009.jpg)