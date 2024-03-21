
---
author: longlikun
title : 在mac上面使用ntfs 硬盘
date : 2024-03-21T13:23:29+08:00
description: 在mac上使用netf 硬盘
draft: false
math: true
categories:
    - Test
    - 随笔

tags :
   - github

---


##### 方法一 使用命令行

在/etc下新建文件fstab

```bash
touch /etc/fstab
```

添加以下内容

```bash
LABEL=drivename none ntfs rw,auto,nobrowse
```

其中 drivename 为磁盘名称 名称不要有空格

可以通过以下命令查看磁盘名称

```bash
diskutil list
```



或者使用uuid

```bash
UUID=4485D2B9-C375-5240-8F5A-2225B24332EB none ntfs rw,auto,nobrowse
```

uuid 可以在`其他-磁盘工具-选中磁盘-简介`中找到



添加后访达中看不见硬盘 ，在其他-磁盘工具找到，添加到访达即可



#### 方法二 下载ntfs for mac的免费版

下载地址

http://ftp.paragon.eu.com/support/att/OEM/NTFS-15.8.109.dmg

完全免费和正版一样，据说只支持西部数据和希捷

方法来源：https://www.youtube.com/watch?v=vQu6LMk88_4

