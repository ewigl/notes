+++
title = 'Mihomo Tun Mode'
date = 2024-04-13
description = "https://github.com/ewigl/mihomo" 
author = "Licht"
tags = ["Mihomo", "Tun"]
categories = ["Apps", "Guide" ]
+++

## Why

Because Tun Mode can enable the “global proxy” of all network traffic, including “small black box” and UWP applications.

## Directory structure

- box_for_root - Box For Root (Magisk / KernelSU Module) required files
- custom-rules - Custom rules, according to personal needs to modify
- metacubexd - Web UI using [Metacubexd](https://github.com/metacubex/metacubexd)
- proxies - Proxy server folder (store your server configuration, optional)
- proxies-example - Proxy server example folder (proxies folder structure example)

  ···

- mihomo.startup.vbs - .VBS for silent start, hide the "black box"
- Mihomo StartUp.xml - Windows Task Scheduler backup file
- update-geo-files.bat
- update-metacubexd.bat

## Windows configuration

1. Click <font color="#1f883d">Code</font> -> Download ZIP, unzip.
2. Modify `proxy-providers` in `config.yaml`.

   - If you are using a subscription service, fill in your subscription link in the `Subscription` section in `config.yaml`.

   - If you use a custom server or want to store server information locally, rename proxies-example to proxies and fill in the server information in Local.yaml. (Format reference: Mihomo Docs)

3. Modify `mihomo-windows-amd64.exe`'s compatiable settings, tick "admin permission".
4. Double click `mihomo.startup.vbs` to run, allow admin permission.
5. Controller dashboard：[http://localhost:9090/ui](http://localhost:9090/ui). default secret: `998486`, can be changed in `config.yaml`.

### Windows start up task and skip account control window

1. Open Windows Task Scheduler.
2. Import `Mihomo StartUp.xml`, or NEW a task to run `mihomo.startup.vbs`.
3. Change task's name, file path, triger, condition...
4. **In "General/Common" tab, tick 'admin/higherst permission'.**

### Stop Mihomo

In Task manager, end task `mihomo-windows-amd64.exe`.

Or use admin permission to run `mihomo.stop.bat`.

## Android configuration

### Box For Root usage:

0.  Bring Box For Root.
1.  Modify `proxy-providers` in `config.yaml`.

    - If you are using a subscription service, fill in your subscription link in the Subscription.

    - If you use a custom server or want to store server information locally, rename proxies-example to proxies and fill in the server information in Local.yaml. (Format reference: Mihomo Docs)

2.  Copy files from `box_for_root` to `/data/adb/box`.
3.  Copy `custom-rules`, `metacubexd`, `(proxies)`, `GeoIP.dat`, `GeoSite.dat` to `/data/adb/box/calsh`.
4.  Reboot.

## Preview

![Preview](https://raw.githubusercontent.com/ewigl/mihomo/main/images/0.png)

## References

[Mihomo](https://github.com/MetaCubeX/mihomo)

[Box For Root](https://github.com/taamarin/box_for_magisk)

[Mihomo Docs](https://wiki.metacubex.one/config/)

[Mihomo Params](https://ewigl.github.io/notes/en/posts/202404/mihomo-params/)
