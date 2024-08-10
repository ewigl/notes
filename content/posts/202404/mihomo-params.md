---
title: "Mihomo 启动参数"
date: 2024-04-12

cover:
  image: "images/shared/terminal.webp"
  alt: "Cover"
summary: "Mihomo 命令行启动参数"
description: "Mihomo 命令行启动参数"

tags: ["Mihomo"]
---

### 来源

[Mihomo 源码](https://github.com/MetaCubeX/mihomo/blob/Meta/main.go)

### 源码

```go
func init() {
	flag.StringVar(&homeDir, "d", os.Getenv("CLASH_HOME_DIR"), "set configuration directory")
	flag.StringVar(&configFile, "f", os.Getenv("CLASH_CONFIG_FILE"), "specify configuration file")
	flag.StringVar(&externalUI, "ext-ui", os.Getenv("CLASH_OVERRIDE_EXTERNAL_UI_DIR"), "override external ui directory")
	flag.StringVar(&externalController, "ext-ctl", os.Getenv("CLASH_OVERRIDE_EXTERNAL_CONTROLLER"), "override external controller address")
	flag.StringVar(&secret, "secret", os.Getenv("CLASH_OVERRIDE_SECRET"), "override secret for RESTful API")
	flag.BoolVar(&geodataMode, "m", false, "set geodata mode")
	flag.BoolVar(&version, "v", false, "show current version of mihomo")
	flag.BoolVar(&testConfig, "t", false, "test configuration and exit")
	flag.Parse()
}

```

### 参数

| 参数       | 参数说明                     | 备注                                                  |
| ---------- | ---------------------------- | ----------------------------------------------------- |
| `-d`       | 设置配置文件所在目录         | `-d .` 表示使用当前目录                               |
| `-f`       | 指定配置文件                 | `-f ./config.yaml` 表示使用当前目录下的 `config.yaml` |
| `-ext-ui`  | 覆盖外部 UI 目录             | 覆盖配置文件中 `external-ui` 值                       |
| `-ext-ctl` | 覆盖外部控制台（Web UI）地址 | 覆盖配置文件中 `external-controller` 值               |
| `-secret`  | 覆盖 RESTful API 密钥        | 覆盖配置文件中 `secret` 值                            |
| `-m`       | 设置 geodata 模式            | 覆盖配置文件中 `geodata-mode` 值                      |
| `-v`       | 显示当前 mihomo 版本         | -                                                     |
| `-t`       | 测试配置文件并退出           | 测试配置文件是否（格式）正确                          |
