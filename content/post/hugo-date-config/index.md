---
author: longlikun
title: hugo设置文章发表时间格式
date: 2024-03-27T23:34:49+08:00
description: hugo 设置文章发表时间格式
draft: false

categories:
    - 教程
    - 随笔

---

## hugo 设置文章发表时间的格式

修改config.yaml 文件 published字段

```yaml
  dateFormat:
    published: 2006年1月2日
    lastUpdated: Jan 02, 2006 15:04 MST
```

**注意:具体时间`2006年1月2日`可能会影响转换结果**