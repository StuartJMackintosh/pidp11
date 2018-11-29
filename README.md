# PiDP-11 software, alpha version
See obsolescence.wix.com/obsolescence/pidp11

## Bootscripts

**Important: I'm struggling with github's handling of large (largish) binary images.**

So, do everything as per below. Then, download the contents of the bootscripts directory (OS disk images and boot scripts) from this Google Drive file:
https://drive.google.com/open?id=1SuBurN3uk6VqRGAmvjwREUWHuFMQLZPM

Once uncompressed, Files can be copied from Linux to the Pi over the network using this command:

`scp -r bootscripts pi@raspberrypi:/opt/pidp11`

*pi@raspberrypi is the default username and hostname, they may be different in your set-up*

**(Apologies)**

## Note

- expect updates of the pidp-11 software in the coming months
- you do not need to have the PiDP-11 hardware, it'll run fine without. Just no lights and switches.

## Install instructions:

- make sure your Pi is connected to the internet during install, pull the pidp11 repository,
- create a 'pidp11' directory into /opt, and copy the files inside the pidp11 clone directory into /opt/pidp11/,
- run sudo ./install.sh in /opt/pidp11/install/,
- reboot
- copy the contents of the above ZIP file into the bootscripts directory. It's easiest to download the file onto a USB stick from your laptop, then copy from the USB stick into the Pi.

After reboot, you should find yourself booting RSX-11M+. See detailed instructions at the end of this file.

NOTE: If you have your Pi booting into the GUI, you need to open a terminal in the GUI and run ~/pdp.sh to grab the terminal of the already running PDP-11. 
However, if you configure the Pi to boot into the CLI, the PDP-11 comes up straight away. Which is nicer.


## Using the PiDP-11, first steps:

To exit the PDP-11 (simh): CTRL-E, exit. 
To restart the PDP-11, see next section

To leave whilst keeping the PDP-11 running: CTRL-A, then d. 
Then, to return to the running PDP-11: ~/pdp.sh


## Restarting with various boot options:

If the PiDP-11 front panel hardware is attached:
  select a boot script using one of the SR switches (1-21, not 0)
  You can now restart the PDP-11 with /opt/pidp11/bin/pidp11.sh

Without front panel hardware, simply use ./pidp11.sh 2 to run boot script 2, etc.


## Currently installed operating systems:

The idea is that this gradually fills up with fully loaded operating systems, of course. For now:

SR switch/OS | SR switch/OS | SR switch/OS | SR switch/OS |  SR switch/OS |
----------|-----------|-----------|-----------|------------|
1 - RSX-11M + | 6 - Unix v6 | 11 - | 16 - | 21 - Nankervis |
2 - BSD211 | 7 - | 12 - | 17 - |      Collection of
3 - RT11 | 8 - | 13 - | 18 - |      15 OSes
4 - RSTS v7 | 9 - | 14 - | 19 -
5 - | 10 -| 15 - | 20 - Hill's Blinky

Also see http://obsolescence.wixsite.com/obsolescence/pidp-11-how-to-use for the current state of the System Collection.


## Changing boot scripts & adding your own:

Simh boot scripts are saved in pidp11/bootscripts. The first digit(s) in the file name will determine 
which SR switch will activate the script at program start. The rest of the file name can be whatever 
description it needs, but the extension has to be .script.

The disk & tape images your configuration script require are by convention stored in 
the numbered subdirectories (0-21) of the bootscripts directory. Also by convention, backup copies are
in a subdirectory in case you mess up a disk image and want to start afresh.


## Step-by-step install instructions

In case you're not too familiar with Raspbian/Linux:
First make sure you've got a working internet connection (googling will help you quickly). 

Then, once attached to your Pi:

1. `sudo apt install git`
1. `cd /opt`
1. `sudo git clone git://github.com/PiDP/pidp11.git`
1. `sudo chown -R $USER /opt/pidp11`
1. `cd /opt/pidp11`
1. `sudo ./install/install.sh`
1. Install bootscripts in to /opt/pidp11/bootscripts - See bootscript comments at the top of this page
1. `sudo reboot`


## Various notes

- This is just to get the beta testers going, and perhaps to attract help from people to set up more interesting OSes... 
- The sources come from https://github.com/j-hoppe/BlinkenBone , I'll set up a proper branch when I leave the sandbox phase.
- The /opt/pidp11/src directory contains all sources. The two scripts in there allow you to recompile the client and server.
