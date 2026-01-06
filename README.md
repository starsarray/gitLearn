这是一个git命令学习仓库
#### 配置git

Git用户名

```cmd
git config --global user.name "Your Name"
```

邮箱

```cmd
git config --global user.email "email@example.com"
```

Git显示颜色

```cmd
git config --global color.ui true
```

Git别名

```cmd
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
```



#### 初始化

创建项目文件夹，进入到文件夹里，然后初始化Git。

```cmd
mkdir project
cd project
git init
```

#### 添加文件并提交代码(`git commit`之前需先`git add`，`commit`只负责提交`暂存区`的内容)

```cmd
git add README.md(文件名)
# git add -f README.md(-f为强制添加，可提交.gitignore中配置的文件)

git commit -m "提交备注"
```

#### 查看当前仓库状态

```cmd
git status
```

#### 对比文件改动内容

```cmd
git diff README.md(文件名)
```

#### 查看Git日志

```cmd
git log
```

#### 版本回退到第N个版本前

```cmd
git reset --hard HEAD~N
```

#### 版本回退(切换)到指定版本(git每次提交的唯一十六进制的id，`git log`或者`git reflog`(记录每次一提交的信息)可以查看)

```cmd
git reset --hard e475afc93c209a690c39c13a46716e8fa000c366(版本号，这只是个例子，此值不必写全，只要能让git知道是哪个把那本就行，一般写5-6位即可)
```

#### 撤销修改(撤销到最近一次`git add`或`git commit`之前的状态)

```cmd
git checkout -- README.md(文件名)
```

#### 撤销暂存区的修改(`git commit`之前)

```cmd
git reset HEAD README.md(文件名)
```

#### 回退到上个提交

```cmd
git reset --hard HEAD~1
```



#### 删除文件(确定删除需要`git commit`，若误删可以使用`git checkout -- 文件名`)

```cmd
git rm README.md(文件名)
```

#### 查看远程仓库连接信息(fetch抓取，push推送)

```cmd
git remote -v
```

#### 关联远程仓库

```cmd
git remote add origin git@github.com:username/xxxx.git
```

#### 推送到远程库(第一次推送`master`分支)

```cmd
git push -u origin master
```

#### 推送到远程库

```cmd
git push origin 分支名
```

#### 克隆代码

```cmd
git clone https://github.com/username/xxxx.git
```

或

```cmd
git clone git@github.com:username/xxxx.git
```

#### 克隆指定分支代码

```cmd
git clone -b 分支名 https://github.com/username/xxxx.git
```

#### 创建分支

```cmd
git branch 分支名
```

#### 切换分支

老版本

```cmd
git checkout 分支名
```

新版本

```cmd
git switch 分支名
```

#### 创建分支并切换

老版本

```cmd
git checkout -b 分支名
```

新版本

```cmd
git switch -c 分支名
```

#### 查看分支

```cmd
git branch
```

#### 查看所有分支(本地+远程，远程分支会以红色标出，当前分支前面会标一个`*`号)

```cmd
git branch -a
```

#### 查看当前分支未合并的分支

```cmd
git branch --no-merged
```

#### 合并某分支到当前分支，若存在冲突会提示手动修改后再提交，`git merge`默认为`fast forward`模式

`fast forward`模式

```cmd
git merge 其他分支名
```

禁用`Fast forward`模式(`--no-ff`) **推荐**

```cmd
git merge --no-ff -m "提交备注" 其他分支名
```

取消还未提交的合并

```cmd
git merge --abort
```

用`git log --graph --pretty=oneline --abbrev-commit`命令可以看到分支合并图

#### 删除当前分支已合并的分支

```cmd
git branch -d 分支名
```

强行删除分支

```cmd
git branch -D 分支名
```

#### 保存工作空间

```cmd
git stash
```

#### 查看保存的工作空间

```cmd
git stash list
```

#### 从保存的工作空间恢复

```cmd
git stash apply
```

若存在多个保存的工作空间(n为序号0开始)

```cmd
git stash apply stash@{n}
```

#### 删除保存的工作空间

```cmd
git stash drop
```

若存在多个保存的工作空间(n为序号0开始)

```cmd
git stash drop stash@{n}
```

#### 从保存的工作空间恢复并删除保存的空间

```cmd
git stash pop
```

若存在多个保存的工作空间(n为序号0开始)

```cmd
git stash pop stash@{n}
```

#### 将其他分支上的提交应用到当前分支

```cmd
git cherry-pick commit的编号
```

#### 抓取代码

```cmd
git pull
```

#### 将本地分支与远程分支关联

```cmd
git branch --set-upstream-to 分支名 origin/分支名
```

#### 把本地未push的分叉提交历史整理成直线；

```cmd
git rebase
```

> rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

#### 打标签

```cmd
git tag v1.0 commit的id(不加则为之后的commit添加标签)
git tag -a v1.0 -m "提交备注" commit的id(不加则为之后的commit添加标签)
```

#### 查看所有标签

```cmd
git tag
```

#### 查看标签信息

```cmd
git show v1.0
```

#### 删除本地标签

```cmd
git tag -d v0.1
```

#### 删除远程标签

```cmd
git push origin :refs/tags/v1.0
```

#### 推送某个标签到远程

```cmd
git push origin v1.0
```

#### 推送全部尚未推送的标签

```cmd
git push origin --tags
```

#### 同一套代码关联多个远程库(同时关联github和gitee为例)

关联GitHub的远程库

```cmd
git remote add github git@github.com:username/xxxx.git
```

关联Gitee的远程库

```cmd
git remote add gitee git@gitee.com:username/xxxx.git
```

推送Github

```cmd
git push github master
```

推送Gitee

```cmd
git push gitee master
```

#### 查看`.gitignore`文件中哪条规则写错了

```cmd
git check-ignore -v 文件名
```