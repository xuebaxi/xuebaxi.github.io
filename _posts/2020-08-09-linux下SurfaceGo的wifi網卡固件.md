---
title: "linux下SurfaceGo的wifi網卡固件"
date: 2020-08-09
last_modified_at: 2020-08-09
categories:
  - blog
tags:
  - SurfaceGo
  - Linux
permalink: /blog/2020_08_09_01
---
## 1. 去微軟官網下載固件

更新的名字叫做Qualcomm Atheros Communications Inc. - Net - 8/24/2018 12:00:00 AM - 12.0.0.722 [下載地址](https://www.catalog.update.microsoft.com/Search.aspx?q=Qualcomm%20Atheros%20Communications%20Inc.%20-%20Net%20-%208%2F24%2F2018%2012%3A00%3A00%20AM%20-%2012.0.0.722)
我下載的是11/16/2018 的

## 2.解壓得到固件

使用cabextract解壓cab文件，其中有我們需要的 eeprom_ar6320_3p0_TX8_lte_clpc.bin 文件相關信息如下

sha256sum: aec1c85301c593e303422cb2f54d27b27eca4efce59f065a127e8fb205233b37

md5sum: 8f2895dd63a0c8f11e2d051f0ed4e0a8

## 3.覆蓋原有的固件

將/lib/firmware/ath10k/QCA6174/hw3.0中的board-2.bin 和 board.bin刪除，用eeprom_ar6320_3p0_TX8_lte_clpc.bin替代board.bin。

### 参见
- - -
> ##### - https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=919652
