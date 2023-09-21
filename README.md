# git-test


### git设置代理
```
git config [--global] http.proxy http://127.0.0.1:端口号
git config [--global] https.proxy https://127.0.0.1:端口号

git config [--global] --unset http.proxy
git config [--global] --unset https.proxy
```

### 设置名字和邮箱

```git
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

![image text](https://github.com/ZzzYYo/git-test/blob/main/img_git/1.jpg)



### 仓库 status diff reset

```git
git init --把目录变成git管理的仓库

git add xxx.txt --把文件添加到仓库 可以一次提交多个文件

git commit -m "说明信息" -- 提交到仓库

git status --查看仓库状态

git diff file.xxx --查看文件信息(不同)

-- 修改文件后，要提交修改 也是
-- git add \ git commit -m ""

git log -- 查看记录记录
(git log --pretty=oneline)


git reset --hard HEAD^ --HEAD表示当前版本 就是最新的提交
--HEAD^ 上个版本 
--HEAD~1 上个版本

git reset --hard (commit id) -- 回到指定版本
--
```

![image text](https://github.com/ZzzYYo/git-test/blob/main/img_git/2.jpg)



```git
git reflog -- 记录每一次命令
-- cat file.xx 查看文件内容
```

![image text](https://github.com/ZzzYYo/git-test/blob/main/img_git/3.jpg)

完整用法：

![image text](https://github.com/ZzzYYo/git-test/blob/main/img_git/4.jpg)





### 记录修改

第一次修改内容 - git add - 第二次修改内容 - git commit 

提交的是第一次修改的。

-- 所以，修改一次 要先 git add 再提交 

-- 修改了内容 就要记得 add



------



```git
git checkout -- file.xxx -- 把在工作区的修改全部撤销 
--
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

```



![image text](https://github.com/ZzzYYo/git-test/blob/main/img_git/5.jpg)







### 撤销修改

![image text](https://github.com/ZzzYYo/git-test/blob/main/img_git/6.jpg)



场景1：修改了某一个文件 file.xxx ， git status   --发现有修改 

使用 git checkout -- file.xxx   就会撤销工作区文件的修改 

![image text](https://github.com/ZzzYYo/git-test/blob/main/img_git/7.jpg)



场景2：修改了文件 ，并且 git add 了  到了暂存区

先使用 git reset HEAD file.xxx 

```git
git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。
```

然后使用 git checkout -- file.txt 就可以了







------



### 删除与还原

删除版本库中的文件

```git
git rm file.xxx
git commit -m "rm xxx"
```



误删还原

```git
git checkout --file.xxx
```

--`git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

--从来没有被添加到版本库就被删除的文件，是无法恢复的！

```git
git add 和 git commit 文件后

在本地误删了文件 

可以用 git checkout -- file.xxx 恢复
```





### vim

vim 

```vim
vi file.txt
按i 进入命令模式
编辑
按esc退出编辑模式
按冒号 : 
wq
保存退出
-- w保存 退出 q  不保存退出 q!
```



### SSH

```gif
ssh-keygen -t rsa -C "电子邮箱"
--C:\Users\用户名\.ssh  秘钥保存位置
--id_rsa 是私钥、 id_rsa.pub 是公钥 可以告诉别人


git remote add origin 仓库名
git push -u origin master
git branch -M main
git push -u origin main

同步之后
本地提交后 就可以用 git push origin main 命令推送到github

```

#### 删除远程库

```gif
git remote -v 查看远程库信息
git remote rm origin 删除
-- 此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除。
```



克隆远程库

```gif
git clone 远程库
```



### 分支

```gif
git checkout -b dev
--git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
--git branch dev
--git checkout dev

git branch -- 查看分支
git checkout 分支名 --切换分支
```



dev分支修改的内容 main分支没有 --因为还没有合并 

![image text](https://github.com/ZzzYYo/git-test/blob/main/img_git/8.jpg)



```git
git merge dev --合并分支

注意到上面的Fast-forward信息，Git告诉我们，这次合并是“快进模式”，也就是直接把master指向dev的当前提交，所以合并速度非常快。

当然，也不是每次合并都能Fast-forward，我们后面会讲其他方式的合并。

git branch -d dev 删除分支

```



#### 切换分支

```git
切换分支
git switch -c dev

--查看分支的合并情况
git log --graph --pretty=oneline --abbrev-commit

--合并分支 并禁用 Fast forward --no-ff
git merge --no-ff -m "描述" dev

合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。
```





### git stash 存放工作现场

```gif
git stash --可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作


git stash list --查看存放的工作现场
两个办法：
一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；

另一种方式是用git stash pop，恢复的同时把stash内容也删了：
```





```gif
git cherry-pinck 提交id --复制一个特定的提交到当前分支
```

![image text](https://github.com/ZzzYYo/git-test/blob/main/img_git/9.jpg)



```gif
git branch -D --强行删除分支
```



```gif
git remote
git remote -v 查看远程仓库的信息
```



```gif
git branch --set-upstream-to=origin/<branch> dev
-- 设置dev和origin/dev的链接
```

![image text](https://github.com/ZzzYYo/git-test/blob/main/img_git/10.jpg)



```gif
git rebase --把分叉的提交历史“整理”成一条直线，看上去更直观。缺点是本地的分叉提交已经被修改过了。
```



Git的标签虽然是版本库的快照，但其实它就是指向某个commit的指针（跟分支很像对不对？但是分支可以移动，标签不能移动），所以，创建和删除标签都是瞬间完成的。





### 标签

```gif
git tag <name> --打标签
git tag --查看标签

给历史提交打标签 git log找到commit id 
git tag <name> id名

git show <name> --查看标签信息

git tag -a 标签名 -m "说明" 

标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签。

git tag -d <name> 删除标签
git push origin 标签名 --上传到远程
git push origin --tags -- 一次性推送全部尚未推送到远程的本地标签

标签已经推送到远程 删除
先在本地删除 然后在远程删除
git tag -d 标签名
git push origin :refs/tags/标签名
```

