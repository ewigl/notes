---
title: "Github Actions 自动任务"
date: 2025-03-23

cover:
  image: "images/shared/terminal.webp"
  alt: "Cover"
summary: 无需个人服务器，利用 GitHub Actions 执行自动任务。
description: 无需个人服务器，利用 GitHub Actions 执行自动任务。

tags: ["Github"]
---

> 示例项目:
>
> - [HIFINI 音乐磁场 定时自动签到](https://github.com/ewigl/hifini-auto-checkin)
> - [iKuuu 机场 定时自动签到](https://github.com/ewigl/ikuuu-auto-checkin)
> - [PicACG 哔咔漫画 定时自动签到](https://github.com/ewigl/picacg-auto-checkin)
> - [ZodGame 定时自动签到](https://github.com/ewigl/zodgame-auto-checkin)

## 示例项目用法

### 1. Fork 仓库

点击仓库右上角 Fork 按钮将仓库复制到自己的 GitHub 账户。

![08](/notes/posts/programming/github-actions/images/08.png)

![09](/notes/posts/programming/github-actions/images/09.png)

### 2. 启用 Actions

在自己仓库的左上角找到 Actions 标签页。启用 Workflows。

![03](/notes/posts/programming/github-actions/images/03.png)

### 3. 配置环境变量

在自己仓库的左上角找到 Settings 标签页，选择 Environments。新建一个环境。

**仓库对应的环境：**

| 项目            | 环境变量 |
| --------------- | -------- |
| HIFINI 音乐磁场 | HIFINI   |
| iKuuu 机场      | IKUUU    |
| PicACG 哔咔漫画 | PICACG   |
| ZodGame         | ZODGAME  |

![00](/notes/posts/programming/github-actions/images/00.png)

点击新建的环境进入环境配置页面，在这里新建 Secrets 。

![01](/notes/posts/programming/github-actions/images/01.png)

![07](/notes/posts/programming/github-actions/images/07.png)

**环境对应的 Secrets：**

| 环境    | Secrets         | 说明                                                                                                                                                                                                                                                        |
| ------- | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| HIFINI  | COOKIE          | 打开 HIFINI 网站并登陆账号。打开浏览器控制台，输入 document.cookie，回车获取。不包含引号。 ![02](/notes/posts/programming/github-actions/images/02.png)                                                                                                     |
| IKUUU   | EMAIL PASSWD    | 邮箱、密码。 可选 Secrets：HOST（iKuuu 域名，默认是 ikuuu.one）                                                                                                                                                                                             |
| PICACG  | EMAIL PASSWD    | 邮箱、密码。                                                                                                                                                                                                                                                |
| ZODGAME | COOKIE FORMHASH | COOKIE 必须从网络请求标头中获取。 ![11](/notes/posts/programming/github-actions/images/11.png) FORMHASH 需要打开浏览器控制台，输入 document.querySelector('[name=formhash]').value，回车获取。 ![12](/notes/posts/programming/github-actions/images/12.png) |

## 示例项目 FAQ

### 手动触发任务

![05](/notes/posts/programming/github-actions/images/05.png)

### 查看运行详情

![06](/notes/posts/programming/github-actions/images/06.png)

### 任务运行时间

修改 Checkin.yml 中的时间表即可，希望运行多次添加多行 crontab 即可。

![10](/notes/posts/programming/github-actions/images/10.png)
