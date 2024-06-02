---
title: "Mihomo Tun 模式配置"
date: 2024-04-13

cover:
  image: "images/0.png"
  alt: "Cover"
summary: "https://github.com/ewigl/mihomo"
description: "https://github.com/ewigl/mihomo"

tags: ["Mihomo", "Tun"]
categories: ["软件", "指南", "Windows", "Android"]
---

## 目录结构

- custom-rules - 自定义规则，根据个人需求修改
- metacubexd - Web UI
- proxies - 代理服务器文件夹 (在本地存放你的服务器配置)

  ···

- mihomo.startup.vbs - VBS 脚本，实现隐藏小黑框启动
- mihomo.stop.bat - 停止 Mihomo
- Mihomo StartUp.xml - Windows 任务计划程序的备份文件
- updater.bat - 更新 Geo 数据文件和 Metacubexd 的脚本

## Windows 配置

1.  点击 <font color="#1f883d">Code</font> -> Download ZIP， 解压缩、放到你平时安装软件的地方。
2.  修改 `config.yaml`。

    - 如果你使用订阅服务，在 `config.yaml` 文件中的 `Subscription` 中填上你自己的订阅链接。

      `config.yaml`示例：

      ```yaml
      proxy-groups:
        # ...
        - name: 🇺🇸 America
          type: select
          use:
            # 不使用 Local 做 proxy-provider 的时候需要注释掉所有 proxy-groups 中的 “- Local"
            # - Local
            - Subscription
          filter: "US|🇺🇸"
        # ...

      proxy-providers:
        # 不想使用 Local 做 proxy-provider 的时候注释掉 “Local:” 部分
        # Local:
        #   type: file
        #   path: ./proxies/Local.yaml
        #   health-check:
        #     enable: true
        #     url: http://www.gstatic.com/generate_204
        #     interval: 7200

        Subscription:
          type: http
          # 订阅链接填这
          url: https://your.subscription.url
          path: ./proxies/Subscription.yaml
          health-check:
            enable: true
            url: http://www.gstatic.com/generate_204
            interval: 7200
      ```

    - 如果你使用自建服务器或想在本地存储服务器信息，创建一个 `proxies` 文件夹，在 `proxies` 文件夹中创建一个 `Local.yaml` 文件，并填上服务器信息（proxy-providers）。

      `Local.yaml:`(格式参考：[Mihomo Docs](https://wiki.metacubex.one/config/proxies/)，或使用各种订阅转换服务自动生成。)

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

3.  右键 -> 属性，修改 `mihomo-windows-amd64.exe` 的兼容性设置，勾选“以管理员权限身份运行此程序” **（Tun 模式需要管理员权限）**。
4.  双击 `mihomo.startup.vbs` 运行，允许管理员权限。
5.  控制台：[http://localhost:9090/ui](http://localhost:9090/ui)。默认密码：`998486`，可在 `config.yaml` 中修改。

### 开机自启并跳过 UAC

1. 打开 Windows 任务计划程序
2. 导入 `Mihomo StartUp.xml`，或新建一个任务来开机运行 `mihomo.startup.vbs`.
3. 按需修改任务名称、文件路径 **（必须修改，除非你的路径和我一样为"D:\Apps\Mihomo"）**、触发器、条件等等。
4. **在“常规”选项卡中， 勾选“使用最高权限运行”**。（如果不设置此选项，每次开机会跳出 UAC 窗口，除非你的 UAC 设置本来就是无警告（真的有人会这样做吗））

### 停止 Mihomo

双击运行 `mihomo.stop.bat`。

或者打开任务管理器，结束 `mihomo-windows-amd64.exe`.

## Android 配置

### Box For Root 使用方法:

0.  刷入 Box For Root，无需重启。
1.  修改 `config.yaml`。**（步骤参考 Windows 配置第二步）**
2.  下载 mihomo android arm64 版本，解压缩并重命名为 `mihomo`。复制 `mihomo` 到 `/data/adb/box/bin/xclash`.
3.  复制 `custom-rules`, `metacubexd`, `proxies(可选)`, `GeoIP.dat`, `GeoSite.dat` 到 `/data/adb/box/calsh`.
4.  修改 `/data/adb/box` 中的 `settings.ini`，将 `network_mode` 设置为 “tun”。
5.  重启。

### BFR FAQ

1.  控制台：[http://localhost:9090/ui](http://localhost:9090/ui)。默认密码：`998486`，可在 `config.yaml` 中修改。
2.  在 Magisk 或 KernelSU 的模块管理界面，启用或停用该模块可以控制内核的启动、停止。无需重启，立即生效。
3.  Log 文件在 `/data/adb/box/run` 文件夹中。

## 参考文档

[Mihomo](https://github.com/MetaCubeX/mihomo)

[Mihomo Docs](https://wiki.metacubex.one/config/)

[Mihomo Params](https://ewigl.github.io/notes/posts/202404/mihomo-params/)

[Box For Root](https://github.com/taamarin/box_for_magisk)

## FBI WARNING

这是实现 tun 模式的自用简单配置，更多定制功能自行参考官方文档。
