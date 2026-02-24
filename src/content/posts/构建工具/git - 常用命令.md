---
title: 'git - 常用命令'
published: 2025-08-24
description: '工作中常用的 git 命令, 助你事半功倍'
image: 'https://img.cdn1.vip/i/68a9f27258d63_1755968114.webp'
tags: [Git,代码片段,教程,入门]
category: '构建工具'
draft: false
---
## commit 规范

可以创建一个 commit_msg.txt 文件, 然后使用 git commit -F commit_msg.txt  来规范格式

---

举例:

fix(login): 修复登录页加载失败的问题

因为 API 返回的数据结构变了,导致解析失败, 这里调整了逻辑, 详情如下:

- 1
- 2

---

| 类型     | 说明                              |
| -------- | --------------------------------- |
| feat     | 新功能                            |
| fix      | 修 bug                            |
| refactor | 重构, 不新增功能, 也不修 bug      |
| docs     | 改文档, 如 README                 |
| style    | 改代码风格, 不影响功能            |
| test     | 加测试, 改测试                    |
| chore    | 杂项, 比如改 .gitignore, 构建脚本 |
| perf     | 性能优化                          |
| ci       | CI/CD 相关改动                    |
| build    | 改构建系统或者依赖                |
| revert   | 回滚某个提交                      |

### 1. 配置 Git

#### 初始化 Git 配置

```bash
git config --global user.name "Your Name"  # 设置用户名
git config --global user.email "you@example.com"  # 设置邮箱
git config --global core.editor "vim"  # 设置默认编辑器
git config --global core.autocrlf input  # 处理换行符（Linux/Mac）
git config --global core.autocrlf true   # 处理换行符（Windows）
```

#### 查看配置

```bash
git config --list  # 查看所有配置信息
```

### 2. 基本操作

#### 初始化 Git 仓库

```bash
git init  # 初始化一个本地 Git 仓库
```

#### 克隆远程仓库

```bash
git clone <repository-url>  # 克隆远程仓库到本地
```

### 3. 分支操作

#### 查看分支

```bash
git branch          # 列出本地分支
git branch -r       # 列出远程分支
git branch -a       # 列出所有分支（本地 + 远程）
```

#### 创建分支

```bash
git branch <branch-name>  # 创建新分支
```

#### 切换分支

```bash
git checkout <branch-name>  # 切换到某个分支
git switch <branch-name>    # 新版切换分支命令
```

#### 创建并切换分支

```bash
git checkout -b <branch-name>  # 创建并切换到新分支
git switch -c <branch-name>    # 新版创建并切换
```

#### 删除分支

```bash
git branch -d <branch-name>   # 删除本地分支（已合并）
git branch -D <branch-name>   # 强制删除本地分支（未合并）
```

#### 推送本地分支到远程

```bash
git push origin <branch-name>
```

#### 删除远程分支

```bash
git push origin --delete <branch-name>
```

### 4. 提交代码

#### 添加文件到暂存区

```bash
git add <file-name>       # 添加单个文件
git add .                 # 添加当前目录的所有文件
git add *.txt             # 添加所有 .txt 文件
```

#### 查看当前状态

```bash
git status  # 查看工作区和暂存区的状态
```

#### 提交代码到本地仓库

```bash
git commit -m "commit message"  # 提交并附带提交信息
git commit                      # 启动编辑器进行提交
```

#### 修改最后一次提交

```bash
git commit --amend  # 修改上一次的提交信息或文件
```

### 5. 查看历史

#### 查看提交历史

```bash
git log                         # 查看完整提交历史
git log --oneline               # 简化输出（每个提交一行）
git log --graph --oneline       # 显示分支图
git log -p                      # 查看每次提交的代码改动
```

#### 查看某文件的修改历史

```bash
git log -- <file-name>  # 查看某个文件的历史
```

### 6. 回滚与撤销

#### 撤销文件修改

```bash
git checkout -- <file-name>  # 撤销工作区文件修改（本地未 add）
```

#### 撤销暂存区文件

```bash
git reset HEAD <file-name>  # 将暂存区文件撤回到工作区
```

#### 回滚到指定提交

```bash
git reset --soft <commit-id>  # 回滚到某提交，保留工作区文件和暂存区
git reset --mixed <commit-id> # 回滚到某提交，保留工作区文件，清空暂存区
git reset --hard <commit-id>  # 回滚到某提交，清空工作区和暂存区
```

### 7. 同步远程仓库

#### 查看远程仓库

```bash
git remote -v  # 查看远程仓库地址
```

#### 添加远程仓库

```bash
git remote add origin <repository-url>  # 绑定远程仓库
```

#### 拉取代码

```bash
git pull origin <branch-name>  # 拉取远程分支代码并合并到当前分支
```

#### 推送代码

```bash
git push origin <branch-name>  # 推送当前分支到远程仓库
```

### 8. 合并与冲突解决

#### 合并分支

```bash
git merge <branch-name>  # 将指定分支合并到当前分支
```

#### 解决冲突

1. 打开冲突文件，手动解决冲突。
2. 将解决冲突后的文件添加到暂存区：

   ```bash
   git add <file-name>
   ```
3. 提交合并：

   ```bash
   git commit
   ```

### 9. 标签操作

#### 创建标签

```bash
git tag <tag-name>                     # 创建轻量级标签
git tag -a <tag-name> -m "message"     # 创建带注释的标签
```

#### 查看标签

```bash
git tag            # 查看所有标签
```

#### 推送标签到远程

```bash
git push origin <tag-name>      # 推送指定标签
git push origin --tags          # 推送所有标签
```

#### 删除标签

```bash
git tag -d <tag-name>            # 删除本地标签
git push origin --delete <tag-name>  # 删除远程标签
```

### 10. Stash（存储现场）

#### 保存当前工作现场

```bash
git stash           # 保存未提交的修改
git stash save "message"  # 保存并附加描述
```

#### 查看所有存储的现场

```bash
git stash list
```

#### 恢复工作现场

```bash
git stash apply          # 应用最近一次存储的现场
git stash pop             # 应用最近一次存储的现场并且将此次 stash 从 stash list 中 删除
git stash apply stash@{n}  # 应用指定的现场
```

#### 删除存储的现场

```bash
git stash drop stash@{n}  # 删除指定的存储
git stash clear           # 清空所有存储
```

### 11. 高级操作

#### 比较差异

```bash
git diff                   # 查看工作区和暂存区的差异
git diff --cached          # 查看暂存区和上一次提交的差异
git diff <branch-name>     # 比较当前分支和指定分支的差异
git diff <commit-id1> <commit-id2>  # 比较两次提交的差异
```

#### Rebasing（变基）

```bash
git rebase <branch-name>   # 将当前分支的提交变基到指定分支
```

#### Cherry-pick（挑拣提交）

```bash
git cherry-pick <commit-id>  # 应用某次提交到当前分支
```

### 12. 清理操作

#### 删除未追踪的文件

```bash
git clean -f              # 删除未追踪的文件
git clean -fd             # 删除未追踪的文件和文件夹
```

#### 清理缓存

```bash
git rm --cached <file-name>  # 从暂存区删除文件但保留在工作区
```

### 13. 常见问题解决

#### 忽略某些文件

创建 `.gitignore` 文件并写入需要忽略的文件或 ：

```bash
*.log
*.pyc
node_modules/
plaintext123
```

#### 修改远程仓库地址

```bash
git remote set-url origin <new-url>
```
