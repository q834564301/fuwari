---
title: vmware 下 debian - 硬盘扩容 
published: 2025-09-08
description: 记录 vm 虚拟机下 debian 13 的扩容操作
image: 
tags: [debian, vmware]
category: linux
draft: false
---
### 背景

空间不够了, 故扩容

### 步骤

#### 1. 虚拟机扩容

![](https://img.cdn1.vip/i/68bedf15736c7_1757339413.webp)

#### 2. debian 13 扩容

1. 下载 parted
   1. 下不下来的话可以使用临时代理下载: sudo http_proxy="http://127.0.0.1:20171" apt install parted
2. 运行 (quit 是退出)
   1. parted
   2. print free 打印所有空间
   3. rm 2 (这个2是扩展空间的序号,要注意有没有显示扩展类型, 如果删除不掉的话, 看看是不是开了虚拟内存, 需要关闭虚拟内存后重试)
      1. 关闭虚拟内存代码: swapoff /dev/sda5 (虚拟内存目标盘, 功能: 禁用交换分区)
   4. resizepart 1 100% (扩展主分区)
   5. quit (退出 parted)
   6. sudo resize2fs /dev/sda1 (调整系统文件大小)
   7. 完成!! 可以使用 df -h 查看了
