---
title: Pi Imaging
description: 
published: true
date: 2024-10-18T16:37:48.946Z
tags: 
editor: markdown
dateCreated: 2024-08-01T04:11:47.615Z
---

# IMPORTANT
All Positrons (as well as the image itself) use a default Pi password.
[**CHANGE THIS AS SOON AS POSSIBLE.**](https://www.raspberrypi-spy.co.uk/2012/10/how-to-change-raspberry-pi-password/)

# Touchscreen Controller Imaging and Backup 
This is a guide to create a fresh Positron Klipper image for the Rapsberry PI CM4 touchscreen controller.

When to use:
- Pi operating system is corrupted
- Failed updates
- Factory reset 
- Creating a backup SD Card

*Imported Note: This will completely erase the SD card, if there are custom macros or settings, download them from Fluidd first.*

## When Not To Use
If there are MCU connection issues a full reflash may not be needed.
Download and add the latest printer.cfg file from [Positron GitHub](https://github.com/Positron3D/Positron/blob/main/Software%2C%20Configs%2C%20Calibration/Klipper%20Configs/printer.cfg) and try again, or proceed to [MCU Not Connecting](/Printers/Positron/Troubleshooting#mcu-not-connecting).

### Supplies Needed
- 32 GB SD card and card reader (smaller or larger SD cards, haven't been tested)
- [BalenaEtcher Website](https://etcher.balena.io/) for flash from URL or another imaging program

## Download and Flash

### Etcher Method
1. Insert the SD Card and notate the drive letter.
2. If Etcher flash from URL is not being used download the img.gz from [Here](https://www.googleapis.com/drive/v3/files/1sboY6woogdmHacunRqMUZkNO5GTnQjvf?alt=media&key=AIzaSyA9_7f2w7ftASKMnk38vMI-hAA9T99_rCs), 2GB of space needed. The image is a direct
clone of the LDO provided SD Card with the empty space removed.
3. If using flash from URL, open Etcher, select flash from URL, copy URL from below, and paste in the "Enter Valid URL" box.

```
Primary: https://www.googleapis.com/drive/v3/files/1sboY6woogdmHacunRqMUZkNO5GTnQjvf?alt=media&key=AIzaSyA9_7f2w7ftASKMnk38vMI-hAA9T99_rCs

Backup: https://onedrive.live.com/download?resid=85EA24ADAC21AF56%2119213&authkey=!AC_DbDIB
```
4. After the img.gz file or URL has been entered, select the correct SD Card drive letter and click Flash.
5. Insert SD Card into a powered off Positron, make sure all cables are connected and then turn it on. Please be patient, the LDO splash screen will loop twice and may pause on a black screen until Klipper finishes loading. On first boot the touchscreen controller is setting up the operating system and may take a few minutes.
6. Done. Touchscreen controller has been updated.

## Touchscreen Controller Backup
This section has instructions to backup the current OS on the Touchscreen Controller.

### Supplies Needed
- 8GB or larger USB 3.0 flash drive
- Touchscreen controller running an imaged SD Card from the previous section or has [image-backup](https://github.com/seamusdemora/RonR-RPi-image-utils) utility installed
  
### Prepare to Backup
- With the Positron powered off insert the flash drive into the available USB port, double check all cables are plugged in,
then power on the machine.
- In order to backup the Raspberry PI touchscreen controller, SSH access is needed and the image-backup utility installed.
	1. Find the IP address of touchscreen from the onscreen buttons, menu -> network. If the RpiHotspot is turned off the IP
  address will be listed on the top line. The HotSpot button can be toggled if the IP address has not appeared yet.
  2. From a computer open either a terminal, Windows PowerShell, or use a program like [Putty](https://www.putty.org/)
  3. Next log into the touch using SSH, the default user name is "pi" and password is "raspberry". Below shows an example of a SSH command using Windows PowerShell and username "pi".
  ```
  ssh pi@EnterIpAdressHere
  ```
  4. If using Windows PowerShell, it will prompt for the password but won't display anything when typing, just press enter when done.
  
 ### Perform Backup
 Once logged into the Rapsberry Pi touchscreen controller using SSH, follow these steps to access the USB Drive to perform a backup.
 There are many different ways to perform the individual steps, but these work for this touchscreen.
- Enter these from the SSH terminal or command line, they may prompt for the password again.
	1. Make a location for the flash drive to mount to.
  ``` 
  sudo mkdir /media/USBDRIVE
  ```
  2. Mount the drive to the previous location
  ```
  sudo mount /dev/sda1 /media/USBDRIVE
  ```
  3. If flash drive has a previous 6GB uncompressed .img file this command will check it for errors.
  ```
  sudo image-check /media/USBDRIVE/PositronV32_stock.img
  ```
  4. If flash drive has the file PositronV32_stock.img the following command will update it and not create a duplicate.
  Otherwise it will create a new backup .img with the name PositronV32_stock.img, any name that ends in .img can be used here. 
  It is roughly 15 minutes to make a new .img or a few seconds to update an exising .img.
  ```
  sudo image-backup /media/USBDRIVE/PositronV32_stock.img
  ```
  5. Now the Positron can be power down and flash drive removed.
  6. The uncompressed .img file uses about 6GB of space but will shrink to around 2GB if compressed to a .zip or .gz.
  Etcher can flash a SD Card from a zip or gz file, so it is fine to leave the backup compressed to save space.
  
  

