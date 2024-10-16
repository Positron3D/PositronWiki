---
title: Z-Endstop Upgrade
description: 
published: true
date: 2024-10-16T18:40:48.558Z
tags: 
editor: markdown
dateCreated: 2024-08-01T04:10:59.209Z
---

# Introduction

## Preamble

If your machine is a Batch 1 or Batch 2 printer, this guide will bring your machine up to current release.

## Z\_Endstop Upgrade 


The purpose of this mod is to increase reliability of homing the Z Axis. While the IR Probe can be used for standard probe use, we find that using a physical switch is far more reliable for constant reliable checks such as homing Z.

This is a fairly easy mod requiring minimal soldering skills and minimum code changes.

## Required Equipment / Tools
### Printed Parts
- [Extruder Body with Endstop Attachment](https://github.com/Positron3D/Positron/blob/main/Printed%20Parts%20%26%20CAD%20Models/Current%20Release%20Printed%20Parts/Extruder/Extruder_Motor_Plate%20-%201x%20-%20Accent%20-%20V1.0.stl)

### Hardware
-   [Microswitch with Lever](https://www.amazon.com/ThtRht-Printer-Endstop-Momentary-Switches/dp/B0CB85485W)
-   [2 pin JST-XH Connector](https://www.amazon.com/dp/B096F5LSVL)

### Tools
- Soldering Iron
	- Solder, Flux, etc
- Crimping Tool
	- Only if making your own cable
- Calipers, or equivalent measuring apparatus.
	- Measuring your work helps avoid a nozzle crash during calibration.
- Multimeter
	- Used for Continuity testing

### Supplemental Reading
- [Board Reference](https://github.com/MotorDynamicsLab/PositronHardware/blob/master/PositronV3.2/Images/Mainboard%20Pinout.png)
	- [<img src="https://raw.githubusercontent.com/MotorDynamicsLab/PositronHardware/master/PositronV3.2/Images/Mainboard%20Pinout.png" alt="Mainboard Pinout" style="background-color: white;" width="400"/>](https://raw.githubusercontent.com/MotorDynamicsLab/PositronHardware/master/PositronV3.2/Images/Mainboard%20Pinout.png)
- [Board Schematics](https://github.com/MotorDynamicsLab/PositronHardware/tree/master/PositronV3.2/Hardware/LDO%20Positron%20Mainboard)

# Guide
## Physical Work

1.  Take a standard Endstop with Lever, orient the lever facing down.
    
2.  Solder wires to Ground and “Normally Closed”
    
    -   This should mean that the end stop has continuity when not triggered.
3.  Mount it to the Extruder using M2x10 bolts, it will thread into plastic.
    
    -   <img src="/Printers/Positron/Mods/z_endstop/endstopphoto.png" alt="Endstop Photo" width="400"/>
4.  Wire the endstop to Z\_ENDSTOP pins on the MCU
    
    -   GPIO3 is the pin, Z\_Stop on PCB Silk Screen
    -   Move the Jumper above the Z\_Endstop pin to the left, bridging `ZSTOP` and `SIG`
    -   <img src="/Printers/Positron/Mods/z_endstop/mcupins.png" alt="MCU Pins" width="400"/>
    
## Printer.CFG Changes
If you haven't already, [update your Printer.CFG to the latest release.](https://wiki.positron3d.com/en/Printers/Positron/Software/PrinterConfigs)

The latest configs are already configured to use the Z_Endstop.

![martychang.gif](/Printers/Positron/Mods/z_endstop/martychang.gif)

## Comments, Feedback, and additional Troubleshooting.
If things aren't working as expected, please note what is wrong and provide feedback to @TheNomad, The Positron Team, and LDO. You can also [join our Discord](https://discord.gg/5ZeAGEkU7G) to submit a support ticket, ask the community questions, and provide other feedback.

Additionally, if you sign into our wiki using Discord, you can leave a comment below for our team to be able to review this document and update it accordingly.