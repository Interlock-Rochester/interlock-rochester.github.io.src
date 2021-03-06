Playing with the JTAGulator 
############################
:date: 2013-10-16 12:50
:author: antitree
:category: Hardware, Security
:slug: jtagulator
:status: published

The JTAGulator is a tool designed by Joe Grand - the guy that used to
make the DEFCON badges for years and was part of one of the first
hackerspaces, \ `Lopht <http://en.wikipedia.org/wiki/L0pht>`__. He did a
Blackhat LV presentation on his newest open hardware, open source
project called the JTAGulator. It's purpose is to help you figure out
the pins of a JTAG or UART device. This is normally an annoying and time
consuming process.

.. raw:: html

   <div style="text-align: center;">

|http://www.adafruit.com/blog/2013/10/04/new-product-grand-ideas-studio-jtagulator/|
    http://www.adafruit.com/blog/2013/10/04/new-product-grand-ideas-studio-jtagulator/

.. raw:: html

   </div>

 

JTAG
====

JTAG (Joint Test Action Group) is just a name for a standard way of
providing a debug interface to your hardware devices. What's nice about
it is with one interface, you can provide debugging capabilities to a
variety of chips on your board. So if you have two microcontrollers,
each of them can be separately accessed through one interface. Pretty
cool.

Hackers have been using JTAG for years to reverse hardware. You might
have seen them used when messing with router firmware to install DD-WRT
or OpenWRT. For WRT supported routers, JTAG often gives you the ability
to push a custom firmware onto a board or extra the firmware that is
currently installed.

JTAG For Security
=================

Of course with all of my projects, I add a security twist. JTAG lets me
gain low level access to a device and see how it works. An interface may
be able to dump an EEPROM which could contain the cryptographic keys
that are securing another piece of memory on the chip. Or it could give
me a serial console similar to a root terminal that lets me interact
with a device like a computer. The point is, it's a debuggable interface
that I can use to exploit in a variety of ways to learn about how the
device works.

You might wonder why these interfaces even exist on hardware since they
give hackers the opportunity to access your hardware. Because JTAG is so
useful for debugging, manufacturers actually use this interface the same
way you would, to make sure the device is functioning properly. That's
why it's highly likely you'll find some kind of debug interface for your
boards.

JTAGulator Setup
================

The JTAGulator connects to your computer using a micro-USB cable that
shows up as a serial device. In Linux, that device will be something
like /dev/ttyUSB0. It uses 115.2K baud 8N1. Once connected using
something like minicom or gtkterm in Linux, you'll see a prompt of
available options. You can now start JTAGulating.

To connect the JTAGulator to a device, the board is designed to use the
cables from a standard Bus Pirate board. You can either do that, or just
use some aligator clips to connect to the pins. Either way, the board
you're working on is going to need to be have the JTAG leads broken out
so you can connect something to them. In my little Asus router that I
found, these pins are pretty easy to access. I just soldered some cables
on to them, and added a bit of glue to make sure they kept. :)

[caption id="attachment_1527" align="aligncenter" width="225"]\ |Asus
Router with wires near JTAG leads| Asus Router with wires near JTAG
leads[/caption]

From this point, your router should be connected to the JTAGulator, your
JTAGulator connected to your computer, and you should have a console
interface waiting for directions.

The first step is to set the voltage. It has a range of 1.2 to 3.3V and
this is going to be important for you to figure out before hand. (If you
don't know how to figure out the voltage on your board, you can probably
ask someone at Interlock to show you using a multimeter.) Then you can
choose how you'd like to scan for JTAG. There are two options, one is
more thorough and time consuming but I don't have enough data to tell
you which is better for which situation (feel free to chime in if you
know). Either one will prompt you for which pins you'd like to test
with, which should correspond to the pins you've connected on your
JTAGulator. When you run it, it will attempt every possible combination
of pins until it thinks it has found the right one. It also has a UART
discovery mode.

This is not the first JTAG discovery product out there but it's the
first I've used. I mentioned that the project is open source so here is
a link to Joe's site to help you build your own board if you want, or if
you're like me, you can buy them from a company like
`Adafruit <http://www.adafruit.com/blog/2013/10/04/new-product-grand-ideas-studio-jtagulator/>`__,
too.

http://www.grandideastudio.com/portfolio/jtagulator/

.. |http://www.adafruit.com/blog/2013/10/04/new-product-grand-ideas-studio-jtagulator/| image:: /wp-uploads/2013/10/1550_LRG-600x4611.jpg
   :class: aligncenter
   :width: 600px
   :height: 461px
   :target: /wp-uploads/2013/10/1550_LRG-600x4611.jpg
.. |Asus Router with wires near JTAG leads| image:: /wp-uploads/2013/10/IMG_20131015_1929571-225x300.jpg
   :class: size-medium wp-image-1527
   :width: 225px
   :height: 300px
   :target: /wp-uploads/2013/10/IMG_20131015_1929571.jpg
