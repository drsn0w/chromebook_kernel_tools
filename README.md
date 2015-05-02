# chromebook_kernel_tools
Kernel repacking and flashing tools for Chromebook.
Please note that these tools do not stop you from flashing a bad file to your Chromebook, so be careful and have some sort of CrOS recovery media handy.


## Requirements

- vbutil_kernel in $PATH (`sudo apt-get install vboot-tools` on Debian and Ubuntu, Chrome OS developer ships with it)
- kernel_data_key.vprivk from your Chromebook (`/usr/share/vboot/devkeys/kernel_data_key.vprivk`, place in directory with scripts)

## extract_kernel

Uses dd and vbutil_kernel to extract KERN-A from Chromebook and tail the config into config.txt.

**Note that this will overwrite existing `kernel2` and `config.txt`.**

## repack_kernel

Uses vbutil_kernel to repack `kernel2` and `config.txt` into `repacked2`. 

**Watch for errors! Flashing a bad kernel could lead to soft-bricking your device!**

## flash_kernel

Uses vbutil_kernel to verify `repacked2`, and then flashes to /dev/mmcblk0p2 (KERN-A).

**Watch for errors! Flashing a bad kernel could lead to soft-bricking your device!**
