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

## [LineageOS 22.2](https://wiki.lineageos.org/devices/pdx234/)

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

- 可使用 Magisk 修补 init_boot 获取 Root 权限，难以隐藏。
- 可自主编译 KernelSU 内核获取 root 权限。
- APatch 会导致屏幕触控失灵。相关 Issue： https://github.com/bmax121/APatch/issues/934
- Integrity-Box 可用。

## 注意事项

> 如果系统未正确识别以下模式，需要在设备管理器处手动指定驱动程序。

- 音量上 + 电源 = Bootloader - 蓝色灯
- 音量下 + 电源 = SOMC Flash Mode - 绿色灯
