

---
author: longlikun
title : wsl 设置主机网络互通
date : 2024-03-13T15:21:01+08:00
description: wsl 检测到localhost代理配置，但未镜像到wsl，nat模式下的wsl不支持localhost代理 怎么处理
draft: false
categories:
    - test


tags :
   - WSL
   - HUGO

---

## 解决办法


在 %userprofile%\.wslconfig 中，
假如您的用户名是 user123，则 .wslconfig 文件的路径为：`C:\Users\user123\.wslconfig`,写入以下内容然后保存：

```shell
[experimental]
autoMemoryReclaim=gradual # 可以在 gradual 、dropcache 、disabled 之间选择
networkingMode=mirrored
dnsTunneling=true
firewall=true
autoProxy=true
sparseVhd=true
sparseVhd=true
```

上面的各个参数的作用:
#### autoMemoryReclaim

> gradual：渐进式内存回收。WSL 会在需要时自动回收内存，但不会立即释放所有未使用内存。
> dropcache：立即释放所有未使用内存。这可能会导致性能下降，但可以确保释放所有可用的内存。
> disabled：禁用自动内存回收。这可能会导致内存泄漏，但可以提供最佳性能。

#### networkingMode

>mirrored：使用与 Windows 相同的网络设置。
>isolated：为 WSL 分配独立的网络连接。
#### dnsTunneling

>true：将所有 DNS 请求路由到 Windows DNS 解析器。
false：允许 WSL 使用自己的 DNS 解析器。
#### firewall

>true：启用 Windows Defender 防火墙。
false：禁用 Windows Defender 防火墙。
#### autoProxy

>true：自动检测和使用 Windows 代理设置。
false：不使用 Windows 代理设置。
#### sparseVhd

>true：使用稀疏虚拟硬盘 (VHD)。这可以节省磁盘空间，但可能会导致性能下降。
false：使用固定大小的 VHD。这可以提供最佳性能，但需要更多磁盘空间。

配置完成后运行 wsl --shutdown ，关闭wsl。
然后再运行 wsl --manage 发行版名字 --set-sparse true 启用稀疏虚拟硬盘 (VHD), 允许 WSL2 的硬盘空间自动回收，比如 `wsl --manage ubuntu20.04 --set-sparse true`,ubuntu20.04 名字可能不同，先通过 `wsl --list`查询版本。

然后你会发现，提示没有了，WSL2 和 Windows 主机的网络互通而且 IP 地址相同了，还支持 IPv6 了，并且从外部（比如局域网）可以同时访问 WSL2 和 Windows 的网络。这波升级彻底带回以前 WSL1 那时候的无缝网络体验了，并且 Windows 防火墙也能过滤 WSL 里的包了，再也不需要什么桥接网卡、端口转发之类的操作了。并且 WSL2 的内存占用和硬盘空间都可以自动回收了！

参考：
github https://github.com/microsoft/WSL/issues/10753
wsl官方文档 https://learn.microsoft.com/zh-cn/windows/wsl/wsl-config
