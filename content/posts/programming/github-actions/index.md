---
title: "Github Actions"
date: 2025-03-23

cover:
  image: "images/shared/terminal.webp"
  alt: "Cover"
summary: 无需个人服务器，利用 GitHub Actions 执行自动任务。
description: 无需个人服务器，利用 GitHub Actions 执行自动任务。

tags: ["Github"]
---

> 示例:
>
> - [HIFITI 音乐磁场 定时自动签到](https://github.com/ewigl/hifiti-auto-checkin)
> - [iKuuu 机场 定时自动签到](https://github.com/ewigl/ikuuu-auto-checkin)
> - [PicACG 哔咔漫画 定时自动签到](https://github.com/ewigl/picacg-auto-checkin)
> - [ZodGame 定时自动签到](https://github.com/ewigl/zodgame-auto-checkin)

## 用法

### 1. Fork 仓库

点击仓库右上角 Fork 按钮将仓库复制到自己的 GitHub 账户。

![08](/notes/posts/programming/github-actions/images/08.png)

![09](/notes/posts/programming/github-actions/images/09.png)

### 2. 启用 Actions

在自己仓库的左上角找到 Actions 标签页。启用 Workflows。

![03](/notes/posts/programming/github-actions/images/03.png)

### 3. 配置 Actions 变量

在仓库的左上角找到 Settings 标签页，选择 Secrets and variables。新建 Actions 变量。

![01](/notes/posts/programming/github-actions/images/01.png)

![02](/notes/posts/programming/github-actions/images/02.png)

<!-- ![11](/notes/posts/programming/github-actions/images/11.png)
![12](/notes/posts/programming/github-actions/images/12.png) -->

## FAQ

### 手动触发任务

![05](/notes/posts/programming/github-actions/images/05.png)

### 查看运行详情

![06](/notes/posts/programming/github-actions/images/06.png)

### 任务运行时间

修改 Checkin.yml 中的时间表即可，希望运行多次添加多行 crontab 即可。

时区为 UTC。且 GitHub Actions 定时任务存在时间延迟。尽量避免将时间设置在高峰时段（零点、八点九点等整点时段）。

![10](/notes/posts/programming/github-actions/images/10.png)
