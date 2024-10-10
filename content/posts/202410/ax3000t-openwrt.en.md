---
title: "AX3000T X OpenWrt"
date: 2024-10-09

cover:
  image: "images/shared/terminal.webp"
  alt: "Cover"
summary:
description:

tags: ["Router", "OpenWrt", "AX3000T"]
---

## AX3000T Info

| Model        | AX3000T                                                                                      |
| ------------ | -------------------------------------------------------------------------------------------- |
| CPU          | MediaTek MT7981B                                                                             |
| Arch         | ARMv8 Processor rev 4 / AArch64 Cortex-A53                                                   |
| Platform     | Mediatek/Filogic                                                                             |
| Flash Size   | 128 MB                                                                                       |
| RAM          | 256 MB                                                                                       |
| OpenWrt Wiki | [https://openwrt.org/inbox/toh/xiaomi/ax3000t](https://openwrt.org/inbox/toh/xiaomi/ax3000t) |

## OpenWrt Flashing

1. From OpenWrt Wiki, We can use [XMiR-Patcher](https://github.com/openwrt-xiaomi/xmir-patcher).

## OpenWrt Notes

- AX3000T CN new version（production date 202408 or later）has different firmware, stock firmware is 1.0.84 +, no openwrt available yet.
- OP official tutorial no need to downgrade, support 1.0.64 and below official firmware version directly flash.
- XMiR-Patcher backup process may have Timed Out issue.
  Solution：[https://github.com/openwrt-xiaomi/xmir-patcher/issues/9#issuecomment-2209618296](https://github.com/openwrt-xiaomi/xmir-patcher/issues/9#issuecomment-2209618296)。
  Timeout set to 90 and use `extra options` menu to backup each partition separately.

## OpenWrt UBoot Flashing

- See OP official wiki.
- Use scp command to copy files from computer to router need using `-O` parameter.

## OpenWrt Wireless Settings

- 5G WIFI - Advanced Settings - Country Code Set to US。
- Signal Coverage Density, please set accordingly.
- General Settings - Maximum RSSI 24 dBm or Auto.
<!-- - 选择 AU 等国家代码可能会因为频率过高 (超过 6GHZ) 导致搜索不到 5G 信号。 -->
- Country Code AU or similar may cause 5G WIFI signal lost. (cause it's frequency is higher then 6GHZ)
