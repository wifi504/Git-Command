# 版本控制 Git ⭐️

Version Control Tools - Git

开源的、分布式、多分支、本地化的版本控制工具，本文将主要对git相关操作进行总结与归纳

![git-command.jpg](git-command.jpg)

## 1. Git 常用命令

> 以下将列举常用的所有命令，你可以点击小火箭[🚀](#1-Git-常用命令)快速前往该命令的详情位置。

### 1.1 设置常用操作

| 命令名称                                   | 作用                             |
| :----------------------------------------- | -------------------------------- |
| git config --global user.name `你的用户名` | 设置用户签名[🚀](#21-git-config) |
| git config --global user.email `你的邮箱`  | 设置用户签名[🚀](#21-git-config) |

- 签名的作用是**区分**不同操作者身份。
- 用户的签名信息在每一个版本的提交信息（commit）中能够看到，以此确认本次提交是谁做的。
- Git 首次安装必须设置一下用户签名，否则无法提交代码。
- 设置的用户签名和登录 GitHub（或其他代码托管中心）的账号没有任何关系。

### 1.2 仓库常用操作

| 命令名称                            | 作用                                                         |
| :---------------------------------- | :----------------------------------------------------------- |
| git init                            | 初始化本地库[🚀](#22-git-init)                               |
| git status                          | 查看本地库状态[🚀](#25-git-status)                           |
| git add `文件名`                    | 添加到暂存区[🚀](#24-git-add)                                |
| git rm --cached `文件名`            | 从暂存区移除[🚀](#29-git-rm)                                 |
| git commit -m "`日志信息`" `文件名` | 提交到本地库[🚀](#27-git-commit)                             |
| git reflog                          | 查看历史记录（版本）[🚀](#211-git-log-&-git-reflog)          |
| git log                             | 查看版本详细信息[🚀](#211-git-log-&-git-reflog)              |
| git reset --hard `版本号`           | 版本穿梭[🚀](#28-git-reset)                                  |
| git tag `标签名`                    | 为快照打上标签，常用标记版本（重要里程的commit）[🚀](#220-git-tag) |

### 1.3 分支常用操作

| 命令名称               | 作用                                            |
| :--------------------- | :---------------------------------------------- |
| git branch `分支名`    | 创建分支[🚀](#217-git-branch)                    |
| git branch -v          | 查看分支[🚀](#217-git-branch)                    |
| git checkout `分支名`  | 切换分支[🚀](#218-git-checkout)                  |
| git switch -c `分支名` | 切换分支（新）[🚀](#221-git-switch)              |
| git merge `分支名`     | 把指定的分支合并到当前分支上[🚀](#219-git-merge) |

### 1.4 上云常用操作

| 命令名称                         | 作用                                                         |
| :------------------------------- | :----------------------------------------------------------- |
| git remote -v                    | 查看当前所有远程地址别名[🚀](#213-git-remote-&-ssh)          |
| git remote add `别名` `远程地址` | 起别名，相当于定义常量存储地址[🚀](#213-git-remote-&-ssh)    |
| git push `地址` `分支`           | 推送本地分支上的内容到远程仓库，建议使用别名[🚀](#216-git-push) |
| git clone `地址`                 | 将远程仓库的内容克隆到本地[🚀](#23-git-clone)                |
| git pull `地址` `远程分支名`     | 将远程仓库对于分支最新内容拉下来后与当前本地分支直接合并，建议使用别名[🚀](#215-git-pull) |

## 2. 命令详情

### 2.1 git config

git config 工具，用来配置或读取相应的工作环境变量

| 命令                                               | 含义 / 作用                                         |
| :------------------------------------------------- | :-------------------------------------------------- |
| git config --list                                  | 检查（列举）已有的配置信息                          |
| git config user.name（即以下命令不追加参数的情况） | 查看对应的内容，此处为查看当前工作空间下用户名      |
| git config --global user.name 用户名               | 配置个人的用户名称                                  |
| git config --global user.email 邮箱                | 配置个人的邮件地址                                  |
| git config --global core.editor 编辑器名           | 设置Git默认使用的文本编辑器（Vim、Emacs……）         |
| git config --global merge.tool 工具名              | 设置Git默认使用的差异分析工具（vimdiff、ecmerge……） |


环境变量可以存放在以下三个不同的地方：

| 命令指定范围（选项名） | 含义                                         | 配置文件位置   |
| :--------------------- | -------------------------------------------- | :------------- |
| git config --system    | 系统中对所有用户都适用的配置（根配置）       | /etc/gitconfig |
| git config --global    | 用户目录下适用于该用户的配置（全局配置）     | ~/.gitconfig   |
| git config             | 工作目录中针对当前项目的配置（工作空间配置） | .git/config    |

配置文件有覆盖关系，就近原则，即：`工作空间配置 > 全局配置 > 根配置`

> 在 Windows 系统上，Git 会找寻用户**主目录**下的 .gitconfig 文件。主目录即 $HOME 变量指定的目录，一般都是 C:\Documents and Settings\$USER。
>
> 此外，Git 还会尝试找寻 /etc/gitconfig 文件，只不过看当初 Git 装在什么目录，就以此作为根目录来定位。

### 2.2 git init

- 使用当前目录作为 Git 仓库，我们只需使它初始化。

  ```shell
  git init
  ```

  该命令执行完后会在当前目录生成一个 .git 目录。

- 使用我们指定目录作为Git仓库。

  ```shell
  git init newrepo
  ```

  初始化后，会在 newrepo 目录下会出现一个名为 .git 的目录，所有 Git 需要的数据和资源都存放在这个目录中。

### 2.3 git clone

git clone 拷贝一个 Git 仓库到本地，让自己能够查看该项目，或者进行修改。

拷贝项目命令格式如下：

```shell
git clone [url]
```

`[url]` 是你要拷贝的项目。

### 2.4 git add

git add 命令可将该文件添加到暂存区。

- 添加一个或多个文件到暂存区：

  ```shell
  git add [file1] [file2] ...
  ```

- 添加指定目录到暂存区，包括子目录：

  ```shell
  git add [dir]
  ```

- 添加当前目录下的所有文件到暂存区：

  ```shell
  git add .
  ```

### 2.5 git status

- git status 命令用于查看在你上次提交之后是否有对文件进行再次修改。

  ```shell
  git status
  ```

- 通常我们使用 **-s** 参数来获得简短的输出结果：

  ```shell
  git status -s
  ```

### 2.6 git diff

git diff 命令比较文件的不同，即比较文件在**暂存区**和**工作区**的差异。

git diff 命令显示**已写入暂存区**和**已经被修改但尚未写入暂存区文件**的区别。

git diff 有两个主要的应用场景。

- 尚未缓存的改动：**git diff**
- 查看已缓存的改动： **git diff --cached**
- 查看已缓存的与未缓存的所有改动：**git diff HEAD**
- 显示摘要而非整个 diff：**git diff --stat**

显示暂存区和工作区的差异:

```shell
git diff [file]
```

显示暂存区和上一次提交(commit)的差异:

```shell
git diff --cached [file]
git diff --staged [file]
```

显示两次提交之间的差异:

```shell
git diff [first-branch]...[second-branch]
```

### 2.7 git commit

git commit 命令将暂存区内容添加到本地仓库中。

- 提交暂存区到本地仓库中:

  ```shell
  git commit -m [message]
  ```

  [message] 可以是一些备注信息。

- 提交暂存区的指定文件到仓库区：

  ```shell
  git commit [file1] [file2] ... -m [message]
  ```

- **-a** 参数设置修改文件后不需要执行 git add 命令，直接来提交

  ```shell
  git commit -a
  ```

> 注意，你需要有配置过用户信息才可以执行commit

### 2.8 git reset

git reset 命令用于回退版本，可以指定退回某一次提交的版本。

git reset 命令语法格式如下：

```shell
git reset [--soft | --mixed | --hard] [HEAD]
```

**--mixed** 为默认，可以不用带该参数，用于重置暂存区的文件与上一次的提交(commit)保持一致，工作区文件内容保持不变。

```shell
git reset [HEAD] 
```

实例：

```shell
git reset HEAD^					# 回退所有内容到上一个版本  
git reset HEAD^ hello.php		# 回退 hello.php 文件的版本到上一个版本  
git reset 052e					# 回退到指定版本
```

**--soft** 参数用于回退到某个版本：

```shell
git reset --soft HEAD
```

实例：

```shell
git reset --soft HEAD~3   # 回退上上上一个版本 
```

**--hard** 参数撤销工作区中所有未提交的修改内容，将暂存区与工作区都回到上一次版本，并删除之前的所有信息提交：

```shell
git reset --hard HEAD
```

实例：

```shell
git reset --hard HEAD~3			# 回退上上上一个版本  
git reset –hard bae128			# 回退到某个版本回退点之前的所有信息。 
git reset --hard origin/master	# 将本地的状态回退到和远程的一样 
```

### 2.9 git rm

git rm 命令用于删除文件。

如果只是简单地从工作目录中手工删除文件，运行 **git status** 时就会在 **Changes not staged for commit** 的提示。

git rm 删除文件有以下几种形式：

将文件从暂存区和工作区中删除：

```shell
git rm <file>
```

强行从暂存区和工作区中删除文件：

```shell
git rm -f <file>
```

如果想把文件从暂存区域移除，但仍然希望保留在当前工作目录中，换句话说，仅是从跟踪清单中删除，使用 **--cached** 选项即可：

```shell
git rm --cached <file>
```

### 2.10 git mv

git mv 命令用于移动或重命名一个文件、目录或软连接。

```shell
git mv [file] [newfile]
```

如果新文件名已经存在，但还是要重命名它，可以使用 **-f** 参数：

```shell
git mv -f [file] [newfile]
```

### 2.11 git log & git reflog

在使用 Git 提交了若干更新之后，又或者克隆了某个项目，想回顾下提交历史，我们可以使用 git log 命令查看。

```shell
git log
```

我们可以用 --oneline 选项来查看历史记录的简洁的版本。

```shell
git log --oneline
```

我们还可以用 --graph 选项，查看历史中什么时候出现了分支、合并。

```shell
git log --graph
```

你也可以用 --reverse 参数来逆向显示所有日志。

```shell
git log --reverse
```

如果只想查找指定用户的提交日志可以使用命令

```shell
git log --author 
```

查看历史记录（版本）的简要信息

```shell
git reflog
```

### 2.12 git blame

如果要查看指定文件的修改记录可以使用 git blame 命令，格式如下：

```shell
git blame <file>
```

### 2.13 git remote & ssh

git remote 命令用于在远程仓库的操作。

显示所有远程仓库：

```shell
git remote -v
```

显示某个远程仓库的信息：

```shell
git remote show [remote]
```

添加远程版本库：（shortname 为本地的版本库）

```shell
git remote add [shortname] [url]
```

删除远程仓库：

```shell
git remote rm name
```

修改仓库名：

```shell
git remote rename old_name new_name
```

涉及到远程仓库，我们经常会用到ssh免密登陆，生成ssh密钥的方式为

```shell
ssh-keygen -t rsa -C "youremail@example.com"
```

### 2.14 git fetch & git merge

git fetch 命令用于从远程获取代码库。

该命令执行完后需要执行 git merge 远程分支到你所在的分支。

从远端仓库提取数据并尝试合并到当前分支：

```shell
git merge
```

该命令就是在执行 git fetch 之后紧接着执行 git merge 远程分支到你所在的任意分支。

假设你配置好了一个远程仓库，并且你想要提取更新的数据，你可以首先执行:

```shell
git fetch [alias]
```

以上命令告诉 Git 去获取它有你没有的数据，然后你可以执行：

```shell
git merge [alias]/[branch]
```

### 2.15 git pull

git pull 命令用于从远程获取代码并合并本地的版本。

git pull 其实就是 git fetch 和 git merge FETCH_HEAD 的简写。

命令格式如下：

```shell
git pull <远程主机名> <远程分支名>:<本地分支名>
```

### 2.16 git push

git push 命令用于从将本地的分支版本上传到远程并合并。

命令格式如下：

```shell
git push <远程主机名> <本地分支名>:<远程分支名>
```

如果本地分支名与远程分支名相同，则可以省略冒号：

```shell
git push <远程主机名> <本地分支名>
```

### 2.17 git branch

创建分支命令

```shell
git branch (branchname)
```

没有参数时，git branch 会列出你在本地的分支。

```shell
git branch
```

删除分支命令：

```shell
git branch -d (branchname)
```

### 2.18 git checkout

切换分支命令:

```shell
git checkout (branchname)
```

### 2.19 git merge

合并分支命令:（此操作将把指向的分支合并到当前分支）

```shell
git merge (branchname)
```

这里，我们单独讲一下冲突合并

> 当前所在分支和要被合并的支线分支中的相同文件都发生更改时，会产生合并冲突
>
> 此时，需要手动把所有冲突都修改为正确状态
>
> 最后，执行 git commit ，完成合并分支

### 2.20 git tag

如果我们要查看所有标签可以使用以下命令：

```shell
git tag
```

创建带注解的标签，当你执行 git tag -a 命令时，Git 会打开你的编辑器，让你写一句标签注解，就像你给提交写注解一样。

```shell
git tag -a v1.0 
```

创建标签，指定注解

```shell
git tag -a <tagname> -m "<注解内容>"
```

为过去的快照追加标签（此处的85fc7e7需要替换你想打标记的快照版本号）

```shell
git tag -a <tagname> 85fc7e7
```

### 2.21 git switch

新版本中，可以使用以下命令切换分支

```shell
git switch <branchname>
```

如果想先创建新分支再切换，可以添加 **-c** 参数

```shell
git switch -c <branchname>
```

