---
title: "Mihomo Tun 模式配置"
date: 2024-07-31

cover:
  image: "images/shared/keyboard-light.webp"
  alt: "Cover"
summary: "https://github.com/ewigl/mihomo"
description: "https://github.com/ewigl/mihomo"

tags: ["Mihomo", "Tun", "Windows", "Android"]
---

## 准备

1. 下载 [Mihomo Core](https://github.com/MetaCubeX/mihomo/releases)。
2. 在[这里](https://github.com/Loyalsoldier/v2ray-rules-dat/releases)下载 `GeoIP.dat` 、 `GeoSite.dat`。
3. 在[这里](https://github.com/MetaCubeX/metacubexd/releases)下载 `metacubexd`。
4. Android 版本需要 [Box for Root](https://github.com/taamarin/box_for_magisk/releases)。

## Windows 配置

### 目录结构

```
.
└── D:/Apps/Mihomo/
    ├── config.yaml
    ├── GeoIP.dat
    ├── GeoSite.dat
    ├── Mihomo StartUp.xml
    ├── mihomo-windows-amd64.exe
    ├── mihomo.startup.vbs
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

1.  点击 <font color="#1f883d">Code</font> -> Download ZIP， 解压缩。
2.  修改 `config.yaml`。

    - 如果使用订阅服务，在 `config.yaml` 文件中的 `Subscription` 中填上订阅链接。

      `config.yaml`片段示例：

      ```yaml
      proxy-groups:
        - name: 🚀
          type: select
          proxies:
            - 🇺🇸 美国
            - 🇭🇰 香港
            - 🇨🇳 台湾
            - 🇸🇬 狮城
            - 🇯🇵 日本
            - 🇺🇳 全球

        # Regions
        - name: 🇺🇸 美国
          type: select
          use:
            # - Local
            - Subscription
          filter: "US|🇺🇸|美国"

        - name: 🇭🇰 香港
          type: select
          use:
            # - Local
            - Subscription
          filter: "HK|🇭🇰|香港"

        - name: 🇨🇳 台湾
          type: select
          use:
            # - Local
            - Subscription
          filter: "TW|🇨🇳|🇹🇼|台湾"

        - name: 🇸🇬 狮城
          type: select
          use:
            # - Local
            - Subscription
          filter: "SG|🇸🇬|新加坡|狮城"

        - name: 🇯🇵 日本
          type: select
          use:
            # - Local
            - Subscription
          filter: "JP|🇯🇵|日本"

        - name: 🇺🇳 全球
          type: select
          use:
            # - Local
            - Subscription

      proxy-providers:
        # 注释掉 “Local:” 部分
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

    - 如果使用自建服务器或在本地存储服务器信息，创建 `proxies` 文件夹，在 `proxies` 内创建 `Local.yaml` 文件。

      `config.yaml`片段示例：

      ```yaml
      proxy-groups:
        - name: 🚀
          type: select
          proxies:
            - 🇺🇸 美国
            - 🇭🇰 香港
            - 🇨🇳 台湾
            - 🇸🇬 狮城
            - 🇯🇵 日本
            - 🇺🇳 全球

        # Regions
        - name: 🇺🇸 美国
          type: select
          use:
            - Local
            # - Subscription
          filter: "US|🇺🇸|美国"

        - name: 🇭🇰 香港
          type: select
          use:
            - Local
            # - Subscription
          filter: "HK|🇭🇰|香港"

        - name: 🇨🇳 台湾
          type: select
          use:
            - Local
            # - Subscription
          filter: "TW|🇨🇳|🇹🇼|台湾"

        - name: 🇸🇬 狮城
          type: select
          use:
            - Local
            # - Subscription
          filter: "SG|🇸🇬|新加坡|狮城"

        - name: 🇯🇵 日本
          type: select
          use:
            - Local
            # - Subscription
          filter: "JP|🇯🇵|日本"

        - name: 🇺🇳 全球
          type: select
          use:
            - Local
            # - Subscription

      proxy-providers:
        Local:
          type: file
          path: ./proxies/Local.yaml
          health-check:
            enable: true
            url: http://www.gstatic.com/generate_204
            interval: 7200

        # Subscription:
        #   type: http
        #   # your subscription url here
        #   url: https://your.subscription.url
        #   path: ./proxies/Subscription.yaml
        #   health-check:
        #     enable: true
        #     url: http://www.gstatic.com/generate_204
        #     interval: 7200
      ```

      `Local.yaml`示例：

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
4.  双击 `mihomo.startup.vbs` 运行。
5.  控制台：[http://localhost:9090/ui](http://localhost:9090/ui)。
6.  默认密码：`998486`，可在 `config.yaml` 中修改。

### 开机自启

1. 打开 Windows 任务计划程序
2. 导入 `Mihomo StartUp.xml`，或新建一个任务来开机运行 `mihomo.startup.vbs`.
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
        ├── GeoIP.dat
        └── GeoSite.dat
```

### 配置流程

0.  刷入 Box For Root，无需立刻重启。
1.  修改 `config.yaml`。（步骤参考 Windows 配置第二步）
2.  下载 mihomo android arm64 版本，解压缩并重命名为 `mihomo`。复制 `mihomo` 到 `/data/adb/box/bin/xclash`.
3.  复制 `custom-rules`, `metacubexd`, `proxies(可选)`, `GeoIP.dat`, `GeoSite.dat` 到 `/data/adb/box/calsh`.
4.  修改 `/data/adb/box` 中的 `settings.ini`，将 `network_mode` 设置为 “tun”。
5.  重启。
6.  控制台：[http://localhost:9090/ui](http://localhost:9090/ui)。
7.  默认密码：`998486`，可在 `config.yaml` 中修改。

### 注意事项

1.  在 APatch、KernelSU、Magisk 的模块管理界面，启用或停用该模块可以控制内核的启动、停止。无需重启，立即生效。
2.  Log 文件在 `/data/adb/box/run` 文件夹中。

## 参考文档

[Mihomo](https://github.com/MetaCubeX/mihomo)

[Mihomo Docs](https://wiki.metacubex.one/config/)

[Mihomo Params](https://ewigl.github.io/notes/posts/202404/mihomo-params/)

[Box For Root](https://github.com/taamarin/box_for_magisk)

## WARNING

这是实现 tun 模式的简单配置，更多定制功能可参考官方文档。
