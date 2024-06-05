---
title: "Xperia 1 V 更新"
date: 2024-05-30T22:35:02+08:00

summary: "Xperia 1 V 手动更新系统步骤"
description: "Xperia 1 V 手动更新系统步骤"

tags: ["Android", "Xperia"]
---

## 更新系统:

1. 使用 [XperiFirm](https://xdaforums.com/t/tool-xperifirm-xperia-firmware-downloader-v5-7-0.2834142/) 下载最新固件
2. 复制 [NewFlasher](https://xdaforums.com/t/tool-newflasher-xperia-command-line-flasher.3619426/) 文件 `newflasher.exe` 与 `newflasher.x64` 至固件目录
3. 手机关机，按住音量 - ，插入 USB 线，指示灯绿色后松手
4. 运行 NewFlasher
5. **注意选项，询问是否 keep data 时输入 `y` 保存数据！！！**

## ROOT - KSU:

0. 下载 [UnSIN](https://xdaforums.com/t/tool-unsin-sin-v3-v4-v5-unpacker-v2-0.3128106/)
1. 在固件目录中找到 `init_boot_X-FLASH-ALL-25B1.sin`
2. 将 sin 文件拖动到 `unsin.exe` 得到 `init_boot_X-FLASH-ALL-25B1.img`
3. 使用 kernelSU app 修补 `init_boot_X-FLASH-ALL-25B1.img` 得到 `kernelsu***.img`
4. 重启到 fastboot 模式, 执行 `fastboot flash init_boot kernelsu***.img`
5. 重启

## 隐藏状态栏 VOLTE、VONR 图标

**每次更新系统后需要重新操作**

1. 找到`/data/user_de/0/com.android.phone/files/carrierconfig-***`（双卡两个）
2. 约 50+ 行，`<boolean name="s_show_volte_icon_in_status_bar_bool" value="true" />`
3. `value="true"` 改为 `value="false"`
4. 重启

## Lawnchair -KSU:

[Guide](https://ewigl.github.io/notes/posts/202405/lawnchair-quickswitch/)
