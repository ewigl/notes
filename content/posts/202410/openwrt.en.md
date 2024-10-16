---
title: "OpenWrt"
date: 2024-10-10

cover:
  image: "images/shared/openwrt.webp"
  alt: "Cover"
summary: OpenWrt
description: OpenWrt

tags: ["Router", "OpenWrt"]
---

## Custom Build

[https://firmware-selector.openwrt.org/](https://firmware-selector.openwrt.org/)

### Optional PKGs

Chinese language packages

```
luci-i18n-base-zh-cn luci-i18n-firewall-zh-cn luci-i18n-opkg-zh-cn
```

curl

```
curl
```

SmartDNS

```
luci-app-smartdns luci-i18n-smartdns-zh-cn
```

SQM

```
luci-app-sqm luci-i18n-sqm-zh-cn
```

Attended Sysupgrade

```
luci-app-attendedsysupgrade luci-i18n-attendedsysupgrade-zh-cn
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

## Proxy Tools

### OpenWrt-Mihomo (MihomoTProxy)

[https://github.com/morytyann/OpenWrt-mihomo/wiki](https://github.com/morytyann/OpenWrt-mihomo/wiki)

- Configuration directory: /etc/mihomo/profiles
- Running directory: /etc/mihomo/run
- UI directory: /etc/mihomo/run/ui
- Router proxy has small performance impact.
- LAN proxy has big performance impact.
