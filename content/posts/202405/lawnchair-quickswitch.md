---
title: "Lawnchair Quickswitch 集成"
date: 2024-05-18

summary: "Lawnchair Quickswitch 集成, Android 14, KSU"
description: "Lawnchair Quickswitch 集成, Android 14, KSU"

tags: ["Lawnchair", "Quickswitch", "Android"]
categories: ["软件", "指南", "Android"]
---

### 环境

- Xperia 1 V
- Android 14
- [KernelSU](https://github.com/tiann/KernelSU/releases) lastest
- [Quickswitch](https://github.com/skittles9823/QuickSwitch/releases) V[4.0.2](https://t.me/QuickstepSwitcherReleases)
- [Lawnchair](https://github.com/LawnchairLauncher/lawnchair/releases) latest Nightly

### 安装

- 安装 Lawnchair ，设为默认启动器。
- 使用 KernelSU 刷入 Quickswitch，重启。
- 使用终端 SU 权限运行 `/data/adb/modules/quickswitch/quickswitch --ch=app.lawnchair.debug`。
- 重启

### 常见问题

- Lawnchair beta 2 有 overlay 卡住的问题，所以必须使用 Nightly。
- Quickswitch V4.0.2 目前只 Telegram 群组中有。
