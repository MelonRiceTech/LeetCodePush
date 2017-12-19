## GIT常用操作
### 1. 获取帮助

```markdown
$ git help <verb>
$ git <verb> --help
$ man git-<verb> 
```
### 2. 获取与创建项目
#### 初始化一个新仓库

`git init`在当前目录下创建.git目录，同时当前目录成为一个Git仓库。
#### 拷贝已有的仓库

`git clone 仓库url` 将http或ssh链接指向的Git仓库拷贝到本地。
```markdown
git clone https://github.com/MelonRiceTech/LeetCodePush.git
```

`git clone 仓库url 本地目录路径`将远程Git仓库拷贝到本地指定目录。
### 3. 添加与提交
#### 使用git add添加需要追踪的新文件和待提交的更改
**工作区->缓存区**
`git add 文件`将文件添加到缓存区，该文件被标记为被追踪。

`git add .`缓存当前目录下所有文件，不包括已删除的文件。
#### 使用git status和git diff查看有何改动


`git status`显示当前仓库的最新状态。

`git status -s`当前仓库的最新状态的简介。

`git diff`比较工作区和缓存区的不同。

`git diff --cached`比较缓存区和仓库的不同。

`git diff 文件`比较指定文件在工作区和缓存区的不同。

`git diff 文件 --cached`比较指定文件在缓存区和仓库的不同。

`git diff 提交版本号1 提交版本号2`比较两次提交之间的区别。

`git diff 分支1 分支2`比较两个分支之间的区别。
#### 使用git commit提交快照
**缓存区->仓库**
`git commit -m "本次提交说明"`一次性将缓存区所有文件修改提交到仓库的当前分支。

`git commit -am "本次提交说明"`自动把所有已经跟踪过的文件缓存，并提交到仓库。常用于跳过git add步骤快速提交。

`git commit --amend "本次提交说明"`重新提交。此次提交代替上一次提交的结果。尤其适用于提交完了才发现漏掉了几个文件没有添加，或者提交信息写错了的情况。
#### git show
`git show`查看最后一个提交的内容。

`git show HEAD~1`查看倒数第二个提交的内容。

`git show 提交版本号`查看指定提交的内容。
### 4. 删除与恢复
#### git rm
主要用于从版本库中删除文件。

`git rm 文件`把文件从版本库中删除，不再跟踪。

`git rm log/\*.log`将log目录下扩展名为.log的所有文件从版本库中删除，不再跟踪。通常适用于不小心把一些编译、日志、debug文件错误提交到版本库。

`git rm -f 文件`当文件有未提交的缓存区修改时，直接使用git rm 文件会报错。此时执行此命令可强制将文件从缓存区和版本库中删除。

`git rm --cached 文件`把文件从版本库中删除，但让文件保留在工作区且不被Git继续跟踪。通常适用于rm文件之后把其添加到.gitignore中。
#### 恢复
`git checkout -- 文件`丢弃工作区的修改。此文件必须是Git跟踪的。

1. 修改后仍未放到缓存区，恢复到上一次git commit的状态。
2. 添加到缓存区后又做了修改，恢复到上一次git add的状态。

`git reset HEAD 文件`丢弃缓存区的修改，回退到工作区。

`git reset --hard`重置所有文件到上次commit的状态。

`git reset --hard HEAD~1`将当前分支重置为倒数第2个版本。

`git reset --hard 提交版本号`将当前分支重置为指定版本。
### 5. 版本控制
#### 版本号
**Git的版本号是SHA1校验和**，而不是用递增的1、2、3……，因为分布式的版本控制系统要确保每个用户的修改记录都是唯一的，不会发生版本号冲突的情况。

`HEAD`表示当前版本，`HEAD^`表示上一个版本，`HEAD^100`表示往上100个版本。
#### git log
`git log`显示从最近到最远的提交日志。包含每个提交的SHA1校验和、作者的名字和邮箱、提交时间以及提交说明等。

`git log --oneline`git log的简要版。

`git log --decorate`不仅输出git log的信息，还带标签等额外信息。

`git log --graph` 不仅输出git log的信息，还可查看当前分支什么时候出现了分支、合并。

`git log 分支名`查看指定分支的提交日志。

`git log 要查看的分支名branchA ^要忽略的分支名branchB`查看branchA的日志信息（排除branchB的信息）
#### git reflog
记录每一次的版本改动。包括commit记录、reset版本退回记录。
#### git tag
`git tag`查看所有标签。注意：标签不是按时间列出，而是按字母排序。

`git show <tag-name>`查看指定标签的信息。

`git tag <tag-name> <commit-id>`在指定版本号上打上标签。

`git checkout <tag-name>`切换到指定标签。

`git push --tags`将标签推送给远程仓库。
### 6. 远程项目
#### git remote
`git remote add <shortname> <url>`添加并关联一个远程库。shortname一般为origin。

以http方式添加：

```markdown
git remote add origin https://github.com/MelonRiceTech/LeetCodePush.git
```

以ssh方式添加:

```markdown
git remote add origin git@github.com:MelonRiceTech/LeetCodePush.git
```
`git remote`查看已配置的远程仓库，列出各远程仓库的shortname。

`git remote -v`查看已配置的远程仓库的读写url。

```markdown
// git remote -v
origin  git@github.com:MelonRiceTech/LeetCodePush.git (fetch)
origin  git@github.com:MelonRiceTech/LeetCodePush.git (push)
```
`git remote show <shortname>`查看shortname对应的远程仓库的fetch和push等详细信息。

```markdown
* remote origin
    Fetch URL: git@github.com:MelonRiceTech/LeetCodePush.git
    Push  URL: git@github.com:MelonRiceTech/LeetCodePush.git
    HEAD branch: (unknown)
```
`git remote rm <shortname>`移除指定的远程仓库。

`git remote rename <old_shortname> <new_shortname>`重命名一个远程仓库的shortname。
#### git push
`git push <remote-repo-shortname> <local-branch>`将本地分支推送到远程仓库。
#### git pull
`git pull <remote-shortname> <local-branch>`拉取远程仓库最新提交，并合并到指定的本地分支上。

`git fetch`拉取远程仓库最新提交，但不会自动合并分支。
### 7. 分支
#### git branch
`git branch`列出本地分支列表。当前分支前会标有*号。

`git branch -r`列出远程分支列表。

`git branch -a`列出所有分支列表。

`git branch 分支`创建新分支。

`git branch -d 分支`删除指定分支。

`git branch -v -a`查看所有分支的最后一次提交。
#### git checkout
`git checkout 分支`切换到指定分支。

`git checkout -b 分支`创建并切换到指定分支。
#### git merge
`git merge 分支`将指定分支合并到当前分支上。
### 8. 合并冲突
不同分支修改了相同区块的代码时，合并分支时git会将此部分标记为冲突，需要用户手动去修改。
可用`git diff`查看冲突详情
可用`git status -s`查看冲突文件，状态标识为UU。
手动修改后，使用`git add`重新写入缓存区。
### 9. git config
`git config --list`列出所有配置信息。

`git config <key>`检查关键字key的配置。如git config user.name，查看姓名配置。

`git config --global alias.命令别名 命令`为指定命令配置一个别名，可快速输入命令。

1. `git config --global alias.unadd 'reset HEAD'`使用`git unadd`文件可丢弃指定文件在缓存区的修改。
2. `git config --global alias.st status`使用`git st`代替`git status`。

3. `git config --global alias.co checkout`使用`git co`代替`git checkout`。

4. `git config --global alias.cm commit`使用`git cm`代替`git commit`。

5. `git config --global alias.br branch`使用`git br`代替`git branch`。

6. `git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"`使用`git lg`输出高逼格的日志信息。

7. `git config --global alias.last 'log -1'`使用`git last`显示最近一次的提交。

`git config --global user.name "yourname"`和`git config --global user.email "youremail"`修改姓名和邮箱，去掉--global可针对每个repo单独设定。

### 10. git rebase
`git rebase`和`git merge`都被设计来将一个分支的更改并入另一个分支，只不过方式有些不同。

####Merge

将 master 分支合并到 feature 分支最简单的办法就是用下面的命令

`git checkout feature`
`git merge master`

或者，你也可以把它们压缩在一行里。

`git merge master feature`
feature 分支中新的合并提交（merge commit）将两个分支的历史连在了一起。

Merge 好在它是一个安全的操作。现有的分支不会被更改，避免了 rebase 潜在的缺点。

####rebase
作为 merge 的替代选择，你可以像下面这样将 feature 分支并入 master 分支：

`git checkout feature`

`git rebase master`

它会把整个 feature 分支移动到 master 分支的后面，有效地把所有 master 分支上新的提交并入过来。但是，rebase 为原分支上每一个提交创建一个新的提交，重写了项目历史，并且不会带来合并提交。

rebase最大的好处是你的项目历史会非常整洁。首先，它不像`git merge`那样引入不必要的合并提交。其次，rebase 导致最后的项目历史呈现出完美的线性——你可以从项目终点到起点浏览而不需要任何的 fork。这让你更容易使用`git log`、`git bisect`和`gitk`来查看项目历史。

不过，这种简单的提交历史会带来两个后果：安全性和可跟踪性。如果你违反了 rebase 黄金法则，重写项目历史可能会给你的协作工作流带来灾难性的影响。此外，rebase 不会有合并提交中附带的信息——你看不到 feature 分支中并入了上游的哪些更改。

