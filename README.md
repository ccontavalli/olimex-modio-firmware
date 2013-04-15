What is this?
=============

  This repository contains a copy of Olimex's mod-io firmware, both in
source and binary form, including documentation.

  mod-io (https://www.olimex.com/Products/Modules/IO/MOD-IO/) is an expansion
board usable from arduino, raspberry pi, olinux, and a variety of other
platforms that provides 4 relays, 4 digital inputs, and 4 analog inputs.

  The full specs are available in the documentation in this repository,
and on Olimex own web site (http://www.olimex.com/).

  For the board to run, it needs to have a valid firmware installed. This
firmware is generally shipped pre-installed on the board itself, but is
also available for download from the olimex web site. 
  
  Unlike many other companies on the market, Olimex Ltd not only provides the
firmware in binary form, but provides the full source code under GPL license,
meaning that anyone can easily modify the firmware to provide more features
or address specific needs.

  In this repository we started off with the original firmware provided by
Olimex. Over time, you will see different changes and branches to experiment
with additional features and various code changes. Stay tuned!


How to compile the firmware
===========================

Make sure you have avr tools installed:

    $ sudo apt-get install gcc-avr avr-libc 

You should now be able to compile individual files by using:

    $ avr-gcc -mmcu=atmega16 -c ./DemoSoft.c

To compile the firmware, run:

    $ cd build; make

You should have a file 'firmware.elf' as output.
