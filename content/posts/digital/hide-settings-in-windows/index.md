---
title: "使用组策略隐藏 Windows 设置项"
date: 2024-06-02T22:40:58+08:00

cover:
  image: "images/shared/windows.webp"
  alt: "Cover"
summary: "隐藏 Windows 设置中的选项"
description: "隐藏 Windows 设置中的选项"

tags: ["Windows"]
---

1. WIN + R
2. 输入 `gpedit.msc`, 回车, 打开本地组策略编辑器
3. 找到 计算机配置 - 管理模板 - 控制面板
4. 在右侧窗口找到`设置页面可见性`
5. 根据帮助提示, 设置需要隐藏的设置选项, 参考文档: [Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/uwp/launch-resume/launch-settings-app)
6. 勾选`已启用`
7. 填写示例

   ```
   hide:maps;search-permissions;cortana-windowssearch;tabletmode;project;crossdevice;autoplay;usb;mobile-devices;speech;gaming-gamedvr;easeofaccess-eyecontrol;easeofaccess-highcontrast;easeofaccess-colorfilter;findmydevice;gaming-gamebar;
   ```
