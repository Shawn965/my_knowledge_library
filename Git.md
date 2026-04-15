| Git相关技术讲解

# 配置：
`git config [<options>]`

配置文件位置
- `默认`：当前仓库
- `--global`：用户所有仓库（全局变量）

行为
- `--list`：查看配置列表
- --add：添加参数
- --unset：移除参数
- --replace-all：替换参数

用户身份
- user.name
- user.email

远程仓库
- remote.origin.url
- remote.origin.fetch

代理
- http.proxy

**分支**branch
- 指向某个提交的可变指针

**提交**commit
- 包含sha-id、日期、作者等

**暂存区**index
- 介于“工作目录”和“版本仓库”之间的缓冲区，通过add修改存入

**HEAD**
- 指向当前检出的提交或分支的符号引用
- 默认指向所在分支最新提交

**Origin**
- 远程仓库分支

**抽象区域**
【（工作目录，暂存区，贮藏区，本地仓库），（远程仓库）】

#### 克隆
- git **clone** 克隆远程仓库

- `git clone <repo-url>`
- `git` `**-o <remote-name>**` `clone <repo-url>` 修改默认别名 (--origin)

#### 查看类

- git **status** 显示项目文件当前状态

- 指出修改暂存未跟踪文件

- git **log** 检查完整历史提交信息

- `git log --oneline`

- git **show** 查看单一提交的完整信息
- git **diff** 显示文件、分支或提交commit间的差异

- `git diff HEAD` 查看“工作&暂存区”与“最新提交”的差异
- `git diff <branch_name1> <branch_name2>` 俩分支比较
- `git diff <哈希1> <哈希2>` 俩提交比较

- git **blame** 查看代码是谁写的

- `git blame <文件路径>`

- git **remote** 查看远程仓库名字

- `git remote -v` 查看仓库对应的URL链接

- origin [git@gitlab.xxx.com](mailto:git@gitlab.xxx.com):robot/paramconfigurator.git (fetch)
- <**远程仓库别名**> <仓库url> (方式)

#### 提交

- git **add** 暂存修改后的文件，准备提交

- `add .`（添加当前目录及其子目录的所有改动）
- 工作目录 -> 暂存区
- 用以将其包含在下一次commit

- git **commit** 保存提交，记录至本地仓库，附上提交信息

- 暂存区 -> 本地仓库
- `git commit -m "你的提交说明"`

- git **reset** 将分支移至以前的提交、取消暂存、丢弃提交撤销

- `git reset HEAD~1 回退到上一个提交`

- git **tag** 特定点，表示版本或发布

- `git tag <标签名> <可指定commitID>` 创建轻量标签

#### 分支

- git **branch** 查看、创建分支等

- _无后缀_：显示本地分支
- `-r`：查看本地记录的远程跟踪分支

- 所以不一定最新，要最新的话先_git fetch_

- `-v`：查看本地分支+上次提交的信息
- `-vv`：查看本地分支+上次提交的信息+本地和远程分支的关系

- git **checkout** 分支间切换，或回复工作树文件

- `-b <分支名称>`：创建本地分支，切换至该分支
- -d 删除分支

- git **pull** 从远程仓库下载更新，并将其合并到本地仓库

- 远程库 ->本地库&工作区

- git **merge** 将两个分支的提交历史整合

- 本地库-> 工作区
- 把指定的分支**合并到当前分支**，可能产生“合并提交”来集成变更
- 不同的修改文件默默合并，相同的修改要手动解决
- `git merge <branch>`

- git **fetch** 从远程仓库下载更新，无需将其合并到本地分支

- 远程库 ->本地库

- git **push** 将提交从本地仓库上传到远程仓库

- 别人推送了代码，得先pull

- git **stash** 临时保存“工作目录/暂存区”更改，是分支恢复至HEAD状态

- `push "描述"`：暂时存储未提交
- `list`：stash列表
- `pop`：应用最新存储的stash，并从列表中移除
- `apply`：应用最新存储的stash，仍保留在列表

- git **rebase** 变基

#### 信息配置

- `git init` 开档
- `git config --global user.name "Your Name"`
- `git config --global user.email "``email@example.com``"`
- `git config --global --list`

#### 基于远程仓库分支创建本地分支流程

1. 拉取远程仓库的最新状态（更新本地的远程跟踪分支）

2. `git fetch origin`

3. 确认远程跟踪分支

4. `git branch -r`

5. 从远程跟踪分支创建一个本地分支

6. git branch <新分支名> <远程跟踪分支名>

7. 切换到新建本地分支

8. git checkout <新分支名>

#### **Gitlab密钥**

1. 测试安装ssh
2. 配置name/email : git config --global user.name
3. 生成密钥：ssh-keygen -t ed25519 -C "[your_email@example.com](mailto:your_email@example.com)"，然后连续按回车键三次

4. ~~远程仓库叫origin是默认的吗？如何确认~~
5. origin/dev这个名字是一个静态整体还是说是由 origin 和dev两个名字动态合并出来的？
6. git clone 远程仓库，一开始只会创建本地main分支并跟踪远程仓库的main分支吗？其他分支呢？
7. git branch -r 是检查远程仓库的实际最新分支列表，还是上一次fetch获取到的远程仓库分支状态？
8. upstream是什么
9. git pull指令如何使用？为什么pull 的时候是origin dev ，checkout的时候是origin/dev？

10. origin/dev 这个名字，origin是本地起的，但是dev一定是跟远程仓库分支同名是吗

11. 如果一个分支在上一次fetch远程仓库的时候还在，但我没有创建这个分支的本地分支，现在如果远程仓库把这个分支删除了，我在fetch远程仓库，是不是这个分支就无法再找到了？