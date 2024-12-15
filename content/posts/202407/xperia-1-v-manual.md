---
title: "Xperia 1 V 相关"
date: 2024-09-15

cover:
  image: "images/shared/android.webp"
  alt: "Cover"
summary: Xperia 1 V 系统更新，Root，自定义等
description: Xperia 1 V 系统更新，Root，自定义等

tags: ["Android"]
---

## 港版系统

### 更新

0. 使用 [Xperia Check](https://xpericheck.com/XQ-DQ72) 检查系统更新。
1. 使用 [XperiFirm](https://xdaforums.com/t/tool-xperifirm-xperia-firmware-downloader-v5-7-0.2834142/) 下载最新固件。
2. 复制 [NewFlasher](https://xdaforums.com/t/tool-newflasher-xperia-command-line-flasher.3619426/) 文件 `newflasher.exe` 与 `newflasher.x64` 至固件目录。
3. 手机关机，按住音量 - ，插入 USB 线，指示灯绿色后松手。
4. 运行 NewFlasher。
5. **询问是否 keep data 时输入 `y` 保存数据！！！**

### 隐藏 VOLTE、VONR 图标

**每次更新系统后需要重新操作**

1. 找到`/data/user_de/0/com.android.phone/files/carrierconfig-***`（双卡两个）
2. 约 50+ 行，`<boolean name="s_show_volte_icon_in_status_bar_bool" value="true" />`
3. `value="true"` 改为 `value="false"`
4. 重启

### Lawnchair - KSU

- [QuickSwitch](https://github.com/skittles9823/QuickSwitch/releases)
- [Lawnchair Nightly](https://github.com/LawnchairLauncher/lawnchair/releases)

## [LineageOS](https://wiki.lineageos.org/devices/pdx234/)

版本：0915

### 功能

| 功能            | 详情                                                  |
| --------------- | ----------------------------------------------------- |
| 大师模式        | √                                                     |
| 完整分辨率 / 4K | √ 存在 Bug                                            |
| 全高刷新率      | √                                                     |
| 大师 Apps       | ApkMirror                                             |
| 杜比音效        | ×                                                     |
| 相机键快速启动  | √                                                     |
| GApps           | MindTheGApps                                          |
| 人脸解锁        | ×                                                     |
| 自定义          | 状态栏网速、电池图标、隐藏手势 💊、隐藏启动器抽屉应用 |

### Bug

| BUG                                 | 详情                               |
| ----------------------------------- | ---------------------------------- |
| 美团无法使用，部分银行 App 无法使用 | 梆梆加固                           |
| 指纹图标指示器位置不对              | 仅完整分辨率模式（4K）下有这个问题 |
| 短信对话页面需要返回两次            | 仅完整分辨率模式（4K）下有这个问题 |
| 短信通知无快速“已读”操作            | 特性...                            |

### 补充

- 可使用 APatch 获取 Root 权限。
- Play Integrity Fix 可用。

## 注意事项

- 音量上 + 电源 = Bootloader - 蓝色灯
- 音量下 + 电源 = SOMC Flash Mode - 绿色灯
