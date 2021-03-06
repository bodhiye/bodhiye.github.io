---
title: "同步 Linux 时间"
date: 2021-03-16T22:53:14+08:00
categories: ["Linux 运维"]
tags: ["Linux"]
---

### 前言

　　最近在工作中碰到这么一个问题：我们某台内网服务器的本地时间和 UTC 时间相差了一个多小时，由于该服务器没有联网，所以不能同步网络时间，但是我们部署在其上的某个服务通过时间戳来校验签名，签名算法设置的请求时间戳和当前时间不超过 30s，所以只能离线校准该服务器的本地时间。

### 同步 Linux 时间

#### 修改当前时区

　　将本地时区设置为上海，`timedatectl set-timezone Asia/Shanghai`。

#### 修改机器硬件时间

　　把机器硬件时间校准为当前时间，`hwclock --set --date="03/16/2021 22:00:00"`。

#### 同步系统时间

　　将机器时间同步到系统时间，`hwclock --hctosys`。
　　相反的，如果要把系统时间同步到机器时间，`hwclock --systohc`。

#### 系统定时同步系统时间

　　通过测试下来发现每隔一段时间后系统还是会比 UTC 时间慢，这里我们就需要在系统设置定时任务来校准时间。通过 crontab 命令我们能够定时启动系统指令或者 shell 脚本，我们通过在 `/etc/crontab` 文件最后加上 `*/10 * * * * root hwclock --hctosys` 来实现每隔十分钟同步系统时间。

#### 拓展一下

　　hwclock是Linux系统中用于修改系统时间和硬件时间的命令工具。硬件时间是指主板BIOS设置的时间，系统时间是指操作系统内核中的时间。默认情况下，操作系统启动时，会自动从硬件中读取操作系统的时间。

　　hwclock可以读取硬件时间，hwclock可以把系统时间同步到硬件，也可以把硬件时间同步到操作系统。
