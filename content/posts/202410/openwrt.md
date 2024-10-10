---
title: "OpenWrt"
date: 2024-10-10

cover:
  image: "images/shared/openwrt.webp"
  alt: "Cover"
summary: OpenWrt 定制
description: OpenWrt 定制

tags: ["Router", "OpenWrt"]
---

## 自定义构建

[https://firmware-selector.openwrt.org/](https://firmware-selector.openwrt.org/)

### 可选 PKG

中文语言包

```
luci-i18n-base-zh-cn luci-i18n-firewall-zh-cn luci-i18n-opkg-zh-cn
```

curl

```
curl
```

ttyd (网页终端)

```
ttyd luci-app-ttyd luci-i18n-ttyd-zh-cn
```

### uci-defaults

```sh
# Beware! This script will be in /rom/etc/uci-defaults/ as part of the image.
# Uncomment lines to apply:
#
host_name="Licht_AX"
#
wlan_name="Licht_AX_5G"
wlan_password="Licht998486."
#
root_password="Licht998486."
lan_ip_address="192.168.8.1"

# log potential errors
exec >/tmp/setup.log 2>&1

if [ -n "$root_password" ]; then
(echo "$root_password"; sleep 1; echo "$root_password") | passwd > /dev/null
fi

# Set hostname & timezone
if [ -n "$host_name" ]; then
uci set system.@system[0].hostname="$host_name"
uci set system.@system[0].timezone='CST-8'
uci set system.@system[0].zonename='Asia/Shanghai'
uci commit system
fi

# Configure LAN
# More options: https://openwrt.org/docs/guide-user/base-system/basic-networking
if [ -n "$lan_ip_address" ]; then
uci set network.lan.ipaddr="$lan_ip_address"
uci commit network
fi

# Configure WLAN
# More options: https://openwrt.org/docs/guide-user/network/wifi/basic#wi-fi_interfaces
# 5G HZ WLAN @wifi-device[1]
if [ -n "$wlan_name" -a -n "$wlan_password" -a ${#wlan_password} -ge 8 ]; then
# Device
uci set wireless.@wifi-device[1].disabled='0'
uci set wireless.@wifi-device[1].country='US'
uci set wireless.@wifi-device[1].cell_density='2'
uci set wireless.@wifi-device[1].channel='64'
uci set wireless.@wifi-device[1].htmode='HE160'
# WIFI Interface
uci set wireless.@wifi-iface[1].disabled='0'
uci set wireless.@wifi-iface[1].encryption='psk2'
uci set wireless.@wifi-iface[1].ssid="$wlan_name"
uci set wireless.@wifi-iface[1].key="$wlan_password"
#
uci commit wireless
fi

echo "All done!"

```

## 代理工具

### OpenWrt-Mihomo (MihomoTProxy)

[https://github.com/morytyann/OpenWrt-mihomo/wiki](https://github.com/morytyann/OpenWrt-mihomo/wiki)

- 配置目录：/etc/mihomo/profiles
- 运行目录： /etc/mihomo/run
- UI 目录：/etc/mihomo/run/ui
- 路由器代理性能开销较小，局域网代理性能开销较大。
