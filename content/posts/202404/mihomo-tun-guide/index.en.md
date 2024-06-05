---
title: "Mihomo Tun Mode"
date: 2024-04-13

cover:
  image: "posts/202404/mihomo-tun-guide/images/0.png"
  alt: "Cover"
summary: "https://github.com/ewigl/mihomo"
description: "https://github.com/ewigl/mihomo"

tags: ["Mihomo", "Tun", "Windows", "Android"]
---

## Directory structure

- custom-rules - Custom rules, according to personal needs to modify
- metacubexd - Web UI
- proxies - Proxy server folder (store your server configuration locally)

  ···

- mihomo.startup.vbs - .VBS for silent start, hide the "black box"
- mihomo.stop.bat - Batch to stop Mihomo
- Mihomo StartUp.xml - Windows Task Scheduler backup file
- updater.bat - Script to update Geo data file and Metacubexd

## Windows configuration

1. Click <font color="#1f883d">Code</font> -> Download ZIP, unzip.
2. Modify `config.yaml`.

   - If you are using a subscription service, uncomment all `- Subscription` lines and fill your subscription link in the `Subscription` section under `proxy-providers`.

     `config.yaml`示例：

     ```yaml
     proxy-groups:
       # ...
       - name: 🇺🇸 America
         type: select
         use:
           # comment out all "- Local" in the `proxy-groups` section if you do not want to use local files
           # - Local
           - Subscription
         filter: "US|🇺🇸"
       # ...

     proxy-providers:
       # comment out "Local:" section in the `proxy-providers` section if you do not want to use local files
       # Local:
       #   type: file
       #   path: ./proxies/Local.yaml
       #   health-check:
       #     enable: true
       #     url: http://www.gstatic.com/generate_204
       #     interval: 7200

       Subscription:
         type: http
         # your subscription link here
         url: https://your.subscription.url
         path: ./proxies/Subscription.yaml
         health-check:
           enable: true
           url: http://www.gstatic.com/generate_204
           interval: 7200
     ```

   - If you use self-host servers or want to store server information locally, create a folder named `proxies`, create a file named `Local.yaml` in `proxies`.

     `Local.yaml`(Reference:[Mihomo Docs](https://wiki.metacubex.one/config/proxies/), or use any subscription converter.)

     ```yaml
     proxies:
       # shadowsocks
       - {
           name: 🇭🇰 HK,
           server: server.address.hk,
           port: 54321,
           type: ss,
           cipher: chacha20-ietf-poly1305,
           password: 123456789,
           udp: true,
         }
       # vmess
       - {
           name: 🇺🇸 US,
           server: 123.456.789.666,
           port: 443,
           type: vmess,
           uuid: 123456-7890-47c1-b1c3-6666666666666666,
           alterId: 0,
           cipher: auto,
           tls: true,
           skip-cert-verify: false,
           servername: rac.123456.xyz,
           network: ws,
           ws-opts: { path: /123456, headers: { Host: rac.123456.xyz } },
           udp: true,
         }
       # ...
     ```

3. Right click -> see properties, modify `mihomo-windows-amd64.exe`'s compatiable settings, tick "admin permission".
4. Double click `mihomo.startup.vbs` to run, allow admin permission.
5. Controller dashboard：[http://localhost:9090/ui](http://localhost:9090/ui). default secret: `998486`, can be changed in `config.yaml`.

### Windows start up task and skip UAC

1. Open Windows Task Scheduler.
2. Import `Mihomo StartUp.xml`, or NEW a task to run `mihomo.startup.vbs`.
3. Change task's name, file path, triger, condition...
4. **In "General/Common" tab, tick 'admin/higherst permission'.**

### Stop Mihomo

Run `mihomo.stop.bat`.

Or open Task Manager, terminate `mihomo-windows-amd64.exe`.

## Android configuration

### Box For Root usage

0.  Flash [Box For Root](https://github.com/taamarin/box_for_magisk) using Magisk or KernelSU, no need to reboot immediately.
1.  Modify `config.yaml`. (Steps same as Windows configuration above)
2.  Download mihomo android arm64 version, unzip and rename it to `mihomo`, copy `mihomo` to `/data/adb/box/bin/xclash`.
3.  Copy `custom-rules`, `metacubexd`, `proxies(optional)`, `GeoIP.dat`, `GeoSite.dat` to `/data/adb/box/calsh`.
4.  Modify `/data/adb/box` settings.ini, set `network_mode` to "tun".
5.  Reboot.

### BFR FAQ

1.  Controller dashboard：[http://localhost:9090/ui](http://localhost:9090/ui). default secret: `998486`, can be changed in `config.yaml`.
2.  In Magisk or KernelSU module manager, enable or disable the module to start or stop the proxy, No need to reboot.
3.  Log files in `/data/adb/box/run` folder.

## References

[Mihomo](https://github.com/MetaCubeX/mihomo)

[Mihomo Docs](https://wiki.metacubex.one/config/)

[Mihomo Params](https://ewigl.github.io/notes/en/posts/202404/mihomo-params/)

[Box For Root](https://github.com/taamarin/box_for_magisk)

## FBI WARNING

This is a simple implementation of tun mode, more customization features can be found in the official documentation.
