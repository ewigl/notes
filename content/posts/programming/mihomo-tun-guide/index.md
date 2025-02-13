---
title: "Mihomo Tun 模式配置"
date: 2024-12-05

cover:
  image: "images/shared/keyboard-light.webp"
  alt: "Cover"
summary: "Mihomo Tun 模式配置，用于 Windows 和 Android 设备。包含自定义规则。"
description: "Mihomo Tun 模式配置，用于 Windows 和 Android 设备。包含自定义规则。"

tags: ["Mihomo", "Windows", "Android"]
---

## 介绍

> Github 仓库: https://github.com/ewigl/mihomo

- 无需额外软件使用 Mihomo 的方法，默认使用 Mihomo 内核自带 Tun 模式。
- 通过浏览器控制代理设置。
- 内置常用规则。

## 预览

![00](/notes/posts/programming/mihomo-tun-guide/images/00.png)

![01](/notes/posts/programming/mihomo-tun-guide/images/01.png)

## Windows 配置

1. 从 [Release](https://github.com/ewigl/mihomo/releases/tag/latest) 下载 MihomoWindows.zip。
2. 解压缩。
3. 整理现有文件到如下目录结构。

### 目录结构

```
.
└── D:/Apps/Mihomo/
    ├── config.yaml
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
        └── ...
```

### 配置流程

1.  修改 `config.yaml`。

    - 如果使用订阅服务，在 `config.yaml` 文件中的 `Subscription` 中填上订阅链接，注释掉 `Local` 部分。可以添加多个订阅。

      `config.yaml`文件片段示例：

      ```yaml
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
          health-check:
            enable: true
            url: http://www.gstatic.com/generate_204
            interval: 7200

        Subscription2:
          type: http
          # 订阅链接填这
          url: https://your.subscription.url.2
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

2.  在 `mihomo-windows-amd64.exe` 上右键 -> 属性 -> 兼容性，勾选“以管理员权限身份运行此程序” **（Tun 模式需要管理员权限）**。
3.  双击 `mihomo.start.vbs` 运行。
4.  控制台：[http://localhost:9090/ui](http://localhost:9090/ui)。
5.  默认密码：`998486`，可在 `config.yaml` 中修改。

### 开机自启

1. 打开 Windows 任务计划程序
2. 导入 `Mihomo.Startup.xml`，或新建一个任务来开机运行 `mihomo.start.vbs`.
3. 按需修改任务名称、**文件路径**、触发器、条件等等。
4. **在“常规”选项卡中， 勾选“使用最高权限运行”**。（如果不设置此选项，每次启动会跳出 UAC 窗口）

### 停止运行

双击运行 `mihomo.stop.bat`。

或打开任务管理器，结束 `mihomo-windows-amd64.exe`。

## Android 配置

0. 获取手机 Root 权限。
1. 下载 [Box for Root](https://github.com/taamarin/box_for_magisk/releases)，使用 Magisk / KernelSU / Apatch 刷入 Box For Root，**无需立刻重启**。
2. 从 [Release](https://github.com/ewigl/mihomo/releases/tag/latest) 下载 MihomoAndroid.zip。
3. 解压缩。
4. 整理现有文件到如下目录结构，`/data/adb/box/`为绝对路径。

### 目录结构

```
.
└── /data/adb/box/
    ├── bin/
    │   └── xclash/
    │       └── mihomo
    └── clash/
        ├── custom-rules/
        ├── metacubexd/
        ├── proxies/
        ├── ruleset/
        └── config.yaml
```

### 配置流程

1.  修改 `config.yaml`。（参考 Windows 配置流程）
2.  【可选】修改 `/data/adb/box` 中的 `settings.ini`，将 `network_mode` 设置为 “tun”。或者使用默认的 tproxy 模式，tproxy 模式可以仅代理（或不代理）指定的应用程序，具体设置参考 BFR 的文档。

3.  重启。
4.  控制台：[http://localhost:9090/ui](http://localhost:9090/ui)。
5.  默认密码：`998486`，可在 `config.yaml` 中修改。

### 注意事项

1.  在 APatch、KernelSU 的模块管理界面，启用或停用该模块可以控制内核的启动、停止。无需重启，立即生效。
2.  在 Magisk 的模块管理界面, 可以通过操作按钮开关代理。
3.  Log 文件在 `/data/adb/box/run` 文件夹中。

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

这是实现 Tun 模式的简单配置，使用默认 DNS，使用 MetaCubeX 默认规则集，更多定制功能请参考官方文档。
