![Lenovo m93p mini](https://github.com/asle/lenovo_m93p_mini_hackintosh/blob/master/m93p.jpg?raw=true)

# Lenovo m93 mini Hackintosh - OpenCore
- Update - changed SMBIOS to Macmini7,1 for macOS Monterey 12.7.3  support, upgraded to OpenCore 0.9.8.
The Lenovo m93p is a tiny PC and first gen. of the Lenovo mini series using a Haswell Intel cpu 4th gen. e.g. I5-4260U. Perfect for hackintoshing!
NOTE! The SMBIOS is set to Mac Mini (Late 2014). Both models(SMBIOS) are running Intel Haswell 4th gen. cpu so it works fine. Feel free to try. But I am very satisfied with the speed on macOS Monterey. NOTE! -> You must generate a new SystemSerialNumber, MLB, ROM and SystemUUID!

## About this guide
This is not a complete tutorial but based on the [**OpenCore Vanilla Desktop Guide for Haswell**](https://dortania.github.io/OpenCore-Install-Guide/config.plist/haswell.html). I reccomend reading the guide carefully to understand OpenCore. Or else you will not learn anything! My goal with this guide is to help you avoid all the errors you would encounter. The OC guide is great but every PC is different and this one was a bit quirky and needed some tweaking to work! I assume you already have made an OS X install-USB.
-> See changes.txt for updates

## Specs
* Intel i5-4590T @ 2.20GHz (35w) 4-core/4-thread
* 8GB (2x4) DDR3 1600MHz
* 6 x USB 3, 2 front, 4 back
* 2.5" SSD Samsung 860 EVO 500GB
* BCM94352HMB(Mini PCI) wifi/bt card
* 65w external power supply
* OpenCore 0.7.2

## What is working
* Mac Mini (Late 2014)
* macOS 12.7.3
* Sleep
* Wifi/Bluetooth with new Broadcom card
* Audio, in/mic and out
* Multi-monitor (2)
* iMessage, AppStore
* AirDrop, Handoff etc.

## What is not working
* HDMI audio (@Tokobotenkai [**mentioned**](https://github.com/asle/lenovo_m93p_mini_hackintosh/issues/18) mentioned using an active DP-HDMI adapter will fix this. I have not tried it yet.)

## About mini-PCs and this machine
I am fascinated by these small, cute Mac Mini-like PCs and have had my hands on many different models from Lenovo, HP and Dell. You can get the first gen. models very cheap online (much cheaper than a slower Mac Mini) and they pack a lot of power considering their small size and price. They are all easy to upgrade with RAM, hard drives and CPU. That is not possible with a Mac Mini! What differs these machines are mainly:
* Different Intel gen. 4th, 6th, 7th, 8th etc.
* RAM speed and max capacity
* USB3 / USB-C and USB3 speeds
* Single or dual drive capacity
* Heat and noise differences
___
The Lenovo m93p is the first gen. in this series. It features a Haswell low-power cpu, up to 16gb RAM and connector for 2.5" SATA 6.

## Pros Lenovo m93p tiny
* The easiest mini-PC I have ever hackintoshed
* The "T" cpu runs cool and this PC is maybe the quietest I have run
* Easy to open
* Easy to swap the wifi/bt Mini-PCI card with a OS X compatible card (this Mini-PCI card is also much cheaper than a M.2 card)
* Easy to install 2.5" hard drive
* Easy to upgrade CPU

## Cons Lenovo m93p tiny
* Can only install 1 x 2,5" hard drive, no M.2 slot
* 4th gen. Intel CPU lags a bit behind 6th or newer gen.

## Installation
* I installed Windows10 on the drive and used [SSDTIME](https://github.com/corpnewt/SSDTTime) to generate the SSDTs. I copied these over to the ACPI folder. I can not guarantee these are perfect for your PC but I suggest you do this on your own Lenovo m93p Tiny to be sure.
* Copy over my EFI folder (created from  [OpenCore guide for Haswell](https://dortania.github.io/OpenCore-Install-Guide/config.plist/haswell.html#starting-point)) to the EFI partition
* Edit config.plist to enter new serials, MB, UUID etc.

## BIOS setup
I suggest upgrading to latest version. Load default settings. Things to configure:
* Security -> Secure Boot -> Disable
* Advanced -> CPU Setup -> VTd -> Disabled
* Devices -> Video Setup -> Active Video -> IGD
* Devices -> Video Setup -> Pre-Allocated Memory Size -> 64MB
* Devices -> Video Setup -> Total Graphics Memory -> Maximum

## USB port mapping
I have enclosed the USBports.kext derived from hackintool. It should work on your PC of this model.

## config.plist changes
* This info is outdated. Major changes to EFI from original version.
The only change I can recall is this:
* RebuildAppleMemoryMap -> YES
You will see the [OC sanity checker](https://opencore.slowgeek.com/) complain about the change :-)

## Wifi - Bluetooth
I am using the BCM94352HMB from AzureWave ($24). This requires some extra kexts to work.
* AirportBrcmFixup.kext
* BrcmBluetoothInjector.kext
* BrcmFirmwareData.kext
* BrcmPatchRAM3.kext

![BCM94352HMB.jpg](https://github.com/asle/lenovo_m93p_mini_hackintosh/blob/master/BCM94352HMB.jpg?raw=true)

## Multi-monitor
This works OTB with no other patching then the one from the OC Guide. So I have 2 monitors working with not problems. VGA does not work like on any other Hackintosh!

## Audio
Realtek ALC283. ~~This works fine with correct alcid=1.~~ Changed to AppleALC.kext and alcid=11. Still internal speaker not showing up.


Devicepropertides for audio and gpu:

![Deviceproterties](https://github.com/asle/lenovo_m93p_mini_hackintosh/blob/master/lenovo_m93p_deviceproperties.png?raw=true)

## Misc.

### Cosmetics
As you see I have added the OpenCanopy.efi and the resource folder so the startup is a little nicer to look at with icons. Remove the "-v" in boot-args if you want a clean, no-text startup. I just like to see what is going on :-)

### Performance ###
This m93p is an i5 4590T, 4-core/4-thread. It is faster than a 2014 Mac Mini! I just love the Haswell versions since they are so easy to hack- Skylake has been a pain regarding sleep and GPU issues. This m93p runs 17 tracks in Logic Pro X (the test file) with all plugins. Not bad for a machine you can get for $100-$200 used. You can increase the performance if you swap in a i7 4785T.

This must be one of the cheapest Hackintoshes you can do. Forget gaming please! At least anything that requires a dedicated GPU. This is a great desktop for daily tasks. What I love about the m93p is that is small and cute and very well built. One of the most stable Hackintoshes I have built.
