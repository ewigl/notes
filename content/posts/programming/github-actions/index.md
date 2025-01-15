---
title: "Github Actions"
date: 2024-11-27

cover:
  image: "images/shared/terminal.webp"
  alt: "Cover"
summary: Github Actions 基本使用
description: Github Actions 基本使用

tags: ["Github"]
---

## Fork 后启用 Actions

![03](/notes/posts/programming/github-actions/images/03.png)

## 配置环境及 Secrets

![00](/notes/posts/programming/github-actions/images/00.png)

![01](/notes/posts/programming/github-actions/images/01.png)

![07](/notes/posts/programming/github-actions/images/07.png)

## 应用场景

### [HIFINI 音乐磁场](https://github.com/ewigl/hifini-auto-checkin)

#### Environment: `HIFINI`

#### Secrets

1. **COOKIE**: 打开 HIFINI 网站控制台，输入`document.cookie`，回车获取。（不包含引号）

![02](/notes/posts/programming/github-actions/images/02.png)

### [iKuuu 爱坤呦呦](https://github.com/ewigl/ikuuu-auto-checkin)

#### Environment: `IKUUU`

#### Secrets

1. **EMAIL**: 邮箱，例如 `email@example.com`
2. **PASSWD**: 密码，例如 `YourPassword`
3. **HOST**: iKuuu 网站当前域名，可以不设置。例如`ikuuu.one`、`ikuuu.org`等。如果不设置，默认是`ikuuu.one`。

### [PicAcg 哔咔漫画](https://github.com/ewigl/picacg-auto-checkin)

#### Environment: `PICACG`

#### Secrets

1. **EMAIL**:`email@example.com`
2. **PASSWD**: `YourPassword`

## 查看运行结果

![05](/notes/posts/programming/github-actions/images/05.png)

![06](/notes/posts/programming/github-actions/images/06.png)
