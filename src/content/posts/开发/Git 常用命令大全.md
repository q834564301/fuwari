---
title: 'Git 常用命令大全'
published: 2025-08-24
description: '工作中常用的Git命令, 助你事半功倍'
image: 'https://img.cdn1.vip/i/68a9ec0a0b669_1755966474.webp'
tags: [Git]
category: '开发'
draft: false
---
#### 一、仓库初始化与克隆

##### 初始化本地仓库

```csharp
git init                          # 在当前目录创建一个空的 Git 仓库

git init [project-name]           # 创建新目录并初始化为 Git 仓库
```

##### 克隆远程仓库

```php
git clone [url]                   # 下载远程仓库到本地新目录（包含完整提交历史）
```

#### 二、基础配置

##### 查看与编辑配置

```lua
git config --list                 # 显示当前所有 Git 配置

git config -e [--global]          # 编辑全局（--global）或本地配置文件
```

##### 设置用户信息（提交时使用）

```csharp
git config [--global] user.name "[姓名]"  # 设置用户名（--global 为全局配置，不加则为当前仓库）

git config [--global] user.email "[邮箱]" # 设置邮箱
```

#### 三、文件操作（工作流核心）

##### 状态与差异查看

```csharp
git status                        # 查看工作区和暂存区状态（哪些文件未跟踪、已修改、已暂存）

git diff                          # 显示工作区与暂存区的差异

git diff --cached                 # 显示暂存区与最后一次提交的差异

git diff HEAD                     # 显示工作区与最新提交的差异
```

##### 暂存与提交

```cobol
git add [file1] [file2]           # 添加指定文件到暂存区

git add .                         # 添加当前目录所有文件到暂存区

git add -p                        # 交互式暂存（逐块选择修改内容）

 

git commit -m "提交信息"          # 提交暂存区内容到本地仓库（必加 -m 说明提交目的）

git commit -a -m "提交信息"       # 直接提交工作区所有已跟踪文件的变更（跳过 add）

git commit --amend -m "新信息"    # 修改最后一次提交（包括信息或内容）
```

##### 文件管理

```bash
git rm [file1] [file2]            # 删除工作区文件并加入暂存区（同步删除版本控制）

git rm --cached [file]            # 停止跟踪文件但保留在工作区

git mv [原路径] [新路径]           # 重命名/移动文件并记录变更
```

#### 四、分支管理

##### 分支列表

```csharp
git branch                        # 列出本地分支（当前分支标星号）

git branch -r                     # 列出远程分支

git branch -a                     # 列出所有本地和远程分支
```

##### 创建与切换分支

```csharp
git branch [分支名]               # 新建分支（不切换）

git checkout -b [分支名]          # 新建并切换到新分支（等价于 git switch -c [分支名]）

git checkout [分支名]             # 切换到已有分支（更新工作区）

git checkout -                    # 切换回上一次所在分支
```

##### 合并与变基

```csharp
git merge [分支名]                # 合并指定分支到当前分支（Fast-forward 或创建合并提交）

git rebase [分支名]               # 将当前分支变基到目标分支（整理提交历史，使历史线性化）
```

##### 删除分支

```perl
git branch -d [分支名]            # 删除本地分支（需先切换到其他分支，未合并会报错）

git branch -D [分支名]            # 强制删除未合并的本地分支

git push origin --delete [分支名]  # 删除远程分支（或 git push origin :[分支名]）
```

#### 五、远程仓库交互

##### 远程仓库管理

```csharp
git remote -v                     # 查看所有远程仓库（名称和 URL）

git remote add [名称] [URL]       # 添加远程仓库（如 origin）

git remote rm [名称]              # 删除远程仓库

git remote set-url [名称] [新URL]  # 修改远程仓库 URL
```

##### 拉取与推送

```perl
git fetch [远程名]                # 从远程仓库获取最新数据（不合并到本地）

git pull [远程名] [分支名]         # 拉取并合并远程分支到本地（等价于 fetch + merge）

git pull --rebase [远程名] [分支]  # 拉取并通过变基合并（保持线性提交历史）

 

git push [远程名] [本地分支]:[远程分支]  # 推送本地分支到远程（远程分支名可省略，默认同名）

git push origin --all             # 推送所有本地分支到远程

git push --tags                   # 推送所有标签到远程

git push --force                  # 强制推送（覆盖远程，慎用！）
```

#### 六、撤销与重置

##### 撤销修改

```perl
git checkout -- [文件]            # 丢弃工作区修改，恢复到最后一次提交的状态

git reset [文件]                  # 从暂存区移除文件（工作区不变）

git reset --hard [提交ID]         # 重置 HEAD、暂存区和工作区到指定提交（彻底回退，丢失未提交修改）
```

##### 撤销提交

```csharp
git revert [提交ID]               # 创建新提交撤销指定提交的变更（推荐用于公共分支）
```

##### 暂存工作进度

```perl
git stash                         # 暂存当前工作区修改（保存到栈）

git stash pop                     # 恢复最近暂存的修改并删除栈中记录

git stash apply                   # 恢复暂存的修改但保留记录

git stash list                    # 查看所有暂存记录
```

#### 七、历史与日志查看

```perl
git log                           # 显示当前分支的提交历史（详细信息）

git log --oneline                 # 简洁模式，一行显示一个提交

git log -p [文件]                 # 显示指定文件的每次提交差异

git log --stat                    # 显示每次提交的文件变更统计（增/删行数）

git show [提交ID]                 # 显示某次提交的详细内容（代码变更+元数据）

git blame [文件]                  # 显示文件每行的最后修改者和提交信息

git reflog                        # 显示 HEAD 的所有历史操作（包括撤销的提交）
```

#### 八、标签管理（版本标记）

##### 创建标签

```csharp
git tag [标签名]                  # 在当前提交创建轻量标签（默认）

git tag -a [标签名] -m "说明"     # 创建带说明的附注标签
```

##### 标签操作

```ruby
git tag                           # 列出所有本地标签

git show [标签名]                 # 查看标签详细信息

git push origin [标签名]          # 推送单个标签到远程

git push origin --tags            # 推送所有标签到远程

git tag -d [标签名]               # 删除本地标签

git push origin :refs/tags/[标签名] # 删除远程标签
```

#### 九、高级功能

##### 补丁与归档

```perl
git format-patch [提交范围]       # 生成补丁文件（.patch）

git apply [补丁文件]              # 应用补丁到工作区

git archive -o [文件名].tar HEAD  # 生成当前 HEAD 版本的代码归档（tar包）
```

##### 二分查找（定位问题提交）

```perl
git bisect start                  # 启动二分查找

git bisect good [提交ID]          # 标记正常提交

git bisect bad [提交ID]           # 标记有问题的提交

git bisect reset                  # 结束查找并重置到原始状态
```

##### 子模块与大文件

```csharp
git submodule add [URL] [路径]    # 添加子模块

git submodule update              # 更新子模块到最新版本

git lfs install                   # 安装 Git LFS（管理大文件）

git lfs track [文件模式]          # 追踪大文件（通过 LFS 存储）
```

##### 工作树与清理

```csharp
git worktree add [路径] [分支]    # 添加多个工作树（同时开发多个分支）

git clean -n                      # 预览将删除的未跟踪文件

git clean -f                      # 强制删除未跟踪文件

git clean -df                     # 删除未跟踪文件和目录
```

#### 十、常用快捷键与技巧

```csharp
git switch [分支名]：替代 git checkout [分支名]（切换分支，更语义化）

git restore [文件]：替代 git checkout -- [文件]（恢复文件，更清晰）

git merge --squash [分支]：合并时压缩多个提交为一个

git rebase -i [提交ID]：交互式变基（编辑、合并、删除提交）
```

#### 十一、跨仓库与离线操作

##### 1\. Git Bundle（打包仓库）

```php
git bundle create repo.bundle HEAD   # 打包当前分支及依赖的提交到 repo.bundle（离线传输用）

git bundle verify repo.bundle        # 验证捆绑包完整性

git clone repo.bundle [分支名]       # 从捆绑包克隆仓库（无网络时使用）
```

**场景** ：在没有网络的环境中分享代码，或备份仓库历史。

##### 2\. 子模块进阶

```csharp
git submodule init                    # 初始化子模块（仅首次克隆后执行）

git submodule sync                    # 同步子模块的远程 URL（更新配置）

git submodule foreach "git pull"      # 对所有子模块执行 git pull（批量更新）
```

**注意** ：子模块默认指向特定提交，更新时需显式切换分支或提交。

#### 十二、钩子（Hooks）：自动化工作流

Git 钩子位于 `.git/hooks/` 目录（需手动复制示例文件并去除 `.sample` 后缀），常用钩子：

##### 1\. 提交前检查（代码规范、测试）

```cobol
# pre-commit（本地钩子，提交前运行）

#!/bin/sh

npm run lint || exit 1  # 代码检查不通过则阻止提交
```

##### 2\. 合并后操作（更新子模块）

```sql
# post-merge（本地钩子，合并后运行）

git submodule update --init --recursive
```

##### 3\. 服务器端钩子（如 pre-receive 阻止非法提交）

```bash
# 远程仓库管理员配置（阻止向主分支直接提交）

#!/bin/sh

while read oldrev newrev refname; do

  if [ "$refname" = "refs/heads/main" ]; then

    echo "禁止直接提交到 main 分支，请通过 PR 合并"

    exit 1

  fi

done
```

#### 十三、环境与性能优化

##### 1\. 全局配置优化

```csharp
git config --global core.editor "code --wait"  # 设置默认编辑器为 VS Code（等待关闭后继续）

git config --global merge.tool meld             # 设置图形化合并工具（如 meld、kdiff3）

git config --global credential.helper store     # 记住 HTTPS 密码（避免每次输入）
```

##### 2\. 仓库瘦身与性能

```csharp
git gc --aggressive --prune=now  # 强制清理无效对象，压缩历史（用于大型仓库）

git prune --expire=now           # 删除过期的引用（配合 gc 使用）

git count-objects -v             # 查看仓库对象数量（排查膨胀原因）
```

##### 3\. 稀疏检出（Sparse Checkout）：仅下载部分文件

```bash
git init myrepo

cd myrepo

git remote add origin [url]

git config core.sparsecheckout true

echo "src/" >> .git/info/sparse-checkout  # 仅检出 src 目录

git pull origin main                      # 拉取时仅下载 src 相关文件
```

**场景** ：大型仓库中只需要部分代码（如前端项目无需后端代码）。

#### 十四、安全与签名

##### 1\. GPG 签名提交 / 标签

```sql
# 生成 GPG 密钥并配置到 Git

gpg --generate-key

git config --global user.signingkey [密钥ID]

 

# 提交时签名（-S 或 --gpg-sign）

git commit -S -m "签名提交"

 

# 验证标签/提交签名

git verify-commit [提交ID/标签名]
```

##### 2\. 禁止推送至特定分支（本地保护）

```csharp
git update-ref -d refs/heads/main  # 本地删除 main 分支（防止误推）

# 需通过 git checkout -b main 重新创建后才能推送
```

#### 十五、交互式操作与高级技巧

##### 1\. 交互式变基（整理提交历史）

```csharp
git rebase -i HEAD~3  # 对最近 3 个提交进行交互式编辑

# 进入编辑器后，可将操作改为 pick（保留）、reword（修改信息）、squash（合并）等
```

##### 2\. 部分暂存（选择代码块添加到暂存区）

```csharp
git add -p  # 逐行或逐块选择要暂存的修改

# 按 s 分割块，按 y 暂存，按 n 跳过
```

##### 3\. 解决合并冲突

```cobol
git merge feature-branch  # 合并时冲突，进入冲突状态

vi 冲突文件                # 手动编辑冲突（<<<<< ===== >>>>> 标记处）

git add 冲突文件            # 标记冲突已解决

git commit                  # 生成合并提交
```

**工具辅助** ： `git mergetool` 调用图形化工具（如 VS Code 内置合并编辑器）。

#### 十六、冷门但实用的命令

##### 1\. 查找文件历史（含重命名）

```csharp
git log --follow [文件名]    # 跟踪文件重命名后的所有提交历史

git whatchanged [文件名]      # 等价于 git log --follow --diff [文件]
```

##### 2\. 统计代码贡献

```swift
git shortlog -sn            # 按提交次数统计所有作者

git log --author="张三" --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "Added lines: %s, Removed lines: %s, Total lines: %s\n", add, subs, loc }'
```

##### 3\. 比较分支差异

```csharp
git diff main...feature     # 比较 main 分支与 feature 分支的差异（不包含共同祖先）

git diff main feature       # 比较两个分支的所有差异（包含共同祖先）
```

##### 4\. 恢复误删的分支 / 提交

```perl
git reflog  # 找到误删分支的 HEAD 历史记录（如 HEAD@{3}）

git branch 恢复的分支名 HEAD@{3}  # 从记录重建分支
```

#### 十七、Git 新特性（Git 2.23+）

##### 1\. git switch 替代 git checkout（分支切换）

```csharp
git switch -c new-branch  # 新建并切换分支（等价于 git checkout -b）

git switch existing-branch  # 切换到已有分支（更语义化）
```

##### 2\. git restore 替代部分 git checkout（文件恢复）

```csharp
git restore --staged [文件]  # 从暂存区移除文件（等价于 git reset [文件]）

git restore [文件]           # 丢弃工作区修改，恢复到上次提交（等价于 git checkout -- [文件]）
```

##### 3\. 工作树管理（多分支同时开发）

```bash
git worktree add ../project-feature main  # 在同级目录创建新工作树，基于 main 分支

cd ../project-feature

git switch -c feature-branch  # 独立开发，不影响原工作目录
```

#### 十八、常见问题解决方案

| 问题场景                   | 解决方案命令                                                                     |
| -------------------------- | -------------------------------------------------------------------------------- |
| 远程分支已删除，本地仍显示 | `git remote prune origin` （清理无效的远程分支引用）                           |
| 提交后发现漏加文件         | `git add 漏加文件 && git commit --amend --no-edit` （追加到上一次提交）        |
| 强制覆盖本地未提交修改     | `git fetch --all && git reset --hard origin/main` （慎用，丢失本地未提交内容） |
| 子模块未更新导致构建失败   | `git submodule update --init --recursive` （克隆时添加 `--recursive` 参数）  |

#### 十九、提交历史的深度控制

##### 1\. 选择性合并提交（cherry-pick）

```cobol
git cherry-pick [commit1] [commit2]    # 从其他分支选择特定提交应用到当前分支

git cherry-pick -n [commit]            # 应用提交但不自动创建提交（用于合并多个提交）
```

**场景** ：仅需要某个分支的部分功能，而非整个分支。

##### 2\. 修改历史提交信息（多个提交）

```csharp
git rebase -i HEAD~3                   # 修改最近3个提交的信息

# 将需要修改的提交前的pick改为reword，保存退出后逐个修改提交信息
```

##### 3\. 压缩多个提交为一个

```csharp
git rebase -i HEAD~5                   # 将最近5个提交压缩为一个

# 将需要压缩的提交前的pick改为squash或fixup（fixup会丢弃提交信息）
```

#### 二十、代码审查与协作

##### 1\. 生成补丁文件（用于邮件或离线审查）

bash

```perl
git format-patch -3                   # 生成最近3个提交的补丁文件（.patch）

git send-email --to dev@example.com 0001*.patch  # 通过邮件发送补丁
```

**接收方** ： `git am 0001.patch` 应用补丁。

##### 2\. 查看某功能的所有提交

```perl
git log --grep="feature: add login" --oneline  # 搜索包含特定关键词的提交
```

##### 3\. 临时切换分支（保留未提交修改）

```perl
git stash push -m "work in progress"  # 暂存当前修改并添加描述

git checkout other-branch             # 切换到其他分支

# 处理完后返回原分支：

git checkout original-branch

git stash pop                         # 恢复暂存的修改
```

#### 二十一、大型仓库优化

##### 1\. 浅克隆（仅下载最新提交）

```php
git clone --depth=1 [url]             # 只克隆最新一次提交（节省空间和时间）

git fetch --unshallow                 # 后续需要完整历史时，下载全部提交
```

##### 2\. 过滤克隆（只下载指定路径）

```bash
git clone --filter=blob:none --sparse [url]  # 初始化空仓库

cd repo

git sparse-checkout init --cone       # 配置稀疏检出

git sparse-checkout set src/ docs/    # 只下载src和docs目录

git pull origin main                  # 拉取指定路径的内容
```

##### 3\. 清理大文件历史（已提交的大文件）

```cobol
# 使用BFG Repo-Cleaner（比git filter-branch更快）

java -jar bfg.jar --strip-blobs-bigger-than 100M repo.git

git reflog expire --expire=now --all && git gc --prune=now --aggressive
```

#### 二十二、多仓库同步与镜像

##### 1\. 镜像克隆（用于备份）

```bash
git clone --mirror [url]              # 创建仓库的完整镜像（含所有引用和配置）

# 定期更新镜像：

cd repo.git

git remote update
```

##### 2\. 推送到多个远程仓库

```perl
git remote add backup [backup-url]    # 添加第二个远程仓库

git push origin main && git push backup main  # 同时推送到两个仓库
```

##### 3\. 同步两个远程仓库（无本地工作区）

```csharp
git clone --bare [source-url]         # 克隆为裸仓库

cd repo.git

git remote add target [target-url]

git push target --all                 # 推送所有分支到目标仓库
```

#### 二十三、疑难问题诊断

##### 1\. 查找引入 bug 的提交

```perl
git bisect start                      # 开始二分查找

git bisect bad                        # 标记当前提交有问题

git bisect good v1.0                  # 标记已知正常的版本

# Git会自动切换到中间提交，测试后：

git bisect good                       # 如果当前提交正常

git bisect bad                        # 如果当前提交有问题

# 重复直到找到第一个有问题的提交

git bisect reset                      # 结束查找
```

##### 2\. 检查文件权限变更

```bash
git diff --word-diff=porcelain --stat  # 显示文件权限变更

git config core.fileMode false         # 忽略文件权限变更（仅限Linux/Mac）
```

##### 3\. 修复损坏的仓库

```csharp
git fsck --full                       # 检查仓库完整性

git reflog expire --expire=now --all  # 删除过期引用

git gc --prune=now                    # 清理无效对象
```

#### 二十四、Git 别名与自定义命令

##### 1\. 设置常用命令别名

```perl
git config --global alias.co checkout  # git co 替代 git checkout

git config --global alias.st status    # git st 替代 git status

git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"  # 美化日志输出
```

##### 2\. 创建自定义 Git 命令（shell 脚本）

```bash
#!/bin/sh

# ~/bin/git-undo（需添加到PATH）

git reset --hard HEAD~1

 

# 使用：

git undo                            # 回退上一个提交
```

#### 二十五、Git 工作流最佳实践

##### 1\. GitFlow 工作流

```perl
# 初始化

git flow init                       # 设置主分支和开发分支

 

# 开发新功能

git flow feature start my-feature   # 创建功能分支

git flow feature publish my-feature # 推送到远程

git flow feature finish my-feature  # 完成功能并合并到develop

 

# 发布版本

git flow release start v1.0.0       # 创建发布分支

git flow release finish v1.0.0      # 完成发布并合并到master和develop
```

##### 2\. GitHub Flow（简化工作流）

1. 创建分支： `git checkout -b feature/my-feature`
2. 提交代码并推送： `git push origin feature/my-feature`
3. 创建 Pull Request，通过 CI/CD 测试
4. 批准后合并到 main，删除分支

#### 二十六、Git 安全与合规

##### 1\. 清除敏感信息

```python
# 使用filter-branch（注意：修改历史会影响所有协作者）

git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch path/to/secret.file' --prune-empty --tag-name-filter cat -- --all

 

# 推送强制更新（警告：会覆盖远程历史）

git push origin --force --all
```
