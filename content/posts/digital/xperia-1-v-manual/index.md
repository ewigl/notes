---
title: "Sony Xperia 1 V"
date: 2025-11-14

cover:
  image: "images/shared/android.webp"
  alt: "Cover"
summary: Sony Xperia 1 V 系统更新，LineageOS，Root，自定义等相关记录。
description: Sony Xperia 1 V 系统更新，LineageOS，Root，自定义等相关记录。

tags: ["Android"]
---

## [LineageOS 23.0](https://wiki.lineageos.org/devices/pdx234/)

版本: `Latest`

### 功能

| 功能                                   | 详情                                        |
| -------------------------------------- | ------------------------------------------- |
| 创作者模式（BT.2020 色域和 10 位色深） | √                                           |
| 完整分辨率 / 4K                        | 支持但存在瑕疵                              |
| 全高刷新率                             | √                                           |
| 大师 Apps                              | ApkMirror                                   |
| 杜比音效                               | ×                                           |
| 相机键快速启动                         | √                                           |
| GApps                                  | MindTheGApps                                |
| 人脸解锁                               | ×                                           |
| 自定义                                 | 状态栏网速、电池图标、隐藏 💊、隐藏抽屉应用 |

### Bug

| BUG                       | 详情                                       |
| ------------------------- | ------------------------------------------ |
| 美团等少部分 App 无法使用 | 梆梆加固 / 国内 App 检测的原因，非系统 Bug |
| 指纹图标指示器位置不对    | 仅完整分辨率模式（4K）下有这个问题         |
| 短信对话页面需要返回两次  | 仅完整分辨率模式（4K）下有这个问题         |

### Root

- [SukiSU Ultra](https://github.com/sukisu-ultra/sukisu-ultra): [XDA](https://xdaforums.com/posts/90326019/), [GitHub](https://github.com/spacealtctrl/a16_sony_sm8550_SukiSU_SUSFS)
- [APatch](https://github.com/bmax121/APatch) 正常。
- Magisk 待测试。

补充:

SukiSU Ultra + Susfs 环境下 12306 在 play 商店无法下载，Apatch 正常，原因暂时不明。

### 修复 Play Integrity

依次安装:

- [ReZygisk](https://github.com/PerformanC/ReZygisk/releases)
- [Play integrity Fix](https://github.com/KOWX712/PlayIntegrityFix/releases)
- [TrickyStore](https://github.com/5ec1cff/TrickyStore)
- [TrickyStore Addon](https://github.com/KOWX712/Tricky-Addon-Update-Target-List/releases)
- [Yuri Keybox Manager](https://github.com/YurikeyDev/yurikey/releases)

重启

"执行" Yuri Keybox Manager。

## 备注

- 使用音量上下 + 电源键强制重启。

> 如果系统未正确识别以下模式，需要在设备管理器处手动指定驱动程序。

- 音量上 + 电源 = Bootloader - 蓝色灯
- 音量下 + 电源 = SOMC Flash Mode - 绿色灯
