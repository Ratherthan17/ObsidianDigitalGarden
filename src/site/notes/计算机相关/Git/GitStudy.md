---
{"dg-publish":true,"permalink":"/计算机相关/Git/GitStudy/","created":"2025-04-01T14:39:00","updated":"2025-04-01T16:10:48.000+08:00"}
---


---

# Git  常用指令速查表

## 仓库操作

| 指令                               | 作用       |
| -------------------------------- | -------- |
| git init                         | 初始化新仓库   |
| git clone <远程仓库 URL>             | 克隆远程仓库   |
| git remote add origin <远程仓库 URL> | 关联远程仓库   |
| git remote -v                    | 查看远程仓库地址 |
## 环境配置

| 指令                                            | 作用       |
| --------------------------------------------- | -------- |
| git config --global user.name “你的名字"          | 设置全局用户名  |
| git config --global user.email“你的邮箱"          | 设置全局邮箱   |
| git config --list                             | 查看所有配置信息 |
| git config user.name<br>git config user.email | 查看当前用户信息 |
## 文件操作

- **添加文件到暂存区**

| 指令                   | 作用               |
| -------------------- | ---------------- |
| git status           | 查看当前文件的状态        |
| git add 文件名1 文件名2... | 添加指定文件到暂存区       |
| git add .            | 添加当前目录的所有文件到暂存区  |
| git add dir名         | 添加指定目录到暂存区，包括子目录 |

- **删除和重命名文件**

| 指令                  | 作用                   |
| ------------------- | -------------------- |
| git rm 文件名1 文件2     | 删除工作区文件，并且将这次删除放入暂存区 |
| git restore 文件名     | 丢弃工作区修改（Git2.23+）    |
| git rm --cached 文件名 | 停止追踪指定文件，但该文件会保留在工作区 |
| git mv 原名 新名        | 给文件改名，并将这个改变放入暂存区    |
## 提交代码

```git
# 提交暂存区到仓库区
$ git commit -m [message]

# 提交暂存区的指定文件到仓库区
$ git commit [file1] [file2] ... -m [message]

# 提交工作区自上次commit之后的变化，直接到仓库区
$ git commit -a

# 提交时显示所有diff信息
$ git commit -v

# 使用一次新的commit，替代上一次提交
# 如果代码没有任何新变化，则用来改写上一次commit的提交信息
$ git commit --amend -m [message]

# 重做上一次commit，并包括指定文件的新变化
$ git commit --amend [file1] [file2] ...

```

## 分支管理

- **分支操作**

```git
# 列出所有本地分支
$ git branch

# 列出所有远程分支
$ git branch -r

# 列出所有本地分支和远程分支
$ git branch -a

# 切换到现有的某个分支
$ git checkout 分支名

# 重命名分支
$ git branch -m 名字

# 新建一个分支，但依然停留在当前分支
$ git branch [branch-name]

# 新建一个分支，并切换到该分支
$ git checkout -b [branch]

# 新建一个分支，与远程分支同步，并切换到该分支
$ git checkout -b [branch] [remote-branch]

# 新建一个分支，指向指定commit
$ git branch [branch] [commit]

# 新建一个分支，与指定的远程分支建立追踪关系
$ git branch --track [branch] [remote-branch]

# 切换到指定分支，并更新工作区
$ git checkout [branch-name]

# 切换到上一个分支
$ git checkout -

# 建立追踪关系，在现有分支与指定的远程分支之间
$ git branch --set-upstream-to=origin/<branch> <branch>

```

- **分支合并与删除**

```git
# 合并指定分支到当前分支
$ git merge [branch]

# 选择一个commit，合并进当前分支
$ git cherry-pick [commit]

# 删除本地分支
$ git branch -d [branch-name]

# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]

```

## 标签管理

```git
# 列出所有tag
$ git tag

# 新建一个tag在当前commit
$ git tag [tag]

# 新建一个tag在指定commit
$ git tag [tag] [commit]

# 删除本地tag
$ git tag -d [tag]

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

## 查看信息

- **基本信息查看**

```git
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

```

- **文件历史查看**

```git
# 显示某个文件的版本历史，包括文件改名
$ git log --follow [file]
$ git whatchanged [file]

# 显示指定文件相关的每一次diff
$ git log -p [file]

# 显示过去5次提交
$ git log -5 --pretty --oneline

# 显示所有提交过的用户，按提交次数排序
$ git shortlog -sn

# 显示指定文件是什么人在什么时间修改过
$ git blame [file]
```

- **差异比较**

```git
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

## 远程同步

```git
# 下载远程仓库的所有变动
$ git fetch [remote]

# 显示所有远程仓库
$ git remote -v

# 显示某个远程仓库的信息
$ git remote show [remote]

# 增加一个新的远程仓库，并命名
$ git remote add [shortname] [url]

# 取回远程仓库的变化，并与本地分支合并
$ git pull [remote] [branch]

# 上传本地指定分支到远程仓库
$ git push [remote] [branch]

# 强行推送当前分支到远程仓库，即使有冲突
$ git push [remote] --force

# 推送所有分支到远程仓库
$ git push [remote] --all
```

## 撤销操作

- **文件恢复**

```git
# 恢复暂存区的指定文件到工作区
$ git checkout [file]

# 恢复某个commit的指定文件到暂存区和工作区
$ git checkout [commit] [file]

# 恢复暂存区的所有文件到工作区
$ git checkout .
```

- **版本回退**

```git
# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
$ git reset [file]

# 重置暂存区与工作区，与上一次commit保持一致
$ git reset --hard

# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
$ git reset [commit]

# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
$ git reset --hard [commit]

# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
$ git reset --keep [commit]

# 新建一个commit，用来撤销指定commit
# 后者的所有变化都将被前者抵消，并且应用到当前分支
$ git revert [commit]

```

- **暂存操作**

```git
# 暂时将未提交的变化移除，临时保存工作进度
$ git stash

# 恢复临时保存的进度
$ git stash pop
```

## 获取帮助

| 指令              | 作用             |
| --------------- | -------------- |
| git help        | 获取 git 命令使用手册  |
| git help config | 获取 config 命令手册 |

---
# Git 教程

---

- [Oh Shit, Git!?!——用Git过程中可能会遇到的错误的解决办法][Oh Shit, Git!?!]
- [Learn git branching——学习Git的网站][Learn git branching]

---

- [黑马程序员Git全套教程，完整的git项目管理工具教程，一套精通git][黑马程序员Git全套教程，完整的git项目管理工具教程，一套精通git]
- [尚硅谷Git入门到精通全套教程（涵盖GitHub\Gitee码云\GitLab）][尚硅谷Git入门到精通全套教程（涵盖GitHub\Gitee码云\GitLab）]
- [2022全新Git实战教程丨看故事学git，通俗易懂][2022全新Git实战教程丨看故事学git，通俗易懂]

---

- [Git工作流和核心原理 | GitHub基本操作 | VS Code里使用Git和关联GitHub][Git工作流和核心原理]
-  [B站UP主 编程八点档 的 Git教程 合集][编程八点档 的 Git教程 合集]
-  [Github使用教程-黑马程序员][Github使用教程-黑马程序员]
-  [Git&Github基础知识附完美解决[rejected] master -＞ master (fetch first)问题方法][Git&Github基础知识]

---

  
  

[Oh Shit, Git!?!]: https://ohshitgit.com/zh
[Learn git branching]: https://learngitbranching.js.org/?locale=zh_CN%252520git


[黑马程序员Git全套教程，完整的git项目管理工具教程，一套精通git]: https://www.bilibili.com/video/BV1MU4y1Y7h5/?spm_id_from=333.337.search-card.all.click&vd_source=4f65863adf19c12522e7026402e62e53

[尚硅谷Git入门到精通全套教程（涵盖GitHub\Gitee码云\GitLab）]: https://www.bilibili.com/video/BV1vy4y1s7k6/?spm_id_from=333.337.search-card.all.click&vd_source=4f65863adf19c12522e7026402e62e53

[2022全新Git实战教程丨看故事学git，通俗易懂]: https://www.bilibili.com/video/BV1zN4y1N7wz/?spm_id_from=333.337.search-card.all.click&vd_source=4f65863adf19c12522e7026402e62e53

 

[Git&Github基础知识]: https://blog.csdn.net/qq_44631615/article/details/124360109?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-124360109-blog-52780677.235%5Ev38%5Epc_relevant_anti_t3_base&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-124360109-blog-52780677.235%5Ev38%5Epc_relevant_anti_t3_base&utm_relevant_index=3

[Git工作流和核心原理]: https://www.bilibili.com/video/BV1r3411F7kn/?spm_id_from=333.1007.top_right_bar_window_custom_collection.content.click&vd_source=4f65863adf19c12522e7026402e62e53

[GitHub使用教程-黑马程序员]: https://www.bilibili.com/video/BV1st411r7Sj?p=1&vd_source=4f65863adf19c12522e7026402e62e53

[编程八点档 的 Git教程 合集]: https://space.bilibili.com/1056179587/channel/seriesdetail?sid=2276054