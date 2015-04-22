# Hardware #

After a little research, I selected this Freetronics Arduino board sourced from my local [Jaycar Electronics](http://www.jaycar.com.au/) (around $70).  Its basically and Arduino Uno model with onboard Ethernet and SD card storage (rather than having to use a separate add-on board - known as a "shield".

http://cdn.shopify.com/s/files/1/0045/8932/products/etherten-top-002_large.png?101689

[Freetronics web site](http://www.freetronics.com/collections/all-products/products/etherten#.UD4P3qM4kdh)

(Next time a better option may be a bare Uno board or maybe something with more space for programs (called "sketches").  These are available through DealExtreme for under $20.  Using a WiFi shield (around $60 or $70 I think) I could probably have put everything outside with the inverter rather than dealing with cabling to inside - See below)

Clenergy inverters offer both USB and RS232 communication through ports located at the bottom of the inverter.  Through research, the initial connection through the USB is reported as somewhat unreliable.  Also, I wanted to extend the connection inside, and the reliable range of RS232 connections is much greater than USB anyway.  So RS232 was the way to go.

Arduino boards also support Serial comms (that's what RS232 is), but I also found out that direct connection would fry the Arduino.  I needed a board to manage the voltages down to Arduino levels.  A "MAX232" board is the easy solution, available from ebay for around $6 delivered (just search for MAX232 on the ebay site).  I looked for the smallest one that would fit is my enclosure that was also from [Jaycar](http://www.jaycar.com.au/), and bought this one.

[![](http://www.nbglin.com/cpjsimage/rs232a2.jpg)](http://www.nbglin.com/rs232.htm)

On reflection, there was another longer but narrower one that may have fitted better for the same money.  But I just ended up adjusting the placement of this one in the case.

I haven't done any programming for quite some time, and had never used C, so I started working through the examples and tutorials available from the Arduino site (arduino.cc).  I soon found out that space on these things is quite limited, both for the compiled program and in terms of processor memory.  The Uno has only 32K for storage of the compiled sketch (Other models have more, and they would allow more functionality to be coded.  Anyway, I still got my project to do all I really wanted it to do).

I was initially going to use a time server from the Internet to set the time for data logging.  And I got that to work with a sketch that used around 17k of storage.  So I gave up on that and bought a Real Time Clock board (from ebay for around $6) like this to help me reduce the code I needed.

![http://thumbs2.ebaystatic.com/m/m4hXmnaqM7Yij1JE37c6pDg/140.jpg](http://thumbs2.ebaystatic.com/m/m4hXmnaqM7Yij1JE37c6pDg/140.jpg)

A more accurate Freetronics unit is available through Jaycar (for $30), but it only needs to be about right.  PVOutput round the time to the nearest 5 minutes so loosing/gaining a second a week won't make much difference.