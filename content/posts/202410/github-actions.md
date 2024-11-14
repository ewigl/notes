---
title: "Github Actions"
date: 2024-10-05

cover:
  image: "images/shared/terminal.webp"
  alt: "Cover"
summary: Github Actions 基本使用
description: Github Actions 基本使用

tags: ["Github"]
---

## 启用 Github Actions (Fork 后)

![03](/notes/posts/202410/images/03.png)

## 配置 Environment Secrets

![00](/notes/posts/202410/images/00.png)

![01](/notes/posts/202410/images/01.png)

## 应用场景

### [HIFINI 音乐磁场 自动签到](https://github.com/ewigl/hifini-auto-checkin)

#### ENV

`HIFINI`

#### Secrets

- COOKIE: `bbs_sid=YourBbs_Sid;bbs_token=YourBbs_Token...`
  ![02](/notes/posts/202410/images/02.png)

### [iKuuu 自动签到](https://github.com/ewigl/ikuuu-auto-checkin)

#### ENV

`IKUUU`

#### Secrets

- EMAIL:`email@example.com`
- PASSWD: `YourPassword`
- HOST: 网站域名，`ikuuu.one`、`ikuuu.org`等。

### [PicAcg 哔咔漫画 自动签到](https://github.com/ewigl/picacg-auto-checkin)

#### ENV

`PICACG`

#### Secrets

- EMAIL:`email@example.com`
- PASSWD: `YourPassword`
