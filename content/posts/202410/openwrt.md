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
uci set system.hostname="$host_name"
uci set system.timezone='CST-8'
uci set system.zonename='Asia/Shanghai'
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
uci set wireless.@wifi-device[1].hemode='HE160'
# WIFI Interface
uci set wireless.@wifi-iface[1].disabled='0'
uci set wireless.@wifi-iface[1].encryption='psk2'
uci set wireless.@wifi-iface[1].ssid="$wlan_name"
uci set wireless.@wifi-iface[1].key="$wlan_password"
#
uci commit wireless
fi

# Configure PPPoE
# More options: https://openwrt.org/docs/guide-user/network/wan/wan_interface_protocols#protocol_pppoe_ppp_over_ethernet
if [ -n "$pppoe_username" -a "$pppoe_password" ]; then
uci set network.wan.proto=pppoe
uci set network.wan.username="$pppoe_username"
uci set network.wan.password="$pppoe_password"
uci commit network
fi

echo "All done!"

```
