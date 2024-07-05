---
title: "Xperia 1 V Derpfest"
date: 2024-07-04

summary: "Flash Derpfest to Xperia 1 V "
description: "Flash Derpfest to Xperia 1 V"

tags: ["Android", "Xperia"]
---

## Flash Derpfest to Xperia 1 V

- [XDA](https://xdaforums.com/t/rom-14-0-unofficial-derpfest-14-for-xperia-1v-updated-06-28-2024-play-integrity-fixed.4657958/)

1. Unlock Bootloader.
2. Poweroff, hold Volume+, plug USB cap to PC, see blue light on (bootloader mode).
3. Make sure Bootloader [Driver](https://developer.android.com/studio/run/win-usb) installed, use commands below.

   ```
   fastboot flash boot boot.img
   fastboot flash recovery recovery.img
   fastboot flash vendor_boot vendor_boot.img
   fastboot flash dtbo dtbo.img
   ```

4. Reboot to recovery with `fastboot reboot recovery`.
5. Clear Data / Factory Reset.
6. Enter Sideload mode.
7. Flash ROM file with `adb sideload <file>`.

## Notice

1. GApps included
2. KernelSU included
