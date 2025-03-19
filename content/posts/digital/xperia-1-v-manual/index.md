---
title: "索尼 Xperia 1 V 定制"
date: 2024-09-15

cover:
  image: "images/shared/android.webp"
  alt: "Cover"
summary: Xperia 1 V 系统更新，LineageOS，Root，自定义等。
description: Xperia 1 V 系统更新，LineageOS，Root，自定义等。

tags: ["Android"]
---

## 港版系统

### 更新系统

0. 使用 [Xperia Check](https://xpericheck.com/XQ-DQ72) 检查系统更新。
1. 使用 [XperiFirm](https://xdaforums.com/t/tool-xperifirm-xperia-firmware-downloader-v5-7-0.2834142/) 下载最新固件。
2. 复制 [NewFlasher](https://xdaforums.com/t/tool-newflasher-xperia-command-line-flasher.3619426/) 文件 `newflasher.exe` 与 `newflasher.x64` 至固件目录。
3. 手机关机，按住音量 - ，插入 USB 线，指示灯绿色后松手。
4. 运行 NewFlasher。
5. **询问是否 keep data 时输入 `y` 保存数据！！！**

### 隐藏图标

> 每次更新系统后需要重新操作

1. 找到`/data/user_de/0/com.android.phone/files/carrierconfig-***`（双卡两个）
2. 约 50+ 行，`<boolean name="s_show_volte_icon_in_status_bar_bool" value="true" />`
3. `value="true"` 改为 `value="false"`
4. 重启

### 相关链接

- [Sony Xperia Companion](https://www.sony.com/zh-cn/electronics/support/articles/00252948)
- [QuickSwitch](https://github.com/skittles9823/QuickSwitch/releases)
- [Lawnchair Nightly](https://github.com/LawnchairLauncher/lawnchair/releases)

## [LineageOS 22.1](https://wiki.lineageos.org/devices/pdx234/)

版本: Latest

### 功能

| 功能            | 详情                                        |
| --------------- | ------------------------------------------- |
| 大师模式        | √                                           |
| 完整分辨率 / 4K | 存在 Bug                                    |
| 全高刷新率      | √                                           |
| 大师 Apps       | ApkMirror                                   |
| 杜比音效        | ×                                           |
| 相机键快速启动  | √                                           |
| GApps           | MindTheGApps                                |
| 人脸解锁        | ×                                           |
| 自定义          | 状态栏网速、电池图标、隐藏 💊、隐藏抽屉应用 |

### Bug

| BUG                         | 详情                                       |
| --------------------------- | ------------------------------------------ |
| 美团等一小部分 App 无法使用 | 梆梆加固 / 国内 App 检测的原因，非系统 Bug |
| 指纹图标指示器位置不对      | 仅完整分辨率模式（4K）下有这个问题         |
| 短信对话页面需要返回两次    | 仅完整分辨率模式（4K）下有这个问题         |

### 补充

- 可使用 Magisk 修补 init_boot 获取 Root 权限。
- KernelSU 暂时未知。
- 使用 APatch 修补 boot 后刷入会导致屏幕触控失灵。使用 scrcpy 进入系统桌面发现 root 权限可以正常工作。

  相关 Issue： https://github.com/bmax121/APatch/issues/934

- Play Integrity Fix 可用。

## 注意事项

> 如果系统未正确识别以下模式，需要在设备管理器处手动指定驱动程序。

- 音量上 + 电源 = Bootloader - 蓝色灯
- 音量下 + 电源 = SOMC Flash Mode - 绿色灯
