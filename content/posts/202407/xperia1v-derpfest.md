---
title: "Xperia 1 V Derpfest"
date: 2024-07-04

summary: "Xperia 1 V Derpfest 刷入"
description: "Xperia 1 V Derpfest 刷入"

tags: ["Android", "Xperia"]
---

## Xperia 1 V 刷入 Derpfest

- [XDA](https://xdaforums.com/t/rom-14-0-unofficial-derpfest-14-for-xperia-1v-updated-06-28-2024-play-integrity-fixed.4657958/)

1. 解锁 Bootloader。
2. 关机，按住音量+键，插入 USB 线连接电脑，亮起蓝灯，进入 Bootloader。
3. 确保已安装 Bootloader [驱动](https://developer.android.com/studio/run/win-usb)，使用如下命令刷入各分区。

   ```
   fastboot flash boot boot.img
   fastboot flash recovery recovery.img
   fastboot flash vendor_boot vendor_boot.img
   fastboot flash dtbo dtbo.img
   ```

4. 使用 `fastboot reboot recovery` 重启到 recovery。
5. 清空 Data / 恢复出厂设置。
6. 进入 Sideload 模式。
7. 使用 `adb sideload <file>` 刷入 ROM 文件。

## 备注

1. 自带 GApps
2. 自带 KernelSU
