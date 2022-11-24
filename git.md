# 架构

![](imgs/git架构.jpg)

stage：暂存区

master：默认主分支

HEAD指向当前版本

Git 跟踪并管理修改，而非文件

# 常用命令

初始化 git 仓库 repository:

```sh
git init
```

添加文件到仓库:

```sh
git add readme.txt
```

提交文件到仓库:

```sh
git commit -m "wrote a readme file"
# -m 后面输入的是本次提交的说明
```

# 版本管理

> HEAD指向当前版本
>
> 穿梭前，用git log 查看提交历史，以确定回退版本
>
> 要重返未来，用git reflog 查看命令历史，以确定回到未来的版本

### 查看工作区状态 -- 简

```sh
git status
```

### 查看修改内容

```sh
git diff readme.txt
# 查看difference，显示格式为Unix通用的diff格式
```

### 查看提交日志

```sh
git log
# 显示从最近到最远的提交日志，可以看到3次提交
# 如果嫌输出信息过多，可以加上 --pretty=oneline 参数
```

### 版本回退

```sh
git reset --hard HEAD^
# HEAD表示当前版本，HEAD^是上一个版本，往上n个版本为 HEAD~n
# --hard 参数
```

### 回到指定版本

```sh
git reset --hard 1094a
# 1094a为该版本的commit id前几位
```

### 查看命令记录

```sh
git reflog
```

### 撤销修改

```sh
git checkout -- readme.txt
# 两种情况：1.修改后没add到暂存区 => 回到版本库状态
#		  2.已在暂存区，又修改  => 回到暂存区修改前状态

# in all: 会回到最近一次 git commit 或 git add时状态
# 命令中的 -- 很重要
```

```sh
git reset HEAD readme.txt
# 把暂存区的修改撤销，重新回到工作区
```

### 删除文件

> 删除 rm 和添加 add 都属于同类型操作，对工作区、暂存区、版本库的影响相同，都是一种 “修改”

```sh
git rm test.txt
git commit -m "remove test.txt"
```

```sh
# 如果误删
git checkout -- test.txt
# git checkout 用版本库里的版本替换工作区的版本
```



# 远程仓库

> 第一次使用 Git clone/push 时会出现SSH警告

### 关联远程仓库

```sh
git remote add origin git@github.com:xxx/xxx.git
# 添加后，远程库的名字就是origin，这是Git默认叫法，也可以更改
```

### 推送到远程库

```sh
git push -u origin master
# 把当前分支master推送到远程库，
# -u把本地master和远程master关联起来，只用关联一次
```

### 查看远程库信息

```sh
git remote -v
```

### 删除远程库

```sh
git remote rm origin
# "删除"为解除本地和远程绑定关系
```

### 从远程库克隆

```sh
git clone git@github.com:xxx/xxx.git
# 会直接克隆到以仓库名为名的文件夹里
# ssh协议速度最快
```



# 分支管理

> 分支之间的跳转，需要保证该分支下工作区、暂存区域分支提交相同，无修改。即 git diff HEAD 无差异

### 创建分支

```sh
git branch dev
```

### 切换分支

```sh
git checkout dev
git switch dev	# 推荐
```

```sh
git checkout -b dev
git switch -c dev	# 推荐
# 上两步简写，创建并切换到dev
```

### 查看分支

```sh
git branch
```

### 合并分支

```sh
git merge dev
# 合并dev到当前分支
```

### 删除分支

```sh
git branch -d dev
```

