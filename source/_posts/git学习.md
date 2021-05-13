---
title: git学习
author: 汉娜
tags: git
categories: git
date: 2021-05-13 14:42:23
---

参考文档：

1、[廖雪峰Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)

Git是目前世界上最先进的分布式版本控制系统（没有之一）。

#### git init
能把当前目录变成git可以管理的仓库，会多一个隐藏的.git目录，来跟踪管理版本库，ls -ah就能看到。
```
git init
```


#### git status
可以让我们时刻掌握仓库当前的状态。
```
$ git status
On branch hexo
Your branch is up to date with 'origin/hexo'.

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   "source/_posts/turtle\347\273\230\345\210\266\345\215\241\346\257\224.md"
        modified:   "source/_posts/\346\233\264\346\215\242\347\224\265\350\204\221\346\233\264\346\226\260\345\215\232\345\256\242\346\223\215\344\275\234.md"
        deleted:    source/images/kirby.png

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        "source/_posts/git\345\255\246\344\271\240.md"
        source/images/kirby.jpg

no changes added to commit (use "git add" and/or "git commit -a")
```


#### git diff
可以查看修改。
```
warning: LF will be replaced by CRLF in source/_posts/turtle绘制卡比.md.
The file will have its original line endings in your working directory
diff --git "a/source/_posts/turtle\347\273\230\345\210\266\345\215\241\346\257\224.md" "b/source/_posts/turtle\347\273\230\345\210\266\345\215\241\346\257\224.md"
index c87a273..d23db65 100644
--- "a/source/_posts/turtle\347\273\230\345\210\266\345\215\241\346\257\224.md"
+++ "b/source/_posts/turtle\347\273\230\345\210\266\345\215\241\346\257\224.md"
@@ -58,5 +58,5 @@ pip3 install turtle
 28、turtle.home()：移动到起始点，坐标原点（0，0）,并设置朝向为起始朝向。

 #### 实践
-用turtle绘制了卡比（不知道细长椭圆如何绘制，目前只能是大眼卡比了
-![kirby](/images/kirby.png)
+绘制了星之卡比（不知道细长椭圆如何绘制，目前只能是大眼卡比了
+![kirby](/images/kirby.jpg)
diff --git "a/source/_posts/\346\233\264\346\215\242\347\224\265\350\204\221\346\233\264\346\226\260\345\215\232\345\256\242\346\223\215\344\275\234.md" "b/source/_posts/\346\233\264\346\215\242\347\224\265\350\204\221\346\233\264\346\226\260\345\215\232\345\256\242\346\223\215\344\275\234.md"
index aa094e6..efc3a20 100644
--- "a/source/_posts/\346\233\264\346\215\242\347\224\265\350\204\221\346\233\264\346\226\260\345\215\232\345\256\242\346\223\215\344\275\234.md"
```


#### git log
显示从近到远的提交日志，加上--pretty=oneline参数可以不眼花缭乱些。
```
$ git log --pretty=oneline
9ccc804e223dfc72d3890e5eb9587b63fb0525e7 (HEAD -> hexo, origin/hexo, origin/HEAD) 更新kirby
0ef0d8581a547c7bf5c2314c3de1e939385a6451 更新文章
56509173799412c0f9575de686cebf85f61a1b46 turtle学习
4feb779ecd44370f3af674d838e96a6addbce46d 添加mac更新博客操作
a89990f1dbc74e279472d014b3987c0defc46b8c 添加mac更新博客操作
cbfd91c059a67a5e7e049e22b8dcc47c52258952 添加mac更新博客操作
ba515fe551dda7065e6cc2dd436d5cf804b25060 0508更新
61691b5c0e91aa72ca8a8fec996b839965db12f9 添加更换电脑更新博客操作
72abe14b6a972b78698e7b092a0b753eb7a258b1 添加文章SQL知识复习
d601245a8cf7c362a7ec5575792275bfffd978ab update
4205797d51a5e297b3f12e5c6745f668b66eaf09 update
49e2c265323b776a201b60fd0d70f1f862a2e107 new blog
905a1084deca61c8ee17084c4ebed8976794ec1d hexo
75ac242a01bedf1ac4f7ea4868d7831df90b0340 Site updated: 2019-07-01 11:34:45
0eacae13be7e584913f3deff4556d79d84e48e3b Site updated: 2019-07-01 09:43:16
10fd9752409b14ca8e645c91f61b8faf371a7f0c Site updated: 2019-06-28 16:02:39
6696512d45f0fd2e1f0aab4462e386a51d63d5f5 First commit
```


#### git reset --hard xxx
可以退回到指定版本。在Git中，用HEAD表示当前版本，上一个版本就是HEAD^，往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。
维护commit id也能退回到指定版本。
```
$ git reset --hard HEAD^
```
```
$ git reset --hard 0ef0d8
```


#### git reflog
可以查看历史命令。
```
$ git reflog
9ccc804 (HEAD -> hexo, origin/hexo, origin/HEAD) HEAD@{0}: pull: Fast-forward
0ef0d85 HEAD@{1}: commit: 更新文章
5650917 HEAD@{2}: commit: turtle学习
4feb779 HEAD@{3}: pull: Fast-forward
ba515fe HEAD@{4}: commit: 0508更新
61691b5 HEAD@{5}: commit: 添加更换电脑更新博客操作
72abe14 HEAD@{6}: clone: from git@github.com:hannnnnah/hannnnnah.github.io.git
```


#### git checkout -- <file
修改后还没有放到暂存区，可以丢弃工作区的修改，回到和版本库一模一样的状态。
```
$ git checkout -- readme.txt
```


#### git reset HEAD <file
可以把暂存区的修改撤销掉，重新放回工作区。
```
$ git reset HEAD readme.txt
```


#### git remote add origin git@github.com:GitHub账户名/仓库名.git
把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。


#### git push -u origin master
由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。


#### git remote rm origin
删除远程库，此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。


#### git clone git@github.com:GitHub账户名/仓库名.git
克隆一个本地库。


#### git branch
查看当前所有分支，当前分支前会标一个*号。
```
$ git branch
* dev
  master
```


#### git branch <name
创建分支。


#### git checkout -b <name
创建并切换到新的分支,相当于：
```
$ git branch dev
$ git checkout dev
Switched to branch 'dev'
```


#### git switch <name
创建分支。


#### git switch -c <name
用switch创建并切换到新的分支更科学。


#### git merge <name
把某分支的工作成果合并到当前分支上：


#### git branch -d <name
合并后就可以删除之前的分支了。


#### git branch -D <name
分支还没有被合并，如果要强行删除，需要使用大写的-D参数。


#### git log --graph
可以看到分支合并图。


#### git stash
当前工作只进行到一半，还无法提交，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作。


#### git stash list
查看工作现场列表。
```
$ git stash list
stash@{0}: WIP on dev: f52c633 add merge
```


#### git stash apply和git stash pop
用git stash apply恢复后，stash内容并不删除，需要用git stash drop来删除，可以指定stash；
用git stash pop，恢复的同时把stash内容也删了。
```
$ git stash apply stash@{0}
```


#### git cherry-pick <cmmmit_id
把某个分支提交的修改“复制”到当前分支，，避免重复劳动。


#### git tag <name
用于新建一个标签，默认为HEAD，也可以指定一个commit id。


#### git tag -a <name -m "xxx..."
可以指定标签信息。


#### git tag
可以查看所有标签。