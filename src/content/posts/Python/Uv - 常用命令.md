---
title: uv - 常用命令
published: 2025-08-29
description: 使用 uv 快速实现虚拟化 python 开发环境
image: https://img.cdn1.vip/i/68b178c6246a4_1756461254.webp
tags: [Uv]
category: Python
draft: false
---
## 安装 uv

```python
pip install uv
```

## 查看 uv 版本

```python
uv --version
```

## 清除 uv 缓存文件

```python
uv clean
```

## uv 安装 pip

```python
uv pip install pip --upgrade
```

## pip 包通过 uv 加速安装和升级

**==注意: 一般情况下建议使用 uv add 安装包, 如果和 pip 混用, 怕包依赖出现问题, 同时混用也不方便管理==**

```python
uv pip install --upgrade pip setuptools wheel
```

## 创建 python 新项目并初始化 uv 环境

```python
uv init project_name
```

## 现有 python 项目文件夹中创建

```python
cd project_name
uv init
```

## 初始化 uv 环境, 指定 python 版本

```python
# uv venv 虚拟环境名称 --python 版本
uv venv venv --python 3.9
```

## python 虚拟环境创建后，修改python版本

```python
uv python list
uv python install 3.9
```

## 快速启动他人 uv 项目

**==注意: 例如别人用 uv 创建的项目, 使用 uv sync 会直接读取 当前项目下的 uv 配置, 生成对应的开发环境==**

```python
uv sync
```

## uv 批量下载依赖

```python
uv add -r requirements.txt
```

## uv 常见指令

```python
uv remove  # 移除依赖
uv sync  # 同步依赖到虚拟环境中
uv lock  # 生成锁文件
uv run  # 虚拟环境中运行脚本
uv tree  # 查看依赖列表
uv build  # 生成发布包
uv publish  # 发布到PyPI
uv pip list  # 查看安装的库
```

```python
uv add package  # package为需安装的包名称
uv remove package 
uv tree  # 树形结构显示已安装的包以及包依赖
uv pip list  # 会显示由uv管理和不由uv管理的所有安装包比如使用uv pip install安装的包
uv lock --upgrade-package loguru  # 更新包
```

## 其他命令

```python
uv add --group dev pandas  # 安装到开发环境
uv add --group production requests  # 安装到生产环境
uv add "numpy>=2.0"   # 版本条件
```
