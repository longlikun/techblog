---


author: longlikun
title : hugo 设置日期格式
date : 2024-03-27T22:44:31+08:00
description: hugo 设置日期不准确
draft: false
categories:
    - 教程
    
tags :
   - hugo

---

### hugo 怎么设置日期格式

修改published 格式, 

正确格式:

```shell

  dateFormat:
    published: 2006年1月2日 15:04 
    lastUpdated: Jan 02, 2006 15:04 MST

```

>**注意:`2006年1月2日` 这里的具体时间会影响时间格式,例如`2006年6月2日` 都会导致时间不准确。**

