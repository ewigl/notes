---
title: "Mihomo 配置"
date: 2024-12-05

cover:
  image: "images/shared/keyboard-light.webp"
  alt: "Cover"
summary: "Mihomo Tun 模式配置，用于 Windows 和 Android 设备。包含自定义规则。"
description: "Mihomo Tun 模式配置，用于 Windows 和 Android 设备。包含自定义规则。"

tags: ["Mihomo", "Windows", "Android"]
---

## 仓库

https://github.com/ewigl/mihomo

## 预览

![00](/notes/posts/programming/mihomo-tun-guide/images/00.png)

![01](/notes/posts/programming/mihomo-tun-guide/images/01.png)

![02](/notes/posts/programming/mihomo-tun-guide/images/02.png)

![03](/notes/posts/programming/mihomo-tun-guide/images/03.png)

## Windows 配置

- 从 [Release](https://github.com/ewigl/mihomo/releases/latest) 下载 windows-\*.zip，解压缩。
- 整理现有文件到如下目录结构。

### 目录结构

```
.
└── D:/Apps/Mihomo/
    ├── config.yaml
    ├── mihomo-windows-amd64.exe
    ├── mihomo.start.vbs
    ├── Mihomo.Startup.xml
    ├── mihomo.stop.bat
    ├── custom-rules/
    │   ├── direct.yaml
    │   ├── proxy.yaml
    │   └── reject.yaml
    ├── zashboard/
    │   ├── index.html
    │   └── ...
    └── proxies/
        └── Local.yaml
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
          url: 这里填订阅链接
          health-check:
            enable: true
            url: http://www.gstatic.com/generate_204
            interval: 7200

        订阅名称随意，不重复即可:
          type: http
          url: 这里填订阅链接
          health-check:
            enable: true
            url: http://www.gstatic.com/generate_204
            interval: 7200
      ```

    - 如果希望在本地存储节点信息，无需修改 `config.yaml`。创建 `proxies` 文件夹，在 `proxies` 内创建 `Local.yaml` 文件。`Local.yaml` 文件内容可以通过 [ACL4SSR](https://acl4ssr-sub.github.io/) 等订阅转换服务获得（勾选“仅输出节点信息”）。

      `Local.yaml` 文件内容示例：

      ```yaml
      proxies:
        - {
            name: 🇭🇰 HongKong Example,
            server: hongkong.server.example,
            port: 12345,
            type: ss,
            cipher: chacha20-ietf-poly1305,
            password: 123456789,
            udp: true,
          }
        - {
            name: 🇭🇰 HongKong 示例,
            server: 香港.节点.示例,
            port: 12345,
            type: ss,
            cipher: chacha20-ietf-poly1305,
            password: 123456789,
            udp: true,
          }
      ```

1.  在 `mihomo-windows-amd64.exe` 上右键 -> 属性 -> 兼容性，勾选“以管理员权限身份运行此程序” **（Tun 模式需要管理员权限）**。
1.  双击 `mihomo.start.vbs` 运行。
1.  浏览器访问控制台：[http://localhost:9090/ui](http://localhost:9090/ui)。
1.  默认密码：`998486`，可在 `config.yaml` 中修改。

### 开机自启

> 需注意设置正确的文件路径。

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
2. 从 [Release](https://github.com/ewigl/mihomo/releases/latest) 下载 android-\*.zip。
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
        ├── proxies/
        ├── zashboard/
        └── config.yaml
```

### 配置流程

1.  修改 `config.yaml`。（参考 Windows 配置流程）
2.  【可选】修改 `/data/adb/box` 中的 `settings.ini`，将 `network_mode` 设置为 “tun”。
3.  重启。
4.  浏览器访问控制台：[http://localhost:9090/ui](http://localhost:9090/ui)。
5.  默认密码：`998486`，可在 `config.yaml` 中修改。

### 注意事项

2.  在 APatch、Magisk、KernelSU 的模块管理界面, 可以通过“执行”按钮开关 mihomo。
3.  Log 文件在 `/data/adb/box/run` 文件夹中。

## 规则配置

- 自定义规则具有最高优先级，可以按照需求修改。规则位于 `custom-rules` 目录内，修改后在 WebUI 刷新规则即可生效。规则示例：

  - 直连：`direct.yaml`

    ```yaml
    payload:
      # 强制 Steam 登陆服务器 steamserver.net 直连，影响 Steam 选择下载服务器。
      - "+.steamserver.net"
    ```

  - 代理：`proxy.yaml`

    ```yaml
    payload:
      # 强制 Kox Moe 走代理。
      - "+.kox.moe"
      - "+.mxomo.com"
    ```

  - 拒绝：`reject.yaml`

    ```yaml
    payload:
      # 强制拦截 Adobe.IO 相关请求。
      - "+.adobe.io"
    ```

## WARNING

这是实现 Tun 模式的简单配置，使用默认 DNS，使用 MetaCubeX 默认规则集，更多定制功能请参考[官方文档](https://wiki.metacubex.one/)。
