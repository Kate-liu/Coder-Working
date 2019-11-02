# 工具|浅谈Git
*Git这个工具，是我一直想写文章，终于我实现了我的想法。在我开始写之前，发表一下自己的看法，git只是一个工具，既然已经认定是一个工具，那么一定具备工具这类的共同特征，请用面向对象的鸭子类型去理解就好~~*

## 前言
    目前所有的文章思想格式都是:知识+情感。
    知识:对于所有的知识点的描述。力求不含任何的自我感情色彩。
    情感:用我自己的方式，解读知识点。力求通俗易懂，完美透析知识。

## 目录
    1.Git介绍
    2.Git下载安装
    3.Git的基本使用
       3.1 小结git基本使用
    4.Git的高级使用
        4.1.Github使用
        4.2.Git分支使用
    5.Git总结
    
## 正文
**正文内容包含，下载与安装git，并且用实际的操作介绍Git的基本使用，与高级使用，会在高级部分涉及git 与github 的交互使用。**

### Git介绍
**Git做版本控制**，还有很多其他的工具也可以实现，如**SVN， 码云**等。
版本控制分为本地和远程，**git与github**可以实现很好的版本控制，并且在实际的使用中，可能还会出现**gitlab与jenkins**，都是做持续集成的工具，记住了啊，**只是工具**。



### Git下载安装
1.**官网:**https://git-scm.com/downloads
*下载自己需要的版本即可，安装也是最常见的软件安装，问题不大的~~*
**注意:**所有的软件，只要是不收费的，都在官网上下载哦!~

2,关于**git的参考book**(全英，非诚勿扰~)
https://git-scm.com/book/en/v2


### Git的基本使用
1，**打开git Bash，鼠标右键，看图操作**
图1

此时会打开一个新窗口，看下图，比window的powershell漂亮一百倍，有没有~~~关键，直接可以使用Linux的命令，就说，老铁服不服~
图2


2，**查看git版本命令**
*此时差评，在命令行不可以直接选中点击进行选中复制......(ipython的交互是可以实现的，想体验的大家可以是一个ipython的命令行交互。)*
```s
Administrator@kate_liu MINGW64 ~/Desktop
$ git --version
git version 2.22.0.windows.1

```

3.**查看帮助文档命令**
*我觉得，我想写的内容全部都被帮助文档写了，哈哈哈~~*
**注意**:使用工具，尤其是陌生的工具，一开始就是先看版本，再看帮助消息，不然一上来就可以操作猛如虎？？？
```s
Administrator@kate_liu MINGW64 ~/Desktop
$ git --help
usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone      Clone a repository into a new directory
   init       Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add        Add file contents to the index
   mv         Move or rename a file, a directory, or a symlink
   reset      Reset current HEAD to the specified state
   rm         Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect     Use binary search to find the commit that introduced a bug
   grep       Print lines matching a pattern
   log        Show commit logs
   show       Show various types of objects
   status     Show the working tree status

grow, mark and tweak your common history
   branch     List, create, or delete branches
   checkout   Switch branches or restore working tree files
   commit     Record changes to the repository
   diff       Show changes between commits, commit and working tree, etc
   merge      Join two or more development histories together
   rebase     Reapply commits on top of another base tip
   tag        Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch      Download objects and refs from another repository
   pull       Fetch from and integrate with another repository or a local branch
   push       Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.

```

4.按照说明文档，现在需要开始**进行初始化**了，好了，那就找个空白文件夹试试吧!
1)新建文件夹-------test_git
2)将命令行切到新建文件夹中------linux的切目录知识，cd test_git 
3)执行命令:git init
4)查看文件夹下的隐藏文件夹，一个 .git的文件，还可以进去看看哈，看下面命令
```s
Administrator@kate_liu MINGW64 ~/Desktop
$ cd test_git/
Administrator@kate_liu MINGW64 ~/Desktop/test_git
$ git init
Initialized empty Git repository in C:/Users/Administrator/Desktop/test_git/.git/
Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ cd ./.git/
Administrator@kate_liu MINGW64 ~/Desktop/test_git/.git (GIT_DIR!) 
$ ls
config  description  HEAD  hooks/  info/  objects/  refs/

```

5.当前文件新建文件 : a.py 。执行命令add，将**当前目录文件添加到暂存区**。
```s
Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ touch a.py
Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ ls
a.py
Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ git add a.py
```

6.查看当前git**工作区的状态，status**
```s
Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   a.py

```

7.可以继续创建文件，例如:b.txt, c.md等等，查看当前工作区的状态，并且添加到暂存区，此时可以在**add后面使用 . ，表示全部的当前文件。**
```s
Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   a.py

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        b.txt
        c.md
Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ git add .

Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   a.py
        new file:   b.txt
        new file:   c.md
```


8.将暂存区的文件，**提交到git版本库，使用 commit -m.**并查看当前git工作区status。
**注意:**这里可能会出现错误，也就是提交失败，git需要知道是谁在提交，所以此时按照git的提示消息，自己设置自己的用户名与邮箱哈~~(我之前已经搞过了，大家自己在这里可以百度一下哈~，配置结束，可以使用 **cat config 查看自己当前配置的用户信息**这里还可以使用--global  设置全局额用户信息。。)
```s
Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ git commit -m 'First commit code ..'
[master (root-commit) 7008e7d] First commit code ..
 3 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 a.py
 create mode 100644 b.txt
 create mode 100644 c.md

Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ git status
On branch master
nothing to commit, working tree clean
```

9.此时可以继续创建几个文件，或者修改文件的内容，**重复 add 与 commit提交。**
```s
Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ echo hello git! >> b.txt

Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ cat b.txt
hello git!

Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ touch d.doc

Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ git add .
warning: LF will be replaced by CRLF in b.txt.
The file will have its original line endings in your working directory

Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ git commit -m 'Create new file d.doc and modify b.txt.'
[master 2dc8bcb] Create new file d.doc and modify b.txt.
 2 files changed, 1 insertion(+)
 create mode 100644 d.doc

Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ git status
On branch master
nothing to commit, working tree clean

```

10.查看**已经提交的日志，使用log命令**
```s
Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ git log
commit 2dc8bcb9dc11aa2ffb972302cd0748398f9747a8 (HEAD -> master)
Author: Administrator <2XXXXXXXXX9@qq.com>
Date:   Mon Jul 22 22:02:59 2019 +0800

    Create new file d.doc and modify b.txt.

commit 7008e7dd988b505063e94e45af68e8a4c9c1845a
Author: Administrator <2XXXXXXXXX9@qq.com>
Date:   Mon Jul 22 21:58:24 2019 +0800

    First commit code ..

```

11.使用**reset命令，进行版本的回滚**，直接会到之前，来试一下哈!~~此时，已经看不到自己刚刚创建的文件了，然后看一下修改的文件，也没见了。。。。。。(还好是自己在玩，要是自己写的代码，就挂了吗？？不会的，还可以滚回去的)
```python
Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ git reset --hard 7008e7dd988
HEAD is now at 7008e7d First commit code ..
Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ ls
a.py  b.txt  c.md

Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ cat b.txt
```

12.继续回滚到创新文件与修改文件的时候，先使用**reflog查看所有的日志**，此时是可以看到所有的git对于本地数据仓库的操作日志，但是log只可以看到当前版本的日志，是不全的。
```s
Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ git reflog
7008e7d (HEAD -> master) HEAD@{0}: reset: moving to 7008e7dd988
2dc8bcb HEAD@{1}: commit: Create new file d.doc and modify b.txt.
7008e7d (HEAD -> master) HEAD@{2}: commit (initial): First commit code ..

Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ git reset --hard 2dc8bcb
HEAD is now at 2dc8bcb Create new file d.doc and modify b.txt.

Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ ls
a.py  b.txt  c.md  d.doc

Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ cat b.txt
hello git!

```

#### 小结git基本使用
git的基本使用，从初始化出发，到提交代码到暂存区，再从暂存区提交到本地版本区，并且进行自己版本的回滚，可以随时查看工作目录的状态，查看提交日志。
必须，一定，需要记住的命令:

    git init
    git status
    git add .
    git commit -m 'information'
    git log
    git reser --hard 'back code'
    git reflog

此时，大家可以看看版本控制中，工作区与暂存区与版本区的交互图了，看下图。
图3


### Git的高级使用
结束了git的基本使用之后，在高级使用中就需要进行远程了，所以此时需要自己先去看下github是个啥~~~
**注意**:github官网:https://github.com/

#### Github使用
1.登录github寻找一个目标项目进行本地克隆，

2.创建新仓库--New repository，填写 Repository name and  Description， then Create repository。

3.复制当前仓库对应的https链接，在本地执行 git remote add  origin https://github.com/Kate-liu/2109git.git ，此时就将远程的仓库地址**添加到了oringin **，现在就可以**进行 git push **，将本地版本区的数据远程到github。看下面。
**会弹出ssh验证，输入自己的github用户名与密码就好。**
**注意:** 创建好的仓库下面就已经写好的基本的命令，直接copy就可以~
```s
Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ git remote add  origin https://github.com/Kate-liu/2109git.git
Administrator@kate_liu MINGW64 ~/Desktop/test_git (master)
$ git push -u origin master
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 6 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 473 bytes | 473.00 KiB/s, done.
Total 6 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/Kate-liu/2109git.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

4.自己在**github官网上查看自己的当前代码仓库**，看下是不是已经出现了本地的多个文件，还可以看下文件内容，这还不是关键，直接在github上就可以查看branch等。

5.现在需要掌握将远程的代码，**拉到本地，使用clone命令**。新建新文件夹，new_git_test，切git命令行进入新的文件中，执行命令 git clone https://github.com/Kate-liu/2109git.git，稍等片刻就可以看到自己的远程的代码仓库直接被拖下来了~~
```s
Administrator@kate_liu MINGW64 ~/Desktop
$ mkdir new_git_test

Administrator@kate_liu MINGW64 ~/Desktop
$ cd new_git_test/

Administrator@kate_liu MINGW64 ~/Desktop/new_git_test
$ ls

Administrator@kate_liu MINGW64 ~/Desktop/new_git_test
$ git clone https://github.com/Kate-liu/2109git.git
Cloning into '2109git'...
remote: Enumerating objects: 6, done.
remote: Counting objects: 100% (6/6), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 6 (delta 1), reused 6 (delta 1), pack-reused 0
Unpacking objects: 100% (6/6), done.

Administrator@kate_liu MINGW64 ~/Desktop/new_git_test
$ ls
2109git/

Administrator@kate_liu MINGW64 ~/Desktop/new_git_test
$ cd 2109git/

Administrator@kate_liu MINGW64 ~/Desktop/new_git_test/2109git (master)
$ ls
a.py  b.txt  c.md  d.doc

```

6.好了，截止到现在，按照我的文档已经可以完成代码的托管，并且可以与github进行远程操作了。接下来我们一起来看看，到底在实际环境下的操作，可能表述不够详细，但是我会尽量~~

7.在自己进行clone的时候，还有**另一种思路可以实现拉代码到本地**，请向下面看:
1)在自己的本地先进行初始化: git init
2)添加远程仓库地址: git remote add origin heep://xxxxx
3)将远程代码，pull下来，使用: git pull origin master 
```s
Administrator@kate_liu MINGW64 ~/Desktop
$ mkdir pull_test

Administrator@kate_liu MINGW64 ~/Desktop
$ cd pull_test/

Administrator@kate_liu MINGW64 ~/Desktop/pull_test
$ git init
Initialized empty Git repository in C:/Users/Administrator/Desktop/pull_test/.git/

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (master)
$ git remote add origin https://github.com/Kate-liu/2109git.git

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (master)
$ git pull origin master
remote: Enumerating objects: 6, done.
remote: Counting objects: 100% (6/6), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 6 (delta 1), reused 6 (delta 1), pack-reused 0
Unpacking objects: 100% (6/6), done.
From https://github.com/Kate-liu/2109git
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> origin/master

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (master)
$ ls
a.py  b.txt  c.md  d.doc

```



#### Git分支使用
git的分支才是git使用中最需要关心的，尤其是最后的分支合并，啊哈~merge，你懂得!~
1.创建分支，先找到自己之前的代码，就用之前另一种思路可以实现拉代码到本地的那个文件夹，pull_test 文件存储地。**创建分支，git branch dev**， 创建dev分支，并**使用git branch 查看分支.** 
```s
Administrator@kate_liu MINGW64 ~/Desktop
$ cd pull_test/

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (master)
$ ls
a.py  b.txt  c.md  d.doc

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (master)
$ git branch dev

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (master)
$ git branch
  dev
* master

```

2.切换分支，此时的项目文件在master分支上，可以切换dev分支上，使用**git checkout dev ，切换分支。**
```s
Administrator@kate_liu MINGW64 ~/Desktop/pull_test (master)
$ git checkout dev
Switched to branch 'dev'

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ git branch
* dev
  master

```

3.此时可以在dev分支上，**创建文件 dev.py , dev.md ,**并且添加到暂存区，提交到本地的管理区。
```s
Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ touch dev.py

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ touch dev.md

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ ls
a.py  b.txt  c.md  d.doc  dev.md  dev.py

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ git add .

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ git commit -m 'dev branch create new file.'
[dev 1e7930f] dev branch create new file.
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 dev.md
 create mode 100644 dev.py

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ git status
On branch dev
nothing to commit, working tree clean

```

4.提交dev分支到远程的github上，还记得不，直接使用** git push origin dev **就可以，需要验证自己的身份信息，输入即可。此时可以登录github，查看自己刚刚创建的内容，并且可以查看dev分支下有自己刚刚创建的文件，但是在master分支下面没有自己刚刚创建的文件夹，这就说明了分支的重要性。
```s
Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ git push origin dev
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 6 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 269 bytes | 269.00 KiB/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/Kate-liu/2109git.git
 * [new branch]      dev -> dev

```

5.此时，在dev分支上，对文件的数据，进行更改，**更改dev.md的内容，并提交到github上**。
```s
Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ echo I am dev test code! >> dev.md

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ cat dev.md
I am dev test code!

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ git status
On branch dev
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   dev.md

no changes added to commit (use "git add" and/or "git commit -a")

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ git add dev.md
warning: LF will be replaced by CRLF in dev.md.
The file will have its original line endings in your working directory

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ git commit -m  'modify dev.py content.'
[dev ec34b39] modify dev.py content.
 1 file changed, 1 insertion(+)

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ git status
On branch dev
nothing to commit, working tree clean

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ git push origin dev
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 6 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 284 bytes | 284.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/Kate-liu/2109git.git
   1e7930f..ec34b39  dev -> dev


```

6.此时应该已经熟练提交代码到github上了，现在需要做一件事，那就是**分支的 合并**。将分支却换到master上，并且执行** git merge dev。**此时就完成了自己的dev的内容合并到自己的master分支上，将内容推导github上看看。
```s
Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ git checkout master
Switched to branch 'master'

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (master)
$ git status
On branch master
nothing to commit, working tree clean

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (master)
$ git merge dev
Updating 2dc8bcb..ec34b39
Fast-forward
 dev.md | 1 +
 dev.py | 0
 2 files changed, 1 insertion(+)
 create mode 100644 dev.md
 create mode 100644 dev.py

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (master)
$ ls
a.py  b.txt  c.md  d.doc  dev.md  dev.py

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (master)
$ git push origin master
Total 0 (delta 0), reused 0 (delta 0)
To https://github.com/Kate-liu/2109git.git
   2dc8bcb..ec34b39  master -> master

```

7.此时，我觉得大家对于代码的推送啥的，都应该很熟悉了，并且此时我们的本地与远程github上的内容都是一样的了，并且dev分支与master分支的内容也已经合并了，好了现在**开始新的挑战。**
1)切换分支到dev
2)修改dev.md文件 与 c.md 文件的内容
3)将内容提交到本地，并同步到github上。
```s
Administrator@kate_liu MINGW64 ~/Desktop/pull_test (master)
$ git checkout dev
Switched to branch 'dev'

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ ls
a.py  b.txt  c.md  d.doc  dev.md  dev.py

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ echo new code for dev branch. >> c.md

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ echo new code for dev branch.6666 >> dev.md

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ cat dev.md
I am dev test code!
new code for dev branch.6666

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ cat c.md
new code for dev branch.

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ git status
On branch dev
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   c.md
        modified:   dev.md

no changes added to commit (use "git add" and/or "git commit -a")

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ git add .
warning: LF will be replaced by CRLF in c.md.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in dev.md.
The file will have its original line endings in your working directory

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ git status
On branch dev
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   c.md
        modified:   dev.md


Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ git commit -m 'modefy new code for c.md and dev.md'
[dev 97eda8a] modefy new code for c.md and dev.md
 2 files changed, 2 insertions(+)

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ git status
On branch dev
nothing to commit, working tree clean

Administrator@kate_liu MINGW64 ~/Desktop/pull_test (dev)
$ git push origin dev
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 6 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (4/4), 372 bytes | 372.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/Kate-liu/2109git.git
   ec34b39..97eda8a  dev -> dev

```

8.此时需要合并dev分支到master分支。
1)切换到master分支
2)修改c.md的值，并且提交到github上
3)合并分支，git merge dev，报错了----看下面---CONFLICT (content)
```s
Administrator@kate_liu MINGW64 ~/Desktop/pull_test (master)
$ git merge dev
Auto-merging c.md
CONFLICT (content): Merge conflict in c.md
Automatic merge failed; fix conflicts and then commit the result.

```


9.根据错误信息，自己手动打开c.md文件，进行解决文件冲突
c.md的内容是这样子的，看下面====需要自己选择留下哪一个，手动解决merge冲突。修改完毕继续进行提交到本地，并同步到github即可。
```s
<<<<<<< HEAD
I am master new modefy infomation.
=======
new code for dev branch.
>>>>>>> dev
~

```

10.此时我们**已经完成了分支的合并时出现冲突的问题**，并且通过手动合并解决问题，此时所有的分支与代码全部都可以在github上看到，并且dev分支与master分支的数据都一样。

### Git总结
*原本，已经不打算写这一部分的内容了，但是呢，为了让我自己可以更好地回看整个操作的流程，我决定将整个流程顺一遍!*

**Git总结会将所有的git命令全部列出来一份，如果以后被用到，可以方便查看。**

    git --vertion
    git --help
    git init 
    git config user.name 你的用户名
    git config user.email 你的邮箱
    git config --global user.name 你的用户名
    git config --global user.email 你的邮箱
    git status 
    git add 文件名
    git add .
    git rm --cached 文件名  # 将提交到暂存区的文件状态删除，不删除本地文件
    git rm -f 文件名   # 直接将暂存区的文件状态与本地文件直接删除
    git mv  原文件名 新文件名  # 暂存区的文件重命名
    mv 原文件名 新文件名  # 工作区的文件重命名
    git commit -m '提交的描述信息'
    git log
    git git log --pretty=oneline  # 一行展示日志信息
    git log --oneline
    git reflog  # 查看每一次版本记录历史
    git reset --hard 日志记录提交的hash值
    git reset --hard HEAD^  # 版本回退一次
    git reset --hard HEAD^^  # 版本回退两次
    git reset --hard HEAD ~n  # 版本回退n次
    git diff 文件名     #  工作目录与暂存区比较文件的差异
    git diff --cached   #  比较暂存区与版本区非区别
    
    git remote -v   # 查看当前远程地址的别名
    git remote add 别名 地址  #添加远程地址与别名
    git push -u 别名 分支    # 第一次推送
    git push 别名 分支   # 更新之后的推送
    git pull 别名 分支  # 相当于先fetch 分支，在merge或者rebase分支
    git clone 仓库地址  # 直接将整个仓库克隆下来
    git branch   # 查看所有分支
    git branch -v  # 查看所有分支与上次commit的信息
    git branch -b 分支  # 相当于创建分支并且切换到分支上
    git branch -D  # 强行删除没有合并到master分支的branch
    git ranch 新分支名   # 创建新分支 
    git checkout 分支名   # 切换分支
    git checkout -b 分支名   # 切换分支
    git checkout -d 分支名   # 删除分支
    git merge 分支名  # 合并分支
    版本冲突: 手动修改，重新提交
    git rebase 分支名  # 合并分支，并且将记录合并到一条主线上，保证提交记录整洁
    版本冲突: 手动修改，git rebase --skip
    
    git stash # 将当前的工作状态保存修改bug
    git stash list  # 查看保存的列表
    git stash apply stash@{n}  # 恢复到之前的n时刻的状态，不删除保存列表
    git stash drop  #  删除保存的数据
    git pop #  恢复到之前的状态，删除保存列表
    
    git tag 标签名   # 创建标签名
    git tag  # 查看标签名字
    git tag 标签名 提交的hash  # 为某一次提交指定标签
    git show 标签名  # 查看标签的详细信息
    git tag -a 标签名 -m '描述信息' 提交的hash  # 添加描述信息
    git tag -d 标签名  # 删除标签
    git push origin 标签名  # 推送标签到远程
    git push origin --tags  # 推送所有标签到远程
    git push origin :refs/tags/标签名   # 删除远程库标签
    
    git log --graph --pretty=oneline --abbrev-commit  # 分支合并缩略图
    git log --graph  # 分支合并图
    
    忽略某些文件，编写.gitignore文件，配置文件参考：https://github.com/github/gitignore
    fork: fork代码到本地之后，可以修改代码，之后创建pull request
    实际开发中: master分支是线上代码分支，dev是开发分支，review分支(代码的review)，每一个人有自己的开发分支，bug分支(专门处理mater分支的bug.)
    

## 结束语
**终于，整理完了git的使用，大概说一下自己的新路历程，一开始很不想整理，因为一旦开始就会被迫着自己回忆很多东西，需要重新捡起来一些东西，当整理到一半的时候，这个东西我不清楚了，是不是需要自己回去过查看啊！!!然而自己确实还是有点懒了!但是最后还是硬着头皮干出来!**
*当然这篇文，还是不是很完整，但是对于git入门到熟练已经完全够了，希望大家阅读愉快~~~此乃深度长文，哈~*







