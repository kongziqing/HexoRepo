---
title: git基本操作
author: ziqing
top: true
cover: true
toc: false
mathjax: false
summary: 这是你自定义的文章摘要内容，如果这个属性有值，文章卡片摘要就显示这段文字，否则程序会自动截取文章的部分内容作为摘要
categories: 分类
tags:
  - Typora
  - 标签
date: 2020-03-27 23:26:25
img:
coverImg:
password:
---
# ==git基本操作==
```
(1)创建版本仓库

git init 获得 .git目录


(2)版本创建
1.git add 文件或目录
2.git commit -m '版本说明信息'


(3)查看版本记录
git log


(4)版本回退
git reset --hard HEAD //HEAD指向当前版本
git reset --hard 版本序列号


(5)查看操作记录
git reflog


(6)工作区、版本库和暂存区
git add是把工作区的修改放入暂存区
git commit是把暂存区的修改一次性做一次版本记录


(7)管理修改
git commit 只会把暂存区的修改提交到版本记录中


(8)撤销修改
1、直接丢弃工作区的改动
git checkout -- 文件
2、修改已经加到暂存区，但未commit
a.git reset HEAD 文件
b.git checkout -- 文件
3、已经commit
则必须版本回退


(9)对比文件的不同
对比工作区和版本库某个文件
git diff HEAD -- 文件
对比两个版本中的文件
git diff HEAD HEAD^ -- code.txt
 

(10)删除文件
rm 文件
git rm 文件
git commit
```


注意：：：删除文件补充
```python 
若直接
vi code3.txt
rm code3.txt
它没有被add到暂存区，git是无法跟踪这个文件的。删除了之后只能由硬盘扫描器搜索出来，没有其他方法。一般这种软件是收费的
```








## Git版本创建
```
创建 版本1 及 版本2
$ vi code.txt
$ git add code.txt
$ git commit -m '版本1'

$ vi code.txt
$ git add code.txt
$ git commit -m '版本2'

查看版本
$ git log
```

## 版本回退
```
(1)
若想回到某一个版本，可以使用如下命令：
$git reset -- hard HEAD^
其中HEAD表示当前最新版本，HEAD^表示当前版本的前一个版本，HEAD^^表示当前版本的前前个版本，
也可以使用HEAD~1 表示当前版本的前一个版本，
HEAD~100表示当前版本的前100版本


(2)假如我们现在又想回到版本2，这个时候怎么办
可以使用命令：
git reset --hard 版本号
这里注意版本号很长，只需要复制前几个数字即可
没有必要全部复制


(3)假如终端关闭，看不到版本号，该如何回退版本

通过

git reflog

命令查看我们的操作记录

***注意此处要将位置cd到仓库的地址才可以查看
392893e (HEAD -> master) HEAD@{0}: reset: moving to HEAD^
a4d2662 HEAD@{1}: reset: moving to a4d2662fc6078
392893e (HEAD -> master) HEAD@{2}: reset: moving to HEAD^
a4d2662 HEAD@{3}: commit: 版本2
392893e (HEAD -> master) HEAD@{4}: commit (initial): 版本1

我们可以看到命令行最前面的就是我们所需要的版本号

$ git reset --hard a4d2662==
即可回退版本


(4) 孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ vi code2.txt


孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ cat code2.txt
the code2 fist line


孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git status
On branch master
Your branch is based on 'origin/master', but the upstream is gone.
  (use "git branch --unset-upstream" to fixup)

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        code2.txt

nothing added to commit but untracked files present (use "git add" to track)

此处需要注意，我们创建了code2.txt，但是没有将其git add 暂存区，所以git会提醒我们将其添加到暂存区。


(5)注意，当提交了新的版本，工作区便无文件要提交，此时提示工作区为干净的
孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git commit  -m '版本3'
[master a605c0d] 版本3
 1 file changed, 1 insertion(+)
 create mode 100644 code2.txt

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git status
On branch master
Your branch is based on 'origin/master', but the upstream is gone.
  (use "git branch --unset-upstream" to fixup)

nothing to commit, working tree clean
```

## 管理修改
```
git管理的文件修改，它只会提交暂存区的修改来创建版本。
若未把修改添加到暂存区，则创建版本仍为上一次添加到暂存区的修改。
```

## 撤销修改
```
未将修改添加到暂存区之前，撤销修改只需要输入git checkout -- code.txt即可

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ cat code.txt
this is the first
this is the second
this is the third line
this is the forth line

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git checkout -- code.txt

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ cat code.txt
this is the first
this is the second
this is the third line


若修改已经被添加到暂存区，则需要先键入git reset HEAD code.txt
再键入git checkout -- code.txt

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ vi code.txt

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ cat code.txt
this is the first
this is the second
this is the third line
this is the newest line

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git add code.txt

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git status
On branch master
Your branch is based on 'origin/master', but the upstream is gone.
  (use "git branch --unset-upstream" to fixup)

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   code.txt



孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git reset HEAD code.txt
Unstaged changes after reset:
M       code.txt
孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git checkout -- code.txt

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ cat code.txt
this is the first
this is the second
this is the third line


孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git status
On branch master
Your branch is based on 'origin/master', but the upstream is gone.
  (use "git branch --unset-upstream" to fixup)

nothing to commit, working tree clean
```

### 小结
```
场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，
用命令git checkout -- file
场景2：当你不但该乱了工作区某个文件的内容，还添加到了暂存区，想丢弃修改，分两步，第一步用命令git reset HEAD file。就回到了场景1，第二部按场景1操作。
场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节。
```
### 对比文件的不同
```
对比工作区和某个版本中文件的不同：
(1)继续编辑文件code.txt，在其中添加一行内容。
加入一行 new line


(2)现在要对比工作区中code.txt和HEAD版本中code.txt的不同，使用如下命令git diff HEAD -- code.txt


孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git diff HEAD -- code.txt
diff --git a/code.txt b/code.txt
index 02ba9de..3979941 100644
--- a/code.txt
+++ b/code.txt // -代表HEAD版本中code.txt的内容，+代表工作区code.txt的内容
@@ -1,3 +1,4 @@
 this is the first
 this is the second
 this is the third line
+new line //此处表示工作区的code.txt比版本中的多了一行new line
```


### 对比两个版本间文件的不同
```
(1) 现在要对比HEAD和HEAD^两个版本中code.txt的不同，使用如下命令：
git diff HEAD HEAD^ -- code.txt，同时git diff HEAD^ HEAD -- code.txt
的位置不同，对应的结果也不同

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$git diff HEAD HEAD^ -- code.txt
diff --git a/code.txt b/code.txt
index 02ba9de..99ec16a 100644
--- a/code.txt
+++ b/code.txt
@@ -1,3 +1,2 @@
 this is the first
 this is the second
-this is the third line//此处为减号

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git diff HEAD^ HEAD -- code.txt
diff --git a/code.txt b/code.txt
index 99ec16a..02ba9de 100644
--- a/code.txt
+++ b/code.txt
@@ -1,2 +1,3 @@
 this is the first
 this is the second
+this is the third line//此处为加号
```

## 删除文件
```
(1)我们把目录中的code2.txt删除
输入命令 rm code2.txt
孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ ls
code.txt  code2.txt

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ rm code2.txt

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ ls
code.txt

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git status
On branch master
Your branch is based on 'origin/master', but the upstream is gone.
  (use "git branch --unset-upstream" to fixup)

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    code2.txt

no changes added to commit (use "git add" and/or "git commit -a")


这个时候，git直到了删除了文件，因此，工作区和版本库就不一样了。git status 命令会立刻提示哪些文件被删除了。

若又不想删除这个文件，该如何撤回呢？可以输入命令
git checkout -- code2.txt


孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ ls
code.txt
孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git checkout -- code2.txt

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ ls
code.txt  code2.txt


(2) 现在你有两种选择，一是确实要从版本库中删除该文件，那就用命令git rm删除，并且git commit

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git rm code2.txt
rm 'code2.txt'

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git status
On branch master
Your branch is based on 'origin/master', but the upstream is gone.
  (use "git branch --unset-upstream" to fixup)

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    code2.txt


孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git commit -m '删除文件code2.txt'
[master 958ef15] 删除文件code2.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 code2.txt

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git status
On branch master
Your branch is based on 'origin/master', but the upstream is gone.
  (use "git branch --unset-upstream" to fixup)

nothing to commit, working tree clean



这个时候查看版本git log

孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git log
commit 958ef1549fdebbf5a4b40c22db3836df4a3cda64 (HEAD -> master)
Author: kongziqing <406805342@qq.com>
Date:   Fri Aug 9 21:08:16 2019 +0800

    删除文件code2.txt

commit 8d52c7db2b1e155c6953d1064d090e45aa6eae98
Author: kongziqing <406805342@qq.com>
Date:   Fri Aug 9 18:09:51 2019 +0800

    版本4

commit a605c0de5ba1ece3dd8fe2072090e6d08f00ca6f
Author: kongziqing <406805342@qq.com>
Date:   Fri Aug 9 17:46:10 2019 +0800
:   //你会发现最下方有一个冒号，这是因为版本记录过长，直接向下翻即可
退出按q即可
那版本记录过长，可以输入git log --pretty=oneline简短显示
孔子@DESKTOP-SV0VDD2 MINGW64 /d/shiyanlou/Git- (master)
$ git log --pretty=oneline
958ef1549fdebbf5a4b40c22db3836df4a3cda64 (HEAD -> master) 删除文件code2.txt
8d52c7db2b1e155c6953d1064d090e45aa6eae98 版本4
a605c0de5ba1ece3dd8fe2072090e6d08f00ca6f 版本3
a4d2662fc607848295c3663497c3e1fd05584923 版本2
392893e5126f8f9fdf22ca2171ead54ddef28f2d 版本1



```


### 小结
```
命令git rm用于删除一个文件，如果一个文件已经被提交到版本库，那么你句永远不用担心误删，但是要小心，你只能回复文件到最新版本，你会丢失最近一次提交后你修改的内容。
```
