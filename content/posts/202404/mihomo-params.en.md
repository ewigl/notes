---
title: "Mihomo Params"
date: 2024-04-12

cover:
  image: "images/shared/terminal.png"
  alt: "Cover"
summary: "Mihomo Command Line Parameters"
description: "Mihomo Command Line Parameters"

tags: ["Mihomo"]
---

### Source

[Mihomo source code](https://github.com/MetaCubeX/mihomo/blob/Meta/main.go)

### Code

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

### Parameters

| Parameter  | Parameter description                | Remarks                                                          |
| ---------- | ------------------------------------ | ---------------------------------------------------------------- |
| `-d`       | Set configuration directory          | `-d .` means using current directory                             |
| `-f`       | Specify configuration file           | `-f ./config.yaml` means using current directory's `config.yaml` |
| `-ext-ui`  | Override external UI directory       | Override configuration file's `external-ui` value                |
| `-ext-ctl` | Override external controller address | Override configuration file's `external-controller` value        |
| `-secret`  | Override RESTful API secret          | Override configuration file's `secret` value                     |
| `-m`       | Set geodata mode                     | Override configuration file's `geodata-mode` value               |
| `-v`       | Show current mihomo version          | -                                                                |
| `-t`       | Test configuration and exit          | Test configuration file's format                                 |
