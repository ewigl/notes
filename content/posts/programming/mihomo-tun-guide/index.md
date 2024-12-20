---
title: "Mihomo Tun 模式配置"
date: 2024-12-05

cover:
  image: "images/shared/keyboard-light.webp"
  alt: "Cover"
summary: "Mihomo Tun 模式配置，用于 Windows 和 Android 设备。包含简单的自定义规则。"
description: "Mihomo Tun 模式配置，用于 Windows 和 Android 设备。包含简单的自定义规则。"

tags: ["Mihomo", "Windows", "Android"]
---

## 介绍

- 系统代理模式默认无法代理命令行程序（小黑框）、UWP 应用等。
- Tun 模式的原理是虚拟网卡，因此可以代理所有系统网络流量。
- 相较于使用路由器进行局域网代理，Tun 模式不会影响局域网中其他设备。
- Tun 模式对 PC 的性能影响几乎可以忽略不计。
- Tun 模式 / 透明代理模式会略微增加 Android 设备耗电。优点是可以常驻代理，且无前台程序。
- 本项目无 GUI 软件。即不需要额外的软件，直接运行 Mihomo 内核即可实现 Tun 模式。
- 使用浏览器通过 WebUI 即可控制代理设置。

## 预览

![00](/notes/posts/programming/mihomo-tun-guide/images/00.png)

![01](/notes/posts/programming/mihomo-tun-guide/images/01.png)

## 链接

| 项目                                                                | 说明                                |
| ------------------------------------------------------------------- | ----------------------------------- |
| [ewigl/mihomo](https://github.com/ewigl/mihomo)                     | Tun 模式配置 (本项目)               |
| [Mihomo](https://github.com/MetaCubeX/mihomo/releases)              | Mihomo 内核                         |
| [GeoIP](https://github.com/MetaCubeX/meta-rules-dat/releases)       | geoip.metadb                        |
| [Metacubexd](https://github.com/MetaCubeX/metacubexd/releases)      | Web UI 控制台                       |
| [Box for Root](https://github.com/taamarin/box_for_magisk/releases) | Android Apatch/KernelSU/Magisk 模块 |

## 准备

### Windows

1. 下载 Mihomo Windows 内核。

### Android

1. 通过 Magisk / KernelSU / Apatch 获取设备 root 权限。
2. 下载 `Box for Root`。
3. 下载 Mihomo Android 内核。

### 共通

1. 下载本项目。
2. 下载 `geoip.metadb`。
3. 下载 `metacubexd`。
4. 按照目录结构整理好文件。

## Windows 配置

### 目录结构

```
.
└── D:/Apps/Mihomo/
    ├── config.yaml
    ├── geoip.metadb
    ├── mihomo-windows-amd64.exe
    ├── mihomo.start.vbs
    ├── Mihomo.Startup.xml
    ├── mihomo.stop.bat
    ├── README.md
    ├── custom-rules/
    │   ├── direct.yaml
    │   ├── proxy.yaml
    │   └── reject.yaml
    ├── metacubexd/
    │   ├── index.html
    │   └── ...
    ├── proxies/
    │   ├── Local.yaml
    │   └── ...
    └── ruleset/
        ├── proxy.yaml
        └── ...
```

### 配置流程

1.  在本项目首页，点击 <font color="#1f883d">Code</font> -> Download ZIP 将项目下载到本地，解压缩。
2.  修改 `config.yaml`。

    - 如果使用订阅服务，在 `config.yaml` 文件中的 `Subscription` 中填上订阅链接，注释掉 `Local` 部分。

      `config.yaml`文件片段示例：

      ```yaml
      used-in-proxy-groups: &used-in-proxy-groups
        type: select
        use:
          # 注释掉 Local
          # - Local
          - Subscription

      proxy-providers:
        # 注释掉 Local 部分
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

    - 如果在本地存储服务器信息，无需修改 `config.yaml`。创建 `proxies` 文件夹，在 `proxies` 内创建 `Local.yaml` 文件。
      `Local.yaml` 文件内容可以通过 [订阅转换](https://acl4ssr-sub.github.io/) 服务获得。

      `Local.yaml` 文件内容示例：

      ```yaml
      proxies:
        - {
            name: 🇺🇸 美国,
            server: us.server,
            port: 8848,
            type: ss,
            cipher: chacha20-ietf-poly1305,
            password: 12345678,
            udp: true,
          }
        - {
            name: 🇭🇰 香港,
            server: hongkong.server,
            port: 8848,
            type: ss,
            cipher: chacha20-ietf-poly1305,
            password: 12345678,
            udp: true,
          }
      ```

3.  在 `mihomo-windows-amd64.exe` 上右键 -> 属性 -> 兼容性，勾选“以管理员权限身份运行此程序” **（Tun 模式需要管理员权限）**。
4.  双击 `mihomo.start.vbs` 运行。
5.  控制台：[http://localhost:9090/ui](http://localhost:9090/ui)。
6.  默认密码：`998486`，可在 `config.yaml` 中修改。

### 开机自启

1. 打开 Windows 任务计划程序
2. 导入 `Mihomo.Startup.xml`，或新建一个任务来开机运行 `mihomo.start.vbs`.
3. 按需修改任务名称、**文件路径**、触发器、条件等等。
4. **在“常规”选项卡中， 勾选“使用最高权限运行”**。（如果不设置此选项，每次启动会跳出 UAC 窗口）

### 停止服务

双击运行 `mihomo.stop.bat`。

或打开任务管理器，结束 `mihomo-windows-amd64.exe`。

## Android 配置

### 目录结构

```
.
└── /data/adb/box/
    ├── bin/
    │   └── xclash/
    │       └── mihomo
    └── clash/
        ├── metacubexd/
        ├── proxies/
        ├── ruleset/
        ├── config.yaml
        └── geoip.metadb
```

### 配置流程

0.  刷入 Box For Root，无需立刻重启。
1.  修改 `config.yaml`。（参考 Windows 配置流程）
2.  下载 mihomo android 版本内核，解压缩并重命名为 `mihomo`。复制 `mihomo` 到 `/data/adb/box/bin/xclash`.
3.  复制 `custom-rules`, `metacubexd`, `proxies(可选)`, `geoip.metadb` 到 `/data/adb/box/calsh`.
4.  【可选】修改 `/data/adb/box` 中的 `settings.ini`，将 `network_mode` 设置为 “tun”。

    你也可以使用默认的 tproxy 模式，tproxy 模式可以仅代理（或不代理）指定的应用程序，具体设置参考 BFR 的文档。

5.  重启。
6.  控制台：[http://localhost:9090/ui](http://localhost:9090/ui)。
7.  默认密码：`998486`，可在 `config.yaml` 中修改。

### 注意事项

1.  在 APatch、KernelSU、Magisk 的模块管理界面，启用或停用该模块可以控制内核的启动、停止。无需重启，立即生效。
2.  Log 文件在 `/data/adb/box/run` 文件夹中。

## 规则配置

- 已内置简易自定义规则，修改 `custom-rules` 目录内的规则，后在 WebUI 刷新规则即可生效。

  - 直连：`direct.yaml`

    ```yaml
    payload:
      # 强制 gofile.io 直连.
      # - "+.gofile.io"
      # 强制 Steam 登陆服务器 steamserver.net 直连，影响 Steam 选择下载服务器。
      - "+.steamserver.net"
    ```

  - 代理：`proxy.yaml`

    ```yaml
    payload:
      # 强制 Kox Moe 走代理。
      - "+.kox.moe"
      - "+.mxomo.com"
      # 强制 LinkedIn 走代理。
      - "+.linkedin.com"
      # 强制 Anime 字幕论坛走代理。
      - "+.acgrip.com"
    ```

  - 拒绝：`reject.yaml`

    ```yaml
    payload:
      # 拦截 Adobe.IO 相关请求。
      - "+.adobe.io"
    ```

- 更进一步的自定义规则配置请参考 [Mihomo Docs](https://wiki.metacubex.one/config/rule-providers/)

## WARNING

这是实现 Tun 模式的简单配置，更多定制功能请参考官方文档。
