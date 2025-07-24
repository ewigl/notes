---
title: "使用 Steam Console 下载 Depot"
date: 2024-06-23

cover:
  image: "images/shared/steam.webp"
  alt: "Cover"
summary: "下载旧版本游戏或者单独下载 DLC 等额外内容。"
description: "下载旧版本游戏或者单独下载 DLC 等额外内容。"

tags: ["Steam"]
---

## 使用 SteamDB 获取游戏 depot 信息

[SteamDB](https://steamdb.info/)

## 开启 Steam 控制台

Win + R

```
steam://open/console
```

## Steam 控制台命令格式

```
download_depot {APPID} {DEPOTID} {MANIFESTID}
```

## 示例：下载 Mirror Emoji

```
download_depot 644560 1120630 5362505210744167703
```

## 示例： 下载 SkyrimSE.exe - 1.6.640

```
download_depot 489830 489833 5291801952219815735
```

## 示例： 下载 Skyrim SE - 1.5.97 All

```
download_depot 489830 489831 7848722008564294070
download_depot 489830 489832 8702665189575304780
download_depot 489830 489833 2289561010626853674
```
