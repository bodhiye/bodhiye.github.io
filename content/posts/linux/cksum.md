---
title: "Linux cksum命令"
date: 2020-07-29T23:25:47+08:00
draft: false
categories: ["每日Linux命令"]
tags: ["Linux"]
---

---

### 前言

最近女朋友要我把相机里旅游时拍的照片发给她，然后我就把照片传到百度云发给她了，她下载后就抱怨说百度云把图片压缩了，导致图片放大后看不清，我马上上百度云看了一下，发现文件大小没有压缩，于是我就把百度云下载的图片和我本地内存卡里的照片比对一下，看百度云是否把我的图片压缩了。这里就可以用到 cksum 命令来检查两个文件是否一致。

### 命令详解

Linux cksum 命令用于检查文件的 CRC（Cyclic Redundancy Check 循环冗余检验码）是否正确，确保文件从一个系统传输到另一个系统的过程中不被损坏。

CRC 是一种排错检查方式，该校验法的标准由 CCITT 所指定，至少可检测到 99.998% 的已知错误。

指定文件交由指令"cksum"进行校验后，该指令会返回校验结果供用户核对文件是否正确无误。若不指定任何文件名称或是所给予的文件名为"-"，则指令"cksum"会从标准输入设备中读取数据。

### 命令全拼

cksum = checksums

### 语法格式

> cksum [--help][--version][文件...]

### 参数说明

- --help：在线帮助。
- --version：显示版本信息。
- 文件…:需要进行检查的文件路径

### 举个栗子

使用指令"cksum"计算文件 yeqiongzhou.jpg 和 yeqiongzhou-baiduyun.jpg 的一致性，输入如下命令：

> cksum yeqiongzhou.jpg yeqiongzhou-baiduyun.jpg

以上命令执行后，将输出校验码等相关的信息，具体输出信息如下所示：

> 2415123943 3538944 yeqiongzhou.jpg  
> 2415123943 3538944 yeqiongzhou-baiduyun.jpg

上面的输出信息中，`2415123943`表示校验码，`3538944`表示字节数。
可见这两张图片是一模一样的，百度云并没有对照片进行压缩。

### Tips

如果文件中有任何字符被修改，都将改变计算后 CRC 校验码的值。
