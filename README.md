# 2019 Hackintosh Build Notes

⚠️ This is currently a work-in-progress and it is incomplete. ⚠️

## Introduction
This document is not a step-by-step guide. Rather, it augments [Corpnewt’s  Vanilla Desktop Guide](https://hackintosh.gitbook.io/-r-hackintosh-vanilla-desktop-guide/) with hardware specific tweaks.

## Warning
You will run into roadblocks. And everyone will give you their advice, most of it *awful*. Stay away from Unibeast, Multibeast, Tonymacx86.com, etc.

But keep things as vanilla as possible. Make minimal changes from the default installation. *Make sure you understand the changes you are making*.

## Hardware Build
* Here is my exact build on [PCPartPicker](https://pcpartpicker.com/list/MCX2Cb).

* Intel i7-8700K CPU
* Sapphire RX 580 Nitro+ SE GPU
* ASUS Z390-I Gaming motherboard
* Samsung 970 EVO Plus NVMe SSD
* Fractal Design Define Nano S mini-ITX case

## Pre-installation
Out of the box, your 970 EVO Plus SSD is probably going to be incompatible with macOS.  You *must* apply the May 2019 firmware update before you begin the macOS installation procedure. 

You can find more info and the firmware download link here: [970 EVO Plus Firmware ISO](http://ssd.samsungsemi.com/ecomobile/ssd/update15.do?fname=/Samsung_SSD_970_EVO_Plus_2B2QEXM7.iso). If you get an error about the download limit being exceed, try refreshing after a couple minutes. It usually allows you to download after the second or third refresh.

## Installation

* Follow  [Corpnewt’s Vanilla Desktop Guide](https://hackintosh.gitbook.io/-r-hackintosh-vanilla-desktop-guide/). Be sure to follow each step closely and do not forget about the Coffee Lake section.

* After that, follow then[GitHub - corpnewt/USBMap](https://github.com/corpnewt/USBMap) instructions to get your USB ports working right.

## Post-Installation

### I recommend you enable SIP

1. Open `config.plist` in  [Clover Configurator](http://mackie100projects.altervista.org/download-clover-configurator/) 

2. Navigate to *RT Variables > CsrActivateConfig*

3. Change `CsrActivateConfig` to appropriate value
  *Disable* SIP: `0x67`
  *Enable* SIP: `0x00`
4. *Reboot* Hackintosh to apply these changes.

### When Quick Look and Preview fails

There are a couple ways to fix this: 

1.  Enable a few settings in your UEFI with regard to the iGPU and iGPU Multi-Monitor. This was unreliable and troublesome for me, especially when dual booting between macOS and Windows.

2. Add a couple of boot arguments to your config.plist. This option replaces the NoVPAJPEG kernel extension. NoVPAJPEG was recently deprecated and its functionality was [moved into WhateverGreen](https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.OldPlugins.en.md).

Now, you simply add `shikigva=32` and `shiki-id=Mac-7BA5B2D9E42DDD94` to your boot arguments in config.plist.

So, what does this do? Well, it tells this part of the OS that it is an iMac Pro and that it does not have an iGPU, only a discrete GPU and the system should use that. This does not change your SMBIOS stuff (the Mac model your hackintosh identifies as).

## What Doesn't Work Yet

### Wi-Fi/Bluetooth

Planned fix: to buy a Dell DW 1560 wi-fi/bluetooth card and swap it on the motherboard. There are many different Broadcom cards that are compatible with macOS, but you need one that is the same form factor as the Intel card the motherboard comes with, otherwise you cannot fit the integral heatsink back over the ports. I learned this the hard way. If this is important to you, just buy the Dell DW 1560. It will fit right in.
