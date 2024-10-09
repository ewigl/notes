---
title: "AX3000T X OpenWrt"
date: 2024-10-09

cover:
  image: "images/shared/openwrt.webp"
  alt: "Cover"
summary: 小米路由器 AX3000T 刷入官方 OpenWrt 教程
description: 小米路由器 AX3000T 刷入官方 OpenWrt 教程

tags: ["Router", "OpenWrt", "AX3000T"]
---

## AX3000T 基本信息

| Model        | AX3000T                                                                                      |
| ------------ | -------------------------------------------------------------------------------------------- |
| CPU          | MediaTek MT7981B                                                                             |
| Arch         | ARMv8 Processor rev 4 / AArch64 Cortex-A53                                                   |
| Platform     | Mediatek/Filogic                                                                             |
| Flash Size   | 128 MB                                                                                       |
| RAM          | 256 MB                                                                                       |
| OpenWrt Wiki | [https://openwrt.org/inbox/toh/xiaomi/ax3000t](https://openwrt.org/inbox/toh/xiaomi/ax3000t) |

## OpenWrt 刷入过程

1. 参考 OpenWrt Wiki 官方教程，使用 [XMiR-Patcher](https://github.com/openwrt-xiaomi/xmir-patcher) 按照提示即可刷入 OpenWrt。

## OpenWrt 注意事项

- AX3000T 新版本（生产日期约为 202408 后的批次）硬件不同，系统出厂版本为 1.0.84 +，暂无 OpenWrt 可用。
- OP 官方教程无需降级，支持 1.0.64 及以下官方固件版本直接刷机。
- 使用 XMiR-Patcher 备份过程中可能出现 Timed Out 的问题。
  解决方法：[https://github.com/openwrt-xiaomi/xmir-patcher/issues/9#issuecomment-2209618296](https://github.com/openwrt-xiaomi/xmir-patcher/issues/9#issuecomment-2209618296)。
  Timeout 设置为 90 并使用额外功能菜单中的单独备份模式分别备份各个分区。

## OpenWrt UBoot 刷入

- 使用 scp 命令在电脑与路由器之间拷贝文件时可使用 `-O` 参数。

## OpenWrt 官方自定义构建

- 使用[固件选择器](https://firmware-selector.openwrt.org/)自定义构建固件。
- 可选包 中文语言

```
luci-i18n-base-zh-cn luci-i18n-firewall-zh-cn luci-i18n-opkg-zh-cn
```

- 可选包 curl

```
curl
```

## OpenWrt 无线设置注意事项

- 5G WIFI - 高级设置 - 国家代码设置为 US。
- 信号覆盖密度酌情设置。
- 常规设置最大传输功率可选 24 dBm 或自动。
- 选择 AU 等国家代码可能会因为频率过高 (超过 6GHZ) 导致搜索不到 5G 信号。
