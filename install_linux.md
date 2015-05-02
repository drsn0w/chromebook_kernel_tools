
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
*Commands in this section are to be typed on your Linux computer*

1. Partition your USB flash drive with a GPT partition table and one ext4 partition using all available space.
2. Download the latest Arch Linux ISO image from the Arch Linux website.
3. Using an archive utility, extract the following from the Arch Linux ISO: `arch/x86_64/airootfs.sfs`.
4. `unsquashfs airootfs.sfs`
5. `cp -R squashfsroot/* /USB/mount/point`
6. Unmount USB drive

## Prepare Chromebook for booting from Arch Installer
*Commands in this section are to be typed on your Chromebook in Chrome OS*

1. Make sure your Chromebook is in Developer Mode. If you're not sure, it probably isn't. Google how to do this, as it is outside the scope of these instructions. 
2. Download the tarball of this repo (link here)
3. Open Crosh and type `shell`
4. `cd ~/Downloads`
5. `tar -xvsf repo.tarball.tar.gz`
6. `cd repo-directory`
7. `bash extract_kernel`
8. `echo "root=/dev/sda1 ro rootwait" > config.txt`
9. `bash repack_kernel`
10. **MAKE SURE THERE ARE NO ERRORS. FLASHING A BAD KERNEL WILL REQUIRE YOU TO RECOVER YOUR CHROMEBOOK AND START FROM THE BEGINNING OF THIS SECTION**
11. `bash flash_kernel`
12. Please note that at this point, your Chromebook will not boot into Chrome OS without being Recovered.
13. Shutdown your Chromebook.


