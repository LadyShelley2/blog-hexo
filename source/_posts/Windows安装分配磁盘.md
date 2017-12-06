---
title: Windows安装分配磁盘
date: 2017-12-06 11:21:13
tags:
---

弹出选择盘符的界面时，按 `shift + F10` 弹出命令行，输入`diskpart`命令进入磁盘管理。

```
list disk
list disk 
select disk 0 选择0号磁盘 
clean 清除磁盘 
convert gpt  转换为gpt格式 
创建EFI分区及系统安装分区： 
create partition efi size=100  创建EFI分区，大小100M 
create partition msr size=128  创建MSR分区，默认是 128M 
创建安装主分区 
create partition primary size=102400  主分区为100G （100*1024） 
```