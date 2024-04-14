+++
title = 'Mihomo Tun 模式配置'
date = 2024-04-13
description = "https://github.com/ewigl/mihomo" 
author = "Licht"
tags = ["Mihomo", "Tun"]
categories = ["软件", "指南" ]
+++

## 为什么

因为 Tun 模式可以实现真正意义上的“全局代理”，接管所有网络流量，包括“小黑框”、UWP 软件等。

## 目录结构

- box_for_root - Box For Root (Magisk / KernelSU 模块) 所需的文件
- custom-rules - 自定义规则，根据个人需求修改
- metacubexd - Web UI 使用 [Metacubexd](https://github.com/metacubex/metacubexd)
- proxies - 代理服务器文件夹 (存放你的服务器配置，可选)
- proxies-example - 代理服务器示例文件 (proxies 文件夹结构示例)

  ···

- mihomo.startup.vbs - VBS 脚本，实现隐藏小黑框启动
- Mihomo StartUp.xml - Windows 任务计划程序的备份文件
- update-geo-files.bat - 更新 Geo 数据文件的脚本
- update-metacubexd.bat - 更新 Metacubexd 控制台的脚本

## Windows 配置

1.  点击 <font color="#1f883d">Code</font> -> Download ZIP， 解压缩。
2.  修改 `config.yaml`。

    - 如果你使用订阅服务，在 `config.yaml` 文件中的 `Subscription` 中填上你自己的订阅链接。

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

    - 如果你使用自建服务器或想在本地存储服务器信息，创建一个 `proxies` 文件夹，并在 `proxies` 文件夹中创建一个 `Local.yaml` 文件，并填上服务器信息。

      `Local.yaml:`(格式参考：Mihomo Docs)

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

3.  **修改 `mihomo-windows-amd64.exe` 的兼容性设置，勾选“以管理员权限身份运行此程序”** (Tun 模式必须以管理员身份运行 Mihomo)。
4.  双击 `mihomo.startup.vbs` 运行，允许管理员权限
5.  控制台：[http://localhost:9090/ui](http://localhost:9090/ui)。默认密码：`998486`，可在 `config.yaml` 中修改。

### 设置开机自启并跳过管理员用户账户控制

1. 打开 Windows 任务计划程序
2. 导入 `Mihomo StartUp.xml`，或新建一个任务来开机运行 `mihomo.startup.vbs`.
3. 按需修改任务名称、文件路径、触发器、条件等等。
4. **在“常规”选项卡中， 勾选“使用最高权限运行”**。

### 停止 Mihomo

任务管理器，结束任务 `mihomo-windows-amd64.exe`.

或使用管理员权限运行 `mihomo.stop.bat`。

## Android 配置

### Box For Root 使用方法:

0.  刷入 Box For Root，无需重启。
1.  修改 `config.yaml` 中的 `proxy-providers` 配置。

    - 如果你使用订阅服务，在 Subscription 中填上你自己的订阅链接。

    - 如果你使用自建服务器或想在本地存储服务器信息，将 proxies-example 文件夹重命名为 proxies，并按照 Local.yaml 中的格式填写服务器信息。(更多格式参考 Mihomo Docs)

2.  复制 `box_for_root` 中的文件到 `/data/adb/box`.
3.  复制 `custom-rules`, `metacubexd`, `proxies(可选)`, `GeoIP.dat`, `GeoSite.dat` 到 `/data/adb/box/calsh`.
4.  重启

## 预览

![Preview](./images/0.png)

## 参考文档

[Mihomo](https://github.com/MetaCubeX/mihomo)

[Box For Root](https://github.com/taamarin/box_for_magisk)

[Mihomo Docs](https://wiki.metacubex.one/config/)

[Mihomo Params](https://ewigl.github.io/notes/posts/202404/mihomo-params/)
