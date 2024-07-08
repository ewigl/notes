---
title: "Xperia 1 V"
date: 2024-07-08

summary: Xperia 1 V 系统更新，Root，自定义等
description: Xperia 1 V 系统更新，Root，自定义等

tags: ["Android", "Xperia"]
---

## 港版系统

### 更新

0. 使用 [Xperia Check](https://xpericheck.com/XQ-DQ72) 检查系统更新。
1. 使用 [XperiFirm](https://xdaforums.com/t/tool-xperifirm-xperia-firmware-downloader-v5-7-0.2834142/) 下载最新固件。
2. 复制 [NewFlasher](https://xdaforums.com/t/tool-newflasher-xperia-command-line-flasher.3619426/) 文件 `newflasher.exe` 与 `newflasher.x64` 至固件目录。
3. 手机关机，按住音量 - ，插入 USB 线，指示灯绿色后松手。
4. 运行 NewFlasher。
5. **询问是否 keep data 时输入 `y` 保存数据！！！**

### ROOT - KSU

0. 下载 [UnSIN](https://xdaforums.com/t/tool-unsin-sin-v3-v4-v5-unpacker-v2-0.3128106/)
1. 在固件目录中找到 `init_boot_X-FLASH-ALL-25B1.sin`
2. 将 sin 文件拖动到 `unsin.exe` 得到 `init_boot_X-FLASH-ALL-25B1.img`
3. 使用 kernelSU app 修补 `init_boot_X-FLASH-ALL-25B1.img` 得到 `kernelsu***.img`
4. 重启到 fastboot 模式, 执行 `fastboot flash init_boot kernelsu***.img`
5. 重启

### 隐藏 VOLTE、VONR 图标

**每次更新系统后需要重新操作**

1. 找到`/data/user_de/0/com.android.phone/files/carrierconfig-***`（双卡两个）
2. 约 50+ 行，`<boolean name="s_show_volte_icon_in_status_bar_bool" value="true" />`
3. `value="true"` 改为 `value="false"`
4. 重启

### Lawnchair - KSU

- [QuickSwitch](https://github.com/skittles9823/QuickSwitch/releases)
- [Lawnchair Nightly](https://github.com/LawnchairLauncher/lawnchair/releases)

## 第三方系统

### DerpFest [Unofficial](https://xdaforums.com/t/rom-14-0-unofficial-derpfest-14-for-xperia-1v-updated-06-28-2024-play-integrity-fixed.4657958/)

版本：0625

功能：

| 功能            | 详情      |
| --------------- | --------- |
| 大师模式        | √         |
| 完整分辨率 / 4K | √         |
| 全高刷新率      | √         |
| 大师 Apps       | ApkMirror |
| 杜比音效        | √         |
| 相机键快速启动  | √         |
| GApps           | √         |
| 人脸解锁        | √         |
| 自定义          | 丰富      |

Bug：

| BUG                  | 详情                           |
| -------------------- | ------------------------------ |
| 主题颜色不统一       | 下拉状态栏等处图标与文字黑白配 |
| 杜比音效声音忽大忽小 | 关闭杜比音效可以解决           |
| 自带通知音效均无声音 | 需要手动添加自定义音效、铃声   |

补充：

- 自带 Root 权限 - KernelSU GKI 模式，可选不带 Root 内核。
- Play Integrity Fix 可用。

### LineageOS [Official](https://wiki.lineageos.org/devices/pdx234/)

版本：0630

功能：

| 功能            | 详情                                                              |
| --------------- | ----------------------------------------------------------------- |
| 大师模式        | √                                                                 |
| 完整分辨率 / 4K | √                                                                 |
| 全高刷新率      | √                                                                 |
| 大师 Apps       | ApkMirror                                                         |
| 杜比音效        | ×                                                                 |
| 相机键快速启动  | √                                                                 |
| GApps           | MindTheGApps                                                      |
| 人脸解锁        | ×                                                                 |
| 自定义          | 适中，包含：状态栏网速、电池图标、隐藏手势 💊、隐藏启动器抽屉应用 |

Bug：

| BUG                             | 详情                                |
| ------------------------------- | ----------------------------------- |
| 美团无法使用，银行 App 无法使用 | 美团显示无网络，银行 App 白屏、卡死 |
| 指纹图标指示器位置不对          | 指示在音量键处                      |
| 短信对话页面需要返回两次        | ？                                  |
| 短信通知无快速“已读”操作        | 也许是特性？...                     |

补充：

- 不可使用 KernelSU Root，可刷入 DerpFest 内核获取 GKI 模式 Root 权限。
- Play Integrity Fix 可用。

## 注意事项

- 音量上 + 电源 = Bootloader - 蓝色灯
- 音量下 + 电源 = SOMC Flash Mode - 绿色灯
