---
title: "Xperia 1 V Update"
date: 2024-05-30T22:35:02+08:00

summary: "Xperia 1 V Manual Update System Steps"
description: "Xperia 1 V Manual Update System Steps"

tags: ["Xperia"]
categories: ["Android"]
---

## Update System

1. Download the latest firmware from [XperiFirm](https://xdaforums.com/t/tool-xperifirm-xperia-firmware-downloader-v5-7-0.2834142/)
2. Download [NewFlasher](https://xdaforums.com/t/tool-newflasher-xperia-command-line-flasher.3619426/), copy `newflasher.exe` and `newflasher.x64` to the firmware directory
3. Turn off the phone, hold the volume button -, insert USB cable, the indicator light turns green and release
4. Run NewFlasher
5. **Note: input `y` to keep data when asking if you want to keep data.**

## ROOT - Ksu

0. Download [UnSIN](https://xdaforums.com/t/tool-unsin-sin-v3-v4-v5-unpacker-v2-0.3128106/)
1. In the firmware directory, find `init_boot_X-FLASH-ALL-25B1.sin`
2. Drag sin file to `unsin.exe` to get `init_boot_X-FLASH-ALL-25B1.img`
3. Use kernelSU app to patch `init_boot_X-FLASH-ALL-25B1.img` to get `kernelsu***.img`
4. Reboot to fastboot mode, execute `fastboot flash init_boot kernelsu***.img`
5. Reboot

## Hide StatusBar VOLTE、VONR Icons

**Redo after every update**

1. Find `carrierconfig-***` in `data/user_de/0/com.android.phone/files`（Dual SIM, two files）
2. About 50+ lines, `<boolean name="s_show_volte_icon_in_status_bar_bool" value="true" />`
3. `value="true"` change to `value="false"`
4. Reboot

## Lawnchair - Ksu

[Guide](https://ewigl.github.io/notes/posts/202405/lawnchair-quickswitch/)
