---
author: longlikun
title : 如何使用 Powershell 和 Oh My Posh 设置 Windows 终端
date : 2024-03-18T18:02:11+08:00
description: 怎么在wsl中使用hugo
draft: false
math: true
categories:
    - Test
    - 随笔

tags :
   - github

---

## 必要条件

### 1.安装window 终端

要安装windows终端，需要在 Windows 10 或 11以上。最简单的方法是使用windows store，方法很简单，直接进入微软商店搜索 Windows 终端并安装该选项即可。
https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701。
你还可以使用winget，Chocolatey ，Scoop等工具来安装，可以参考github 仓库 https://github.com/microsoft/terminal.

### 2.安装Oh My Posh

可以通过 Winget、scoop 或使用 PowerShell 命令手动安装 Oh My Posh
https://ohmyposh.dev/docs/installation/windows
这里我使用winget 安装
```bash
winget install JanDeDobbeleer.OhMyPosh -s winget
```

为了重新加载 PATH，建议重新启动终端。如果 oh-my-posh 未被识别为命令，可以重新运行安装程序，或手动将其添加到 PATH。命令

```bash
$env:Path += ";C:\Users\user\AppData\Local\Programs\oh-my-posh\bin"
```
### 3.安装字体

Oh My Posh 被设计为使用Nerd 字体。Nerd 字体是流行的字体，经过修补以包含图标。推荐Meslo LGM NF，但任何 Nerd 字体都应该与标准主题兼容。你可以直接到https://www.nerdfonts.com/下载安装，或者使用，使用管理员身份运行，选择安装
```bash
oh-my-posh font install
```


### 4. 安装图标
要想在终端中看到漂亮的图标，还应该安装一个icon库，devblackops/Terminal-Icons，github地址https://github.com/devblackops/Terminal-Icons
安装方法:
```bash
Install-Module -Name Terminal-Icons -Repository PSGallery
```
使用方法:在你的Microsoft.PowerShell_profile.ps1文件中添加,
```bash
Import-Module -Name Terminal-Icons
```
Microsoft.PowerShell_profile.ps1 文件一般位于C:\Users\YOUR_USER_NAME\OneDrive\Documentos\PowerShell，可以输入  `$profile` 查看


### 5. 设置模板
Oh My Posh 有很多模板可以选择https://ohmyposh.dev/docs/themes，你可以从中选择你喜欢的，设置方法，在 C:\Users\YOUR_USER_NAME\OneDrive\Documentos\PowerShell\Microsoft.PowerShell_profile.ps1 文件中添加
```bash
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\material.omp.json" | Invoke-Expression
```

 最终的文件设置是这样的
 ```bash
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\half-life.omp.json" | Invoke-Expression

Import-Module -Name Terminal-Icons
```
