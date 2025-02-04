---
title: "Hide Windows Settings"
date: 2024-06-02T22:40:58+08:00

cover:
  image: "images/shared/windows.webp"
  alt: "Cover"
summary: "Hide Windows Settings"
description: "Hide Windows Settings"

tags: ["Windows"]
---

1. WIN + R
2. input `gpedit.msc`, Enter, Open Local Group Policy Editor
3. Find `Computer Configuration - Manage Templates - Control Panel`
4. On the right side, find `Settings page visibility`
5. Refer to the help section, set the settings that need to be hidden, reference: [Microsoft Learn](https://go.microsoft.com/fwlink/?linkid=2102995)
6. Check "Enabled"
7. Input Example

   ```
   hide:maps;search-permissions;cortana-windowssearch;tabletmode;project;crossdevice;autoplay;usb;mobile-devices;speech;gaming-gamedvr;easeofaccess-eyecontrol;easeofaccess-highcontrast;easeofaccess-colorfilter;findmydevice;gaming-gamebar;
   ```
