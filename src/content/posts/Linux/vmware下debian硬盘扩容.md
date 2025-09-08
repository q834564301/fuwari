---
title: vmware 下 debian - 硬盘扩容
published: 2025-09-08
description: 记录 vm 虚拟机下 debian 13 的扩容操作
image: https://img.cdn1.vip/i/68beeec6a1345_1757343430.webp
tags: [debian, vmware]
category: 编程开发
draft: false
---
### 背景

空间不够了, 故扩容

### 步骤

#### 1. 虚拟机扩容

![](https://img.cdn1.vip/i/68bedf15736c7_1757339413.webp)

#### 2. debian 扩容

1. 下载 parted
   1. 下不下来的话可以使用临时代理下载: sudo http_proxy="http://127.0.0.1:20171" apt install parted
2. 运行 (quit 是退出)
   1. parted
   2. print free 打印所有空间
   3. rm 2 (这个2是扩展空间的序号,要注意有没有显示扩展类型, 如果删除不掉的话, 看看是不是开了虚拟内存, 需要关闭虚拟内存后重试)
      1. 关闭虚拟内存代码: swapoff /dev/sda5 (虚拟内存目标盘, 功能: 禁用交换分区)
      2. sudo vim /etc/fstab (进入后删除 swap 那两行 一般是 uuid)
      3. sudo vim /etc/initramfs-tools/conf.d/resume (删除 swap 相关, 一般只有一行 uuid)
      4. sudo update-initramfs-u (更新 initramfs（初始内存文件系统）归档文件)
   4. resizepart 1 100% (扩展主分区)
   5. quit (退出 parted)
   6. sudo resize2fs /dev/sda1 (调整系统文件大小)
   7. 完成!! 可以使用 df -h 查看了

#### 疑难杂症

问题描述：开机时提示“piix4_smbus 0000:00:07.3: SMBus Host controller not enabled”
出现原因：系统装入i2c_piix4模块所致，因为系统找不到这个模块，所以报错


解决办法：

1. 查明装入模块的确切名字。命令：lsmod | grep i2c (查询结果为：i2c_piix4 模块)
2. 将该模块列入不装入名单。编辑文件命令：sudo vi  /etc/modprobe.d/blacklist.conf，在文件最后一行加：blacklist i2c_piix4，保存退出
3. 重新生成引导文件。命令：sudo update-initramfs -u -k all
4. 重启系统。命令：reboot
