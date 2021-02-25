# Git学习 

* https://gitee.com/all-about-git
* https://oschina.gitee.io/learn-git-branching/

# 版本控制

版本迭代

* 开发过程中管理修改历史记录
* 协同开发
* 保护源代码和文档
* 统计工作量
* 并行开发
* 降低人为错误

主流版本控制工具：

* Git
* SVN
* CVS
* VSS
* TFS
* Visual Studio Online

版本控制分类：

* 本地版本控制 (RCS)
* 集中版本控制：所有版本数据保存在服务器上，同步更新或上传自己的修改 (SVN, CVS, VSS)
* 分布式版本控制：所有版本信息同步在每个用户，可以在本地查看所有版本历史，离线提交联网Push，不会因为服务器、网络问题导致不能工作 (Git)

Git和SVN区别：

* SVN是集中式版本控制系统，版本库放在中央服务器，带宽要求高
* Git是分布式版本控制系统，最先进的分布式版本控制系统

Linux和Git之父： Linus Benedic Torvalds 李纳斯·托沃兹

# Git基础操作

| 基础命令 | 说明 |
| ---- | ---- |
| `cd`  | 改变目录 |
| `cd..`  | 回退 |
| `pwd`  | 当前目录路径 |
| `ls( -ll)`  | 当前文件（详细信息） |
| `touch`  | 新建文件 |
| `rm`  | 删除文件 |
| `mkdir`  | 新建目录 |
| `rm -r`  | 删除文件夹 |
| `mv`  | 移动文件 |
| `reset`  | 重新初始化终端/清屏 |
| `clear`  | 清屏 |
| `history`  | 查看命令历史 |
| `help`  | 帮助 |
| `exit`  | 退出 |
| `#`  | 注释 |

# Git环境配置

* 查看配置 `git config -l`
* 设置全局用户名、email地址 `git config --global user.name ` 和 `git config --global user.email `
* 查看全局用户名、email地址 `git config --global --list`
* 所有的配置文件都保存在本地（linux中配置文件都在etc中），用户配置在win下C盘用户文件夹.gitconfig中

# Git基本理论

* 三个本地工作区域 + 一个远程
  * 工作目录 Working Directory ：平时存放项目代码的地方
  * 暂存区 Stage / Index ： 临时存放改动
  * 资源库 Repository / Git Directory ： 本地仓库，安全存放数据的位置，有提交所有版本的数据，HEAD指向最新放入仓库的版本
  * 远程Git仓库 Remote Directory

| 命令(down to top) | 工作区域 | 命令(top to down) |
| :-: | :-: | :-: |
| | Remote Directory | |
|`git push` | | `git pull` - remote to workdir;  |
| | Repository(History) | `git fetch/clone` - remote to repository |
|`git commit -m "info"`| | `git checkout` - repository to workdir| 
| | Stage | |
|`git add`| ||
| | Working Directory | |

* 创建本地仓库
  * `git init` 创建全新仓库
  * `git clone [url]` 镜像远程服务器到本地

* 文件四种状态 `git status`
  * **Untracked**: 未跟踪，文件在文件夹中但是没加入Git库，不参与版本控制。`git add`状态变为 **Staged**
  * **Unmodify**: 文件入库、未修改，即无变化。若被修改，则变为 **Modified**；若`git rm`移除版本库，则变为 **Untracked**
  * **Modified**: 文件修改。若`git add`进入暂存 **Staged**；若`git checkout`则丢弃，返回 **Unmodify**，实际为从版本库Repoisitory中取出历史版本覆盖修改
  * **Staged**: 暂存。若`git commit`则将修改同步到库中，文件变为 **Unmodify**；若`git reset HEAD filename`，则取消暂存，文件恢复 **Modified**

* 忽略文件，在主目录建立".gitignore"
  * 使用Linux通配符
  * ! 表示例外规则，不被忽略
  * 最前面是路径分隔符 / ，则表示要忽略的文件在此目录下，子目录中文件不忽略
  * 最后面是路径分隔符 / ，则表示要忽略的是此目录下该名称的子目录，而非文件（默认两者都忽略）

# 绑定Github

* git bash: `ssh-keygen -t rsa` 生成
* 在github添加


# 许可证
* 开源是否可以随意转载
* 开源但是不能商业使用

# IDEA使用Git

<font size = 6 color = red>待补充</font>

# Git分支

| 命令 | 说明 |
| - | - |
| `git branch` | 列出所有本地分支 |
| `git branch -r` | 列出所有远程分支 |
| `git branch [branch name]` | 新建分支，但仍然停留在当前位置 |
| `git checkout -b [branch]` | 新建分支，并切换到新分支 |
| `git merge [branch]` | 合并指定分支到当前分支 |
| `git branch -d [branch name]` | 删除分支 |
| `git push origin --delete [branch name]` | 删除远程分支 |
| `git branch -dr [remote / branch]` | 删除远程分支 |

* 同一个文件在合并分支的时候如果都被修改了会引起冲突，修改后重新提交
* master主分支应该非常稳定

# 进阶(git exercise)

| 命令 | 说明 |
| - | - |
| `git rebase [target]` | 将当前分支合并到目标分支（看起来串行） |
| `git checkout []` detaching head | 将head指向一次提交 或 分支 |
| `git checkout HEAD^`| ^符号，查找当前分支的父亲分支，^^祖父分支 |
| `git checkout HEAD~n` | ~符号，移动HEAD指向前n个分支（不需要多次^移动） |
| `git branch -f master HEAD~3` | -f，将master移动，~3向上3级 |
| `git reset` | 本地存储，直接回退 |
| `git revert` | 服务器存储，会提交新分支上去（虽然与想要回退的版本完全一样）|

# 更细致的管理

<font size = 6 color = red>待补充</font>

# Commit格式


```
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```

* type用于说明 commit 的类别，只允许使用下面7个标识（特殊加一个revert，在后面)
  * feat：新功能（feature）
  * fix：修补bug
  * docs：文档（documentation）
  * style： 格式（不影响代码运行的变动）
  * refactor：重构（即不是新增功能，也不是修改bug的代码变动）
  * test：增加测试
  * chore：构建过程或辅助工具的变动

* scope
  * scope用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

* subject
  * subject是 commit 目的的简短描述，不超过50个字符。

* body
  * body 部分是对本次 commit 的详细描述，可以分成多行
  * 使用第一人称现在时
  * 说明代码变动的动机，以及与以前行为的对比

* Footer 部分只用于两种情况
  * 如果当前代码与上一个版本不兼容，则 Footer 部分以BREAKING CHANGE开头，后面是对变动的描述、以及变动理由和迁移方法
  * 关闭 Issue，如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue

* 特殊：revert
  * 如果当前 commit 用于撤销以前的 commit，则必须以revert:开头，后面跟着被撤销 Commit 的 Header
  * Body部分的格式是固定的，必须写成This reverts commit <lt;hash>.，其中的hash是被撤销 commit 的 SHA 标识符


# bug

* RPC failed; curl 92 HTTP/2 stream 0 was not closed cleanly: PROTOCOL_ERROR (err 1)
  * You might be pushing data larger than the postBuffer size. You can try increasing post buffer size using `git config --global http.postBuffer 157286400`
* stop when writing objects
  * `git config --global http.postBuffer 524288000`
  * For future references, based on comments:
  * 500 MB: 524288000 (as posted in the original answer)
  * 1 GB: 1048576000
  * 2 GB: 2097152000 (anything higher is rejected as 'out of range')
* stop after total line
  * This turned out to be no problem at all. I simply had to wait until the upload was complete. I had added several large files and there is not a progress indicator.
