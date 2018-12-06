# DPT Stuff
Files for Sony's DPT-RP1

## Restoring System

Download system.img from the 1.4.01.16100 Stock folder. Check that its MD5 is `5081ec24954714373229a7c76154509a`.

Boot your device into diagnostic mode. Open a terminal connection and run `/usr/local/bin/mass_storage`. It will mount its storage partition (mmcblk0p16) as a USB mass storage device on your PC.

Copy system.img to it, then safely remove it.

Go back to the terminal, hit Ctrl+C to end mass_storage and it will unmount from your PC if you haven't safely ejected it.

```
mount /dev/mmcblk0p16 /mnt/sd
cd /mnt/sd
md5sum system.img
```

Check that against the above MD5sum. If it doesn't match, start over and DO NOT FLASH IT.

Run `extract_sparse_file /mnt/sd/system.img /dev/mmcblk0p9`. It won't output anything until it's done flashing, so don't touch the DPT, don't touch the PC, don't move the USB cable, don't cancel it just let it finish.

Once it's done you can type

```
umount /dev/mmcblk0p16
reboot
```

and it should reboot into a stock system.

## Restoring Boot

**You probably do NOT need to do this. Only do this if your device never makes it to the welcome screen.**

I haven't corrupted my boot partition so haven't had to flash it yet. But if flashing system doesn't work and you're still able to boot into diag mode, you can try flashing the boot partition. 

Follow the same instructions to download boot.img, copy to the device, and check its MD5. Note that boot.img's MD5 should be `6a83136b15ad2a55f3e0240a0fe9c1a7`.

If it matches, run `dd if=/mnt/sd/boot.img of=/dev/mmcblk0p8 bs=4M`, then unmount and reboot.