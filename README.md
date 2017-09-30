# macOS on Dell XPS 13 9360
This are the files and patches required for installing macOS on the XPS13 9360.
All credit goes to @bozma88 thread and community over at [https://www.tonymacx86.com/threads/guide-dell-xps-13-9360-on-macos-sierra-10-12-x-lts-long-term-support-guide.213141/] (tonymacx86.com),
please read it __carefully__ !

### @neavend configuration:
- i7-7500U
- 8GB LPDDR3 1866MHz RAM
- 256GB Toshiba NVME SSD
- 1920x1080 screen
- Bios 1.3.5
- USA-International keyboard layout

Target BIOS -> 1.3.5 \
Target OS -> 10.12.6

### Updated files:
- Added HFSPlus.efi
- VoodooPS2Controller.kext to @syscl default controller for trackpad gestures

### To mount an UEFI partition on macOS:
Instead of using an app like EFIMount.app, simply run `diskutil mount EFI` from your terminal.
This will default to external drives, and take the internal one if none is connected.

# REQUIRED STEPS:
### Pre-install:
- Swap the motherboard WIFI card for a DW1560
- Flash Bios 1.3.5 and check settings accordingly
- 4k format the Toshiba drive
- DVMT Patching to 64M

### Install:
- Install clover on your install macOS key
- Copy and the CLOVER folder provided here with the one on your key
- Reboot and install macOS normally

### Post-install:
- Disable hibernation
- Copy POST-INSTALL/S-L-E to System/Library/Extensions and set the permissions to root:wheel 755
- Install CLOVER and copy the CLOVER folder accordingly
- Set up iMessage if you need it [https://www.tonymacx86.com/threads/an-idiots-guide-to-imessage.196827] (GUIDE)
- Remove Eject button from menu bar: `rm -rf "/System/Library/CoreServices/Menu Extras/Eject.menu"`
- Clear caches: `sudo touch /System/Library/Extensions && sudo kextcache -u /`
- Reboot and voila !

## A note on FileVault:
I have added the necessary files to enable Filevault directly, but be advised of a few things:

- You need a working "Recovery HD" partition, which will be your only way to boot.
- You will need to enter your recovery key each time you boot your computer, as your password will not get accepted.

If you can go through with this limitation, or almost never reboot like me and use a password manager, then you should enable FileVault !

## A note on the Power Button:
If you run with the QHD screen instead of the FHD, you can try enabling the power button by tweaking __SSDT-XOSI__ to replace the strings with "*Linux*" with the command `iasl`. If you experience freeze when plugging the power cord, just revert back the changes.
