## 本地Git

#### 刚安装Git需要做的

需要配置用户签名（用户名和邮箱），在提交的时候会连带这些信息一并提交，方便知道代码是由谁写的，以及追责。

***git config --global user.name*** 用户名

***git config --global user.email*** 邮箱

#### 初始化本地库

创建文件夹，右键选择Git Bash Here，在文件夹打开Git命令行窗口

***git init***  初始化本地库

初始化之后可以使用

***git status*** 查询本地库的状态

#### 新建文件，添加到暂存区

新建文件之后，查询本地库状态时会提示有哪些文件未被追踪，只有被追踪的文件才会加入到“工作区->暂存区->本地库”这一过程当中，Git才会去检测文件是否被修改。

对于未被追踪的文件可以通过

***git add 文件名***  来将文件添加到暂存区

此时文件已经到暂存区了，但是也可以通过以下命令从暂存区删除

***git restore --staged 文件名***

***git rm --cached 文件名***

#### 提交到本地库

对于已经添加到暂存区的文件，可以使用以下命令

***git commit -m "修改日志"***

***git commit -a -m "一次将所有修改过的文件提交本地库"***

#### 修改文件

对于修改过的文件，查看本地库状态时会有标注

需要先使用git add命令将文件添加到暂存区

然后使用提交命令将修改过的文件提交到本地库

<u>（对于已经提交到本体库过的文件，不git add直接git commit也没有问题，但是不推荐这么做）</u>

#### 查看日志

***git reflog 查看简洁版的日志***

***git log 查看详细的日志***

#### 版本穿梭

在开发过程中，我们有时候可能会需要返回到之前版本

可以使用git reflog或者是git log查询版本号

![](D:\Program%20Files\MarkText\images\2023-09-27-00-17-10-image.png)

前面有七位字母和数字（简化版，实际版本号更长）组成的版本号，然后使用以下命令

***git reset --hard 版本号***

来进行版本穿梭

![](D:\Program%20Files\MarkText\images\2023-09-27-00-25-02-image.png)

![](D:\Program%20Files\MarkText\images\2023-09-27-00-25-22-image.png)

#### 分支

在实际工作中，会有许多分支，如客户使用的线上分支，测试和开发人员使用的开发分支。同时推进多个任务时为每个任务单独创建一个分支。

程序员在可以把工作从主线上分离开来，开发自己的分支不会影响主线分支的运行，也可以理解为副本。

![](D:\Program%20Files\MarkText\images\2023-09-27-20-51-43-image.png)

**好处：** ①同时并行推进多个功能开发，提高开发效率；②某一个分支开发失败不会影响其它分支，这个分支推倒重来即可。

#### 分支的操作

***git branch 分支名***      创建分支

 ***git branch -v***             查看分支

***git checkout 分支名***     切换分支

***git merge 分支名***         把指定分支合并到当前分支

**创建分支** 

![](D:\Program%20Files\MarkText\images\2023-10-15-20-20-33-image.png)

**查看分支** 

![](D:\Program%20Files\MarkText\images\2023-10-15-20-21-05-image.png)

**切换分支** 

![](D:\Program%20Files\MarkText\images\2023-10-15-20-21-58-image.png)

**分支合并（正常合并）** 

在master下输入以下代码，即将hot-fix合并到master

![](D:\Program%20Files\MarkText\images\2023-10-15-20-37-44-image.png)

**分支合并（冲突合并）** 

当两个分支在**同一个文件同一个位置**有两套完全不同的修改，Git无法决定使用哪一个，必须认为决定新代码内容

对new.txt在master分支之下作出修改，并提交

![](D:\Program%20Files\MarkText\images\2023-10-15-21-07-14-image.png)

对new.txt在hot-fix分支之下作出修改，并提交

![](D:\Program%20Files\MarkText\images\2023-10-15-21-09-13-image.png)

在master下合并hot-fix分支

![](D:\Program%20Files\MarkText\images\2023-10-15-21-10-57-image.png)

如图，分支出现了冲突提示，master后面也有“MERGING（合并中）”的提示，需要手动修改new.txt

![](D:\Program%20Files\MarkText\images\2023-10-15-21-12-51-image.png)

![](D:\Program%20Files\MarkText\images\2023-10-15-21-13-56-image.png)

将new.txt提交到暂存区

![](D:\Program%20Files\MarkText\images\2023-10-15-21-15-54-image.png)

将new.txt提交到本地库（**注意后面不需要跟文件名**）

![](D:\Program%20Files\MarkText\images\2023-10-15-21-16-59-image.png)



## GitHub的使用

#### 团队内协作（简介）

**推送:**    本地库-----push----->远程库

**克隆：** 远程库-----clone----->本地库

**拉取：** 远程库-----pull----->本地库

***git clone*** 用于新建一个本地库并将远程库的代码克隆到本地

***git pull*** 已有本地库，用于将远程库的最新更改同步到本地库

***git fetch*** 只是获取远程库上的更改信息，并不影响当前工作分支



#### 跨团队协作（简介）

远程库1-----fork----->远程库2

远程库1<-----merge<-----审核<-----Pull request<-----远程库2



#### 别名操作

***git remote -v*** 查看所有远程地址的别名

![](D:\Program%20Files\MarkText\images\2023-10-22-15-24-57-image.png)

***git remote add 别名 远程地址***  为远程地址设置好别名

![](D:\Program%20Files\MarkText\images\2023-10-22-15-25-44-image.png)



#### 推送到远程库

***git push 别名/URL 分支***  把指定分支推送到远程库

第一次push可能会需要登录GitHub账号

![](D:\Program%20Files\MarkText\images\2023-10-22-15-39-08-image.png)

![](D:\Program%20Files\MarkText\images\2023-10-22-15-50-18-image.png)



#### 从远程库拉取

***git pull 别名/URL 分支***  把指定分支从远程库拉取过来

![](D:\Program%20Files\MarkText\images\2023-10-22-16-02-58-image.png)



#### 从远程库克隆

***git clone URL*** 从远程库克隆到本地

![](D:\Program%20Files\MarkText\images\2023-10-22-16-15-55-image.png)
