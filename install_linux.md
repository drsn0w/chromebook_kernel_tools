
# Installing Arch Linux on Chromebooks That Don't Support SeaBios

**THIS GUIDE IS NOT YET COMPLETE. IN ITS CURRENT STATE IT SHOULD GET YOU TO A BOOTING ARCH LINUX INSTALLATION WITH A FEW ISSUES. SOLUTIONS TO THESE ISSUES WILL BE ADDED SOON**

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
7. `cp /usr/share/vboot/devkeys/kernel_data_key.vprivk ./`
7. `bash extract_kernel`
8. `echo "root=/dev/sda1 ro rootwait" > config.txt`
9. `bash repack_kernel`
10. **MAKE SURE THERE ARE NO ERRORS. FLASHING A BAD KERNEL WILL REQUIRE YOU TO RECOVER YOUR CHROMEBOOK AND START FROM THE BEGINNING OF THIS SECTION**
11. `bash flash_kernel`
12. Please note that at this point, your Chromebook will not boot into Chrome OS without being Recovered.
13. Plug in the Arch Linux installer USB you created earlier
14. Mount the USB drive
13. `cp -R /usr/lib/modules/3.10.18/* /usb/mount/point/usr/lib/3.10.18/`
14. `cp /usr/share/vboot/devkeys/kernel_data_key.vprivk /usb/mount/point`
13. Shutdown your Chromebook.

## Boot the installation medium on your Chromebook

1. Press the Power button on your Chromebook.
2. Press Control+D to bypass the Developer Mode warning screen.
3. If all goes well, the Arch installation shell should boot. 
4. If it hangs on "Creating Volatile Files and Directories", wait. After two minutes, booting will continue. This is normal and we will fix the issue later in this guide. 

*You should be at a root shell with the prompt `root@archiso# `. This is the Arch Linux installation prompt.*

## Installing Arch Linux

1. `mkfs.ext4 /dev/mmcblk0p1`
2. `mount /dev/mmcblk0p1 /mnt`
3. Use `wifi-menu` to establish an internet connection. Note that it may take up to three minutes for Arch Linux to recognise the WiFi card, so be patient if wifi-menu doesn't work.
4. Follow the [Arch Linux Beginner's Guide starting at Select a mirror](https://wiki.archlinux.org/index.php/Beginners%27_guide#Select_a_mirror), up until "Install and configure a bootloader". **Do not Install and configure a bootloader.**
5. `exit` from the arch-chroot.
6. `pacman -S git`
7. `git clone https://github.com/drsn0w/chromebook_kernel_tools.git`
8. `cd chromebook_kernel_tools`
9. `cp /kernel_data_key.vprivk ./`
9. `./extract_kernel`
10. `echo "root=/dev/mmcblk0p1 ro rootwait" > config.txt`
11. `./repack_kernel`
12. `./flash_kernel`
13. `cp -R /usr/lib/modules/3.10.18/* /mnt/usr/lib/modules/3.10.18/`
13. `umount /mnt`
14. `shutdown -h now`
15. Once the Chromebook powers off, remove the flashdrive.


