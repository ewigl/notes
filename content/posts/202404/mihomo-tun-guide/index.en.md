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
2. Modify `config.yaml`.

   - If you are using a subscription service, uncomment all `- Subscription` lines and fill your subscription link in the `Subscription` section under `proxy-providers`.

     `config.yaml`

     ```yaml
     proxy-groups:
       # ...
       - name: 🇺🇸 America
         type: select
         use:
           # - Local
           - Subscription
         filter: "US|🇺🇸"
       # ...

     proxy-providers:
       # Local:
       #   type: file
       #   path: ./proxies/Local.yaml
       #   health-check:
       #     enable: true
       #     url: http://www.gstatic.com/generate_204
       #     interval: 7200

       Subscription:
         type: http
         # your subscription url here
         url: https://your.subscription.url
         path: ./proxies/Subscription.yaml
         health-check:
           enable: true
           url: http://www.gstatic.com/generate_204
           interval: 7200
     ```

   - If you use self-host servers or want to store server information locally, create a folder named `proxies`, create a file named `Local.yaml` in `proxies`.

     `Local.yaml`(Format reference: Mihomo Docs)

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

![Preview](./images/0.png)

## References

[Mihomo](https://github.com/MetaCubeX/mihomo)

[Box For Root](https://github.com/taamarin/box_for_magisk)

[Mihomo Docs](https://wiki.metacubex.one/config/)

[Mihomo Params](https://ewigl.github.io/notes/en/posts/202404/mihomo-params/)
