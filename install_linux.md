
# Installing Arch Linux on ASUS C300

This guide details the process I used to install Arch Linux on my ASUS C300. Please note that some issues may arise becuase (at the moment) we can only use the kernel provided by Chrome OS, which is version 3.10. 
Currently this guide is only for Linux.

### Known Issues
- Sound does not work
- Occasional freezing
- Suspend does not work

## Requirements
- ASUS C300 Chromebook (others may work, untested)
- Another computer running Linux
- squashfs-utils
- Chrome OS Recovery Media (make this before you start!!!)
- Flash drive larger than 2GB
- Lots of patience.


## Prepare Arch Linux USB Drive

1. Partition your USB flash drive with a GPT partition table and one ext4 partition using all available space.
2. Download the latest Arch Linux ISO image from the Arch Linux website.
3. Using an archive utility, extract the following from the Arch Linux ISO: `arch/x86_64/airootfs.sfs`.
4. `unsquashfs airootfs.sfs`
5. `cp -R squashfsroot/* /USB/mount/point`
