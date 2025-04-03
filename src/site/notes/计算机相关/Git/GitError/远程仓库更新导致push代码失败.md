---
{"dg-publish":true,"permalink":"/计算机相关/Git/GitError/远程仓库更新导致push代码失败/","created":"2024年03月05日 星期二 17:04","updated":"2025-04-01T21:48:30.434+08:00"}
---


---

> 参考自：
> 
> 1. [git push错误failed to push some refs to的解决方法](https://www.cnblogs.com/Rainingday/p/12364690.html)
> 2. [使用git stash命令保存和恢复进度](https://blog.csdn.net/daguanjia11/article/details/73810577)
>
> 
> 2023年10月26日

---

# push 出错

> 可恶，之前在 GitHub 上在线修改了 notes 仓库里的文件，而我在本地又修改了许多代码，导致我把本地代码 push 到 GitHub 上时出错了  
>
> 错误信息：

```shell
To https://github.com/Ratherthan17/my-website.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/Ratherthan17/my-website.git'
hint: Updates were rejected because the remote contains work that you do not
hint: have locally. This is usually caused by another repository pushing to
hint: the same ref. If you want to integrate the remote changes, use
hint: 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

# 解决办法：

## 1. 先将工作区中未完成的内容添加到暂存区  

![1先add](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/1先add.6t7aku3f6z.webp)

## 2. 查看本地库与哪些远程库有联系

- 在终端里输入 ``` git remote -v ``` 查看本地库与哪些远程库有联系  

![2输入git-remote--v](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/2输入git-remote--v.8l09frcv4l.webp)

## 3. 保存未完成的工作进度

- 输入 ``` git stash save '信息' ``` 保存未完成的工作进度

![3输入git-stash-save](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/3输入git-stash-save.969x227z33.webp)

 ![3输入git-stash-save-效果](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/3输入git-stash-save-效果.64e10u8wvm.webp)
 
## 4. 把远程库中的更新合并到本地库中

- 输入 ``` git pull --rebase origin branch ``` 
	- origin 就是第二步输入 ``` git remote -v ``` 后显示的与本地库有联系的远程库，不一定是 origin ，我这里就是 my-website ;
	- branch 是你要 push 到哪个分支就输入哪个分支，我这里是主分支 main  
  
![4输入git-pull-rebase-origin-branch](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/4输入git-pull-rebase-origin-branch.2dovflk1o4.webp)

## 5. 恢复之前保存的工作进度

- 输入 ``` git stash pop ``` ，把之前保存的工作进度恢复

![5输入git-stash-pop](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/5输入git-stash-pop.77dqbq4qra.webp)

## 6. 解决冲突

- 点击 Merge Changes 里的文件，在打开的窗口里点击标红的地方，跳转到冲突位置

![6解决冲突-1](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/6解决冲突-1.2h8hdbd4e0.webp)
 
![6解决冲突-2-点击标红的地方](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/6解决冲突-2-点击标红的地方.3gokqhfvjt.webp)

-  以我这里的 Divination 为例，绿色区域（Current Change）是它在 GitHub 上的样子，蓝色区域（Incoming Change）是它在本地的样子。

![6解决冲突-3-选择要保留的内容2](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/6解决冲突-3-选择要保留的内容2.58hjldz8fx.webp)

- 要是想保留**远程库**的内容，就把本地的（蓝色区域）删掉，再删去 <<<<<<< Updated upstream 、 =======

![保留远程](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/保留远程.8l09frfssq.gif)

- 要是想保留**本地**的内容，就把远程库（绿色区域）删掉，再删去  ======= 和 >>>>>>> Stashed changes

![保留本地](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/保留本地.9rjkod4pe1.gif)

- 要是远程和本地的内容都想保留，就只需把 <<<<<<< Updated upsteam 、 ======= 和 >>>>>>> Stashed changes 删掉就可以了

![本地和远程都保留](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/本地和远程都保留.4ub3uiqxl9.gif)

- 使用 VSCode 提供的按钮可以很方便的进行修改

	- 保留远程库的内容 ——> 点击 `Accept Current Change`

 ![使用VSCode保留远程](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/使用VSCode保留远程.2h8hdbd4eo.gif)

  - 保留本地库的内容 ——> 点击 `Accept Incoming Change`

![使用VSCode保留本地](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/使用VSCode保留本地.7axc9fxthr.gif)

  - 俩都保留 ——> 点击 `Accept Both Changes`

![使用VSCode保留远程和本地](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/使用VSCode保留远程和本地.45huai3ekx.gif)

## 7. 取消暂存

- 之前第 5 步是恢复工作进度；第 6 步是解决冲突；这一步是把现在还没完成的、还不想提交的内容取消 暂存 ，可选。
 - **现在应该已经可以 推送 了**

![6取消add](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/6取消add.5q7l9z0m0x.webp)

- 另外，我发现我的 changes 少了（应该是我这个项目的问题，我做 “从我的 Github 上 clone 下来的网站，用 npm start 出错” 这篇笔记的时候就没少）

![1先add](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/1先add.6t7aku3f6z.webp)

![6修改少了](https://github.com/Ratherthan17/picx-images-hosting/raw/master/ObsidainNotes/Computer/Git/Error/DueToRemoteUpdate/6修改少了.lvwkp0osj.webp)

---

[git pull和git fetch]: https://www.bilibili.com/video/BV1E3411c7cb/?spm_id_from=333.999.0.0&vd_source=4f65863adf19c12522e7026402e62e53

[Git工作流和核心原理]: https://www.bilibili.com/video/BV1r3411F7kn/?spm_id_from=333.1007.top_right_bar_window_custom_collection.content.click&vd_source=4f65863adf19c12522e7026402e62e53

[443 Operation timed out的解决办法]: https://juejin.cn/post/6844904193170341896