---
title: Xperia 1 V Manual
date: 2024-07-08

cover:
  image: "images/shared/android.webp"
  alt: "Cover"
summary: Xperia 1 V system updating, root, customize etc.
description: Xperia 1 V system updating, root, customize etc.

tags: ["Android"]
---

## Official System (HK)

### Update

0. Use [Xperia Check](https://xpericheck.com/XQ-DQ72) to check system updates.
1. Download the latest firmware from [XperiFirm](https://xdaforums.com/t/tool-xperifirm-xperia-firmware-downloader-v5-7-0.2834142/)
2. Download [NewFlasher](https://xdaforums.com/t/tool-newflasher-xperia-command-line-flasher.3619426/), copy `newflasher.exe` and `newflasher.x64` to the firmware directory
3. Turn off the phone, hold the volume button -, insert USB cable, the indicator light turns green and release
4. Run NewFlasher
5. **Input `y` to keep data when asking if you want to keep data.**

### ROOT -KSU

0. Download [UnSIN](https://xdaforums.com/t/tool-unsin-sin-v3-v4-v5-unpacker-v2-0.3128106/)
1. In the firmware directory, find `init_boot_X-FLASH-ALL-25B1.sin`
2. Drag sin file to `unsin.exe` to get `init_boot_X-FLASH-ALL-25B1.img`
3. Use kernelSU app to patch `init_boot_X-FLASH-ALL-25B1.img` to get `kernelsu***.img`
4. Reboot to fastboot mode, execute `fastboot flash init_boot kernelsu***.img`
5. Reboot

### Hide StatusBar VOLTE、VONR Icons

**Redo after every update**

1. Find `carrierconfig-***` in `data/user_de/0/com.android.phone/files`（Dual SIM, two files）
2. About 50+ lines, `<boolean name="s_show_volte_icon_in_status_bar_bool" value="true" />`
3. `value="true"` change to `value="false"`
4. Reboot

### Lawnchair - KSU

- [QuickSwitch](https://github.com/skittles9823/QuickSwitch/releases)
- [Lawnchair Nightly](https://github.com/LawnchairLauncher/lawnchair/releases)

## 3rd Party System

### LineageOS [Official](https://wiki.lineageos.org/devices/pdx234/)

Version: Latest

Features:

| Feature                   | Detail       |
| ------------------------- | ------------ |
| Creator Mode              | ✓            |
| 4K Fullscreen             | ✓            |
| 120HZ Refresh Rate Global | ✓            |
| Pro Apps                  | ApkMirror    |
| Dolby Audio               | ×            |
| Camera Button Fast Start  | ✓            |
| GApps                     | MindTheGApps |
| Face Unlock               | ×            |
| Customization             | Normal       |

Bug:

| Bug                                                        | Detail                         |
| ---------------------------------------------------------- | ------------------------------ |
| Some Bank Apps Not work                                    | Chinese Apps Reinforcement     |
| Fingerprint Indicator on wrong location                    | Full Resulotion (4K) Mode only |
| Need to back twice in Message app to back to previous view | Full Resulotion (4K) Mode only |
| cant recive messages sometime                              | reboot to fix                  |

PS:

- can be rooted by Magisk init_boot.
- Play Integrity Fixed by modules.

## Notes

- VolumeUP + Power = Bootloader - Blue Light
- VolumeDown + Power = SOMC Flash Mode - Green Light
