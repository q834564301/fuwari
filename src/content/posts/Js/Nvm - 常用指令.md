---
title: Nvm - 常用指令
published: 2025-08-25
description: 使用 nvm 更好地管理 node 多开发环境
image: https://img.cdn1.vip/i/68ac18c9dfda7_1756109001.webp
tags: [Nvm]
category: Js
draft: false
---
# 常用命令

```shell
nvm off                                   // 禁用 node.js 版本管理 (不会卸载任何东西)
nvm on                                            // 启用 node.js 版本管理
nvm install 12.1.0                                // 安装指定版本的 node
nvm uninstall 12.1.0                              // 卸载指定版本的 node
nvm ls                                            // 显示所有已经安装的 node.js 版本
nvm ls available                                  // 显示可以安装的所有 node.js 版本
nvm use                                           // 切换到使用指定的 node.js 版本
nvm v                                             // 显示 nvm 版本
nvm install stable                                // 安装最新稳定版
nvm npm_mirror https://npm.taobao.org/mirrors/npm            // 设置 npm 下载镜像地址
nvm node_mirror https://npm.taobao.org/mirrors/node          // 设置 node 下载镜像地址
```
