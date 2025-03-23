---
title: "Github Actions"
date: 2025-03-23

cover:
  image: "images/shared/terminal.webp"
  alt: "Cover"
summary: 利用 GitHub Actions 执行自动任务。
description: 利用 GitHub Actions 执行自动任务。

tags: ["Github"]
---

> 利用 GitHub Actions 执行定时任务。
>
> 适用项目:
>
> - [HIFINI 音乐磁场 定时自动签到](https://github.com/ewigl/hifini-auto-checkin)
> - [iKuuu 定时自动签到](https://github.com/ewigl/ikuuu-auto-checkin)
> - [PicACG 哔咔漫画 定时自动签到](https://github.com/ewigl/picacg-auto-checkin)

## Fork 仓库

点击仓库右上角 Fork 按钮将仓库复制到自己的 GitHub 账户。

![08](/notes/posts/programming/github-actions/images/08.png)

![09](/notes/posts/programming/github-actions/images/09.png)

## 启用 Actions

在自己仓库的左上角找到 Actions 标签页。启用 Workflows。

![03](/notes/posts/programming/github-actions/images/03.png)

## 配置环境变量

### 环境变量

- **HIFINI 音乐磁场:**

  Environment: `HIFINI`

  Secrets: `COOKIE`(打开 HIFINI 网站并登陆账号。打开浏览器控制台，输入`document.cookie`，回车获取。不包含引号)

  ![02](/notes/posts/programming/github-actions/images/02.png)

- **iKuuu:**

  Environment: `IKUUU`

  Secrets: `EMAIL`(邮箱)，`PASSWD`(密码)，`HOST` (可以不配置，iKuuu 域名，默认是`ikuuu.one`)

- **PicAcg 哔咔漫画:**

  Environment: `PICACG`

  Secrets: `EMAIL`(邮箱)，`PASSWD`(密码)

### 配置流程

在自己仓库的左上角找到 Settings 标签页，选择 Environments。新建一个环境。
![00](/notes/posts/programming/github-actions/images/00.png)

点击环境名称进入环境配置页面，在这里新建变量（Secrets）。
![01](/notes/posts/programming/github-actions/images/01.png)

![07](/notes/posts/programming/github-actions/images/07.png)

## 常见问题

### 手动触发任务

![05](/notes/posts/programming/github-actions/images/05.png)

### 查看运行结果

![06](/notes/posts/programming/github-actions/images/06.png)

### 修改任务运行时间

修改 Checkin.yml 中的时间表即可。

![10](/notes/posts/programming/github-actions/images/10.png)
