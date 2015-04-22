# My code #

I did a few programming courses around 10 years + ago, and I've never used C.  My code works, but I would guess that it doesn't represent best practice.

I used the Arduino dev tool version 1.0.1 to develop the code - Downloaded from here:
http://arduino.cc/en/Main/Software.  You will need this to upload your code.

The following standard libraries (included with the dev tool) were used:
  * EEPROM
  * SPI
  * Ethernet
  * Wire
  * SoftwareSerial
  * SD
  * avr/sleep


In addition, the following libraries were used (available free from various sources) and you will need to download and install these:
  * Time (from http://www.arduino.cc/playground/Code/Time)
  * DS1307RTC (Included with the above time library)
  * PString (from http://arduiniana.org/libraries/PString/)


# Reference code used to assist development #

My code has been developed based on a range of tutorials from the Arduino web site (arduino.cc).

In addition I need to give credit to a range of other projects and information sources that were used to assist with this project:
  * http://reisfun.wordpress.com/  and http://libpowercom.sourceforge.net/ - For reverse engineering of the serial comms protocol

  * http://michaelnoland.com/reducing-code-size-on-arduino-ethernet-boards/

  * EngBlaz - For information on sleep libraries, functions and interupts - http://www.engblaze.com/hush-little-microprocessor-avr-and-arduino-sleep-mode-basics/

  * Arduiniana - For the PString library and a guide to use it.  Required to create a log file based on the current date - http://arduiniana.org/libraries/PString/



# Arduino coding issues #

To reduce sketch size, I have not used DNS calls to PVOutput.org.  Nor am I using DHCP.  Both add significantly to the binary code size.

Disabling DNS services if they are not used further reduces the compiled binary size.  Use the guide refernced above to achieve some significant savings - Around 3k.

(**Note** some of the libraries (Client.h and Udp.h)  that need to be updated are located in the directory structure under the Arduino development environment tool and all changes in the guide must be applied to avoid complier errors).

Also, the bootloader on my Arduino EtherTen board had issues with uploading sketches over around 28k, even though they shouldn't be any problem for the board.  To resolve the issue, I needed to update the bootloader (the version in this thread worked for me - http://forum.freetronics.com/viewtopic.php?f=4&t=338&sid=4125253e76802aab3b7d8f16ce98eb3f
You need another Arduino board, or you can use an ISP to upload the code.  I borrowed a USBtinyISP to do the job.  You can source them from ebay for around $10.

# Implementation #

Two key programs exist:

## Clenergy\_Loader ##
Used to load a number of strings into non-volatile memory used for generating and processing requests.  You need to update 3 key items in this code:
  * The serial number of your inverter.  If you run the code with the Arduino properly connected to the inverter, this should be automatically populated (Written but not tested - It should work, but I just hard-coded my SN so I didn't really try it out.  If it doesn't work, the SN is available from the serial monitor trace from the main code.  Even if the loader program doesn't store everything, that bit should still work for you to determine the SN)
  * API-Key - Obtained from PVOutput when you register your solar system and activate auto-updates.  **Note** that you should also change the update frequency on the PVOutput page to 5 Min to match my code.
  * SID - A 4 character system ID also from PVOutput

## Clenergy\_Logger\_0\_1 ##
Used to get data from Clenergy inverter using serial connection, writing to SD card and uploading WattHrs and MaxWatts - both at 5 minute intervals.

Changes required to configure code:
  * Update boolean variables near the top of the code to select Temperature and/or Volts upload - Set to "true" or "false" (No quotes  and case is important)
  * Update IP address for Arduino - It must be unique in your network
  * Update the gateway address to the value relevant to your network

**IMPORTANT** - This program will not run without an SD card present.  It will run without a network connection, but will only log to the SD card.  The SD card must be formatted FAT or FAT32 (I used FAT32) and **must** have a directory "PV" in the root of the SD card.

Each day will be logged to a separate file in the format
> \PV\YYYYMMDD.CSV.

**IMPORTANT** - You need to set the date on the RTC board for the file date to be correct.  There is sample code on with the [time library page](http://www.arduino.cc/playground/Code/Time) of the Arduino site that you can use.  Either sync to your PC time or you can use a NTP server.

You can plug it in at any time and it will start logging from then, provided the panels are generating power.  If not, it will try to connect for around 15 minutes, then will go to sleep.  When generation starts again, it will wake up and start logging.

# Status lights #
**Power**   On at startup  - Fast flash at RTC sync & left on when running Ok.   Slow flash if RTC sync fails

**LAN**    On after Ethernet start.  Fast flash when uploading to PVOutput.  Left on when running Ok.

**SD**    Slow flash if SD init fail.  Fast flash on SD access.  Left off in normal operation.  If left on - SD error condition and nothing more is logged (try power cycle to fix)

**Serial**    Slow flash - Polling for initial connection.  Medium flash - Polling for logon.  Fast flash - Polling for data.  On - waiting for next inverter poll (every half second).