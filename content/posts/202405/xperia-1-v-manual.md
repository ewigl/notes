---
title: "Xperia 1 V 使用手册"
date: 2024-07-08

summary: Xperia 1 V 系统更新，Root，自定义等
description: Xperia 1 V 系统更新，Root，自定义等

tags: ["Android", "Xperia"]
---

## 更新官方系统

0. 使用 [Xperia Check](https://xpericheck.com/XQ-DQ72) 检查系统更新。
1. 使用 [XperiFirm](https://xdaforums.com/t/tool-xperifirm-xperia-firmware-downloader-v5-7-0.2834142/) 下载最新固件。
2. 复制 [NewFlasher](https://xdaforums.com/t/tool-newflasher-xperia-command-line-flasher.3619426/) 文件 `newflasher.exe` 与 `newflasher.x64` 至固件目录。
3. 手机关机，按住音量 - ，插入 USB 线，指示灯绿色后松手。
4. 运行 NewFlasher。
5. **询问是否 keep data 时输入 `y` 保存数据！！！**

## ROOT 官方系统 - KSU

0. 下载 [UnSIN](https://xdaforums.com/t/tool-unsin-sin-v3-v4-v5-unpacker-v2-0.3128106/)
1. 在固件目录中找到 `init_boot_X-FLASH-ALL-25B1.sin`
2. 将 sin 文件拖动到 `unsin.exe` 得到 `init_boot_X-FLASH-ALL-25B1.img`
3. 使用 kernelSU app 修补 `init_boot_X-FLASH-ALL-25B1.img` 得到 `kernelsu***.img`
4. 重启到 fastboot 模式, 执行 `fastboot flash init_boot kernelsu***.img`
5. 重启

## 隐藏官方系统状态栏 VOLTE、VONR 图标

**每次更新系统后需要重新操作**

1. 找到`/data/user_de/0/com.android.phone/files/carrierconfig-***`（双卡两个）
2. 约 50+ 行，`<boolean name="s_show_volte_icon_in_status_bar_bool" value="true" />`
3. `value="true"` 改为 `value="false"`
4. 重启

## Lawnchair - KSU

- [QuickSwitch](https://github.com/skittles9823/QuickSwitch/releases)
- [Lawnchair Nightly](https://github.com/LawnchairLauncher/lawnchair/releases)

## 说明

- 音量上 + 电源 = Bootloader - 蓝色灯
- 音量下 + 电源 = SOMC Flash Mode - 绿色灯
