---
title: General Troubleshooting & Recommendations
description: 
published: true
date: 2024-07-01T19:39:42.284Z
tags: 
editor: undefined
dateCreated: 2024-05-04T04:46:59.067Z
---

# General Care Instructions

## Taking care of Cables

**Under no circumstances should you unplug or plug in either end of the cable connecting the main board and toolhead board while the printer is powered on. Doing so may damage/short out the tool board and/or the mainboard.**

Before storing away in the carrying case, please disconnect your Bowden Tubes and Cables to avoid damage. Power off the machine first.

While the unit can be stored with the Bowden tube connected, there is a chance of the tube becoming ‘warped’ in a folded state, unplugging it from the extruder (not the hot end) can help prevent this.

## Cool Down Before Packing

The Positron can run warm as it uses the Base Plate as a heat sink, we recommend waiting a few minutes after the last print before storing it in the provided case to allow for the baseplate to cool down.

## Taking care of your Glass Bed

We recommend cleaning your bend every 3 to 4 prints. This is a non-textured borosilicate glass plate, so adhesives designed for glass surfaces will work well if you're struggling to get adhesion.

Additionally, while the ITO coating on the back side of the glass is fairly scratch resistant, it's still a thin coating. Wherever possible, avoid any metallic objects coming in contact with this coating, as it's thinness could make the coating easily scratched. Scratching this coating could cause significant problems with heating your bed.

## Printing PETG

PLEASE USE AN ADHESIVE!

To avoid damaging your glass bed, please use a weak adhesive like glue stick to act as a barrier between the Glass and PETG.

PETG Loves to stick to glass, and has been known to rip chunks out of the glass in older printers that use Glass beds.

# Known Issues

We are aware of a few pre-existing issues;

## IR Leveling

The Positron's primary method of leveling is IR Leveling, however this can change accuracy depending on the lighting in the room.

Header Pins will be included on the Main Board to allow for custom probes to be added to the Positron, including custom Z Probes 

Please see the Bed Leveling Guide under General Troubleshooting for our recommendation of bed leveling with the IR Sensor.

## Cooling Performance

Make sure your hotend fan is set to 0.9 or 1.0 in Klipper Config. This will prevent heat creep.

Additionally, we are working on improving the part-cooling performance. We welcome support from the community to see how this can be improved.

# General Troubleshooting
Before delving too deep, make sure your [Configs are up to date.](https://github.com/MotorDynamicsLab/PositronHardware/tree/master/PositronV3.2/Configs)

## MCU Not Connecting

The Positron V3.2 uses two custom boards by LDO communicating over USB, if for some reason your Klipper instance is no longer able to connect to the MCU and PTH boards, please follow this guide.

> **IMPORTANT: Never hot-plug the Toolboard Cable, it may cause a short on the tool-head board which will damage it.**

1.  Turn off your printer and unplug the Toolboard Cable from the Main Board.
2.  Power on the printer
3.  Connect to your Klipper Web interface and open your printer config.
4.  In another window, SSH into your Pi, use whatever username/password you set.
5.  In your SSH Terminal, enter; `ls -l /dev/serial/by-id/`
6.  Copy the `/dev/serial/by-id/usb-Klipper_rp####_#################-####`, this will be unique to the serial of your MCU
    -   If you see two usb-Klipper serials, then you did not unplug your Toolboard Cable. Go back to step 1, and try again.
7.  Paste the usb-Klipper serial and update your `MCU` in Klipper
8.  Power off the Printer and plug-in the Toolboard Cable
9.  Re-connect to the printer via SSH
10.  In your SSH Terminal, enter; `ls -l /dev/serial/by-id/`
    -   Now there will be two usb-Klipper serials, copy the one that isn't your MCU serial.
11.  Update the `MCU PTH` with the second serial in your Klipper config.

## Bed Leveling

Due to the aforementioned issues with the IR Probe, we recommend manually leveling the bed. Bed meshes will not be accurate and will cause issues.

Best method is to use a Cube Primative in slicer, and set it to only slice one layer.

Disable \[BED\_TILT\] in your printer.cfg if it isn't disabled already.

Print the cube and adjust the bed knobs to get the front of the bed level with each other, then adjust your Z-Offset for front/back.

# Updating Firmware
[Follow this guide for updating Firmware, it's the same process as the Nitehawk](https://docs.ldomotors.com/en/Toolboard/nitehawk-sb)
We will have a specific guide for the Positron available once complete from LDO