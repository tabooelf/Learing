# GIT Learning Log - Command

### 1 Work flow & Proper Nouns

![v](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015120901.png)

**1. `WorkSpace` : 持有可实际需要编辑文件**
**2. `Index / Stage` :  暂存区=缓存区=购物车，临时存放你的改动**
**3. `HEAD` :  指向你最后提交的结果**

:black_medium_small_square:`Remote`  : 远程仓库

:black_medium_small_square:`Repository` : 仓库区（本地仓库）

**GitHub**

 Remote 默认名称 `Origin` 

 默认主分支 `Master`  用于正式发布

`dev` 开发分支

`feature ` 新特性分支

### 2. Create a New Repository

```python
  # 在当前目录新建一个Git代码库
  # [project-name] 新建并初始化的代码库名称
  $ git init [project-name]
 
  #创建一个本地仓库的克隆版本
  $ git clone /path/to/repository
  #创建一个远程仓库的克隆版本
  $ git clone username@host:/path/to/repository
```

### 3. Configuration

```python
# 显示当前的Git配置
$ git config --list

# 编辑Git配置文件
$ git config -e [--global]

# 设置提交代码时的用户信息
$ git config [--global] user.name "[name]"
$ git config [--global] user.email "[email address]"
```

### 4. Add&Delete

```python
# [.]添加当前目录的所有文件到暂存区
# [-p]添加每个变化前，都会要求确认，对于同一个文件的多处变化，可以实现分次提交
# [<pathspec>...] 添加指定文件或目录到暂存区，包括子目录
# <pathspec> 可以是[Branch] [HEAD] [Tag]
# Fileglobs (e.g. *.c) can be given to add all matching file
$ git add [.][-p][<pathspec>...]

# 删除工作区文件，并且将这次删除放入暂存区
# [--cached] 停止追踪指定文件，但该文件会保留在工作区
$ git rm [--cached][<file>...]

# 改名文件，并且将这个改名放入暂存区
$ git mv [file-original] [file-renamed]
```

### 5. Commit

```python
# [<file>...]...提交暂存区[指定一个或多个文件]到仓库区
# [-a]提交工作区自上次commit之后的变化，直接到仓库区
# [-v]提交时显示所有diff信息
# [--amend]使用一次新的commit，替代上一次提交
$ git commit [-a][-v][--amend] [<file>...] -m [message]
```

### 6. Branch

```python
# 查看所有本地分支
# [-a]查看所有本地分支和远程分支
# [-r]查看所有远程分支
$ git branch [-r | -a] 

# 新建一个分支
# -b 换到该分支
# --track 新建分支与指定的远程分支建立追踪关系
# --set-upstream 建立追踪关系，不指定上游，现有分支与指定的远程分支之间
# <start-point> 新建分支HEAD指向Commit,本地或者远程皆可
$ git branch [--set-upstream | --track | --no-track] [-b] [-f] <branchname> [<start-point>]

# 删除分支
# -r 同时删除远程分支 
# -D 等同于 --delete --force 
$ git branch (-d | -D) [-r] <branchname>…

# 重命名或移动分支
# -M 等同于 --move --force
$ git branch (-m | -M) [<oldbranch>] <newbranch>

# 切换到指定分支，并更新工作区
# "-"切换到上一个分支
$ git checkout [branch-name] 
$ git checkout -

# 合并指定分支到当前分支
# 默认 fast-forward 合并无记录
# --no-ff 禁用 fast-forward，合并有记录
# [-m <msg>] 合并说明
$ git merge [--no-ff] [-m <msg>] [<branchname> | <commit>...]

# 远程更新指定对象
# <pathspec> 可以是[Branch] [HEAD] [Tag] 等
# [-d | --delete] 删除命令
# GitHub 默认 <repository> 为Origin
# [-u]为--set-upstream 建立关联，不指定上游
$ git push [-u] <repository> [-d | --delete] [<pathspec>...]
```

### 7. Tag

```python
  # 列出所有tag
  $ git tag
  
  # 新建一个tag在指定commit，[commit]省略表示当前
  # [-d] 删除
  $ git tag [-d] [tag] [commit]
 
  # 删除远程tag
  $ git push origin :refs/tags/[tagName]
 
  # 查看tag信息
  $ git show [tag]
 
  # 提交指定tag
  $ git push [remote] [tag]
 
  # 提交所有tag
  $ git push [remote] --tags
 
  # 新建一个分支，指向某个tag
  $ git checkout -b [branch] [tag]
 
```

### 8. View Info

```python
  # 显示有变更的文件
  $ git status
 
  # 显示当前分支的版本历史
  $ git log
 
  # 显示commit历史，以及每次commit发生变更的文件
  $ git log --stat
 
  # 搜索提交历史，根据关键词
  $ git log -S [keyword]
 
  # 显示某个commit之后的所有变动，每个commit占据一行
  $ git log [tag] HEAD --pretty=format:%s
 
  # 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
  $ git log [tag] HEAD --grep feature
 
  # 显示某个文件的版本历史，包括文件改名
  $ git log --follow [file]
  $ git whatchanged [file]
 
  # 显示指定文件相关的每一次diff
  $ git log -p [file]
 
  # 显示过去5次提交，每条log只显示第一行
  $ git log -5 --pretty --oneline
 
  # 显示所有提交过的用户，按提交次数排序
  $ git shortlog -sn
 
  # 显示指定文件是什么人在什么时间修改过
  $ git blame [file]
 
  # 显示暂存区和工作区的差异
  $ git diff
 
  # 显示暂存区和上一个commit的差异
  $ git diff --cached [file]
 
  # 显示工作区与当前分支最新commit之间的差异
  $ git diff HEAD
 
  # 显示两次提交之间的差异
  $ git diff [first-branch]...[second-branch]
 
  # 显示今天你写了多少行代码
  $ git diff --shortstat "@{0 day ago}"
 
  # 显示某次提交的元数据和内容变化
  $ git show [commit]
 
  # 显示某次提交发生变化的文件
  $ git show --name-only [commit]
 
  # 显示某次提交时，某个文件的内容
  $ git show [commit]:[filename]
 
  # 显示当前分支的最近几次提交
  $ git reflog
 
```

### 9. Remote & Sync

```python
  # 下载远程仓库的所有变动
  $ git fetch [remote]

  # 显示所有远程仓库
  $ git remote -v
  
  # 显示某个远程仓库的信息
  $ git remote show [remote]

  # 增加一个新的远程仓库，并命名
  $ git remote add [shortname] [url]
  
  # 取回远程仓库的变化，并与本地分支合并怕 Github默认[remote]值为Origin
  $ git pull [remote] [branch]

  # 上传本地指定分支到远程仓库
  $ git push [remote] [branch]

  # 强行推送当前分支到远程仓库，即使有冲突
  $ git push [remote] --force

  # 推送所有分支到远程仓库
  $ git push [remote] --all
```

### 10. Undo

```python
  # 恢复某个commit或指定文件到暂存区和工作区
  # [.] 暂存区所有文件
  $ git checkout [commit | file][.]

  # 重置当前对象，同时重置暂存区,但工作区不变
  # [commit] 指定对象HEAD为指定commit,省略表示上次commit
  # [file] 暂存区指定文件 ，省略表示整个暂存区
  # [--hard] 同时重置暂存区和工作区
  # [--keep] 保持暂存区和工作区不变
  #  [^|^^|~number] 分别表示 上版本，上上版本，上number版本
  $ git reset [--keep][--hard][^|^^|~number][file][commit]

  # 新建一个commit，用来撤销指定commit
  # 后者的所有变化都将被前者抵消，并且应用到当前分支
  $ git revert [commit]

  # 暂时将未提交的变化移除，稍后再移入
  $ git stash
  # 恢复并删除
  $ git stash pop
  # 查看stash list 并回复指定 stash@{0}
  $ git stash list
  $ git stash apply stash@{0}
```

### 11. Other

```python
 # 生成一个可供发布的压缩包
 $ git archive
```

