# Git项目

## 发demo

{ 

自己分支做完修改

Git add .

Git commit -m “fix:备注”

切到demo分支上

Git pull(每次进来都操作一下)

Git merge 自己分支

./pack.sh

切回自己分支

SSH上操作：

cd devspace

切到项目分支上

Gb 查看自己当前在那条分支

Git pull

Git log 查看是否有自己修改的记录

./build.sh     (w)

./pub_this.sh demo

}

## 发线上

自己分支操作完成

Git add .

Git commit -m “fix:备注”

切到feature分支上

Git pull(每次进来都操作一下)

Git merge 自己分支

Git push

切online分支

Git pull 

Online 分支 merge feature 分支

git push

./pack.sh online

ssh上

cd devspace

切到项目分支上

Gb 查看自己当前在那条分支(online)

Git pull

Git log 查看是否有自己修改的记录

./build.sh  online   (f)

得到tag号 项目 ，分支 保存

# Git项目注意事项

##### 项目打包误操作在远程合作公共分支上打包解决办法：

###### 以项目为例：

回滚远程分支git reset --hard <commit_id>，git push origin HEAD:master(远程分支) --force

回滚完之后，删除本都的合作公共分支，通过git fetch --all拉取最新的远程分支，然后切过来让本地变成回滚后的一个状态(git log确认一下是否是回滚完后的代码) 。

**注：谁出了问题谁进行回滚操作，回滚完后需要在群里通知一下，让用此分支得人删除本地分支，然后走上一步。**

# Git使用技巧

## 0.git如何取消commit

git reset --soft HEAD^  (代码状态(git status查看)回到commit之前add之后了)

(HEAD^  表示上一次的commit，也可以写成HEAD~1)

(撤回两次之前的，可以使用HEAD^^或者HEAD~2，以此类推)

git reset HEAD ***.vue(文件名)  撤回add动作。

将此分支状态退回到修改后的状态

git reset --hard HEAD^，撤销commit，并且撤销add动作。

## 1.回滚到某个版本（把此分支给改了）

git reset --hard <commit_id>

git push origin HEAD:master(远程分支) --force

## 2.在一个新分支上，回滚到某个版本，不影响原分支

git checkout <commit_id>  //这个时候会到一个指针分支上

git checkout -b 新分支名   

## 3.本地git和远程相通（SSH密钥）

http://blog.csdn.net/hustpzb/article/details/8230454/

 一 、

设置Git的user name和email：

​    $ git config --global user.name "xxx"

​    $ git config --global user.email "haiyan.xu.vip@gmail.com"

二、

生成SSH密钥过程：
          1.查看是否已经有了ssh密钥：cd ~/.ssh
          如果没有密钥则不会有此文件夹，有则备份删除（rm -rf ~/.ssh/*）

2.生成密钥： 

$ ssh-keygen -t rsa -C “haiyan.xu.vip@[gmail.com](http://gmail.com/)”

按3个回车，密码为空。

最后得到了两个文件：id_rsa和id_rsa.pub

密钥就要id_rsa.pub文件内，进入后复制

可以用这个方式：运行 cat ~/.ssh/id_rsa.pub ，得到一串东西，完整的复制这串东西

三、

进入github，点击左边的列表，进入Profile Settings,点击SSH Keys添加密钥即可。



## 4.删除远程/本地分支

 git push origin --delete 远程分支名  //远程

git branch -D 分支名  //本地

## 5.merge了之后，push了，但是有错误，需要撤回merge的

https://www.cnblogs.com/utank/p/7880441.html

 git reflog 先查看（这个需要找到谁最后一个提交的，因为这个里边查看的是自己的提交记录）

 git branch 新分支名 HEAD@{4} 这个是上边查看出来的

![img](https://cdn.nlark.com/yuque/0/2021/png/21426585/1627377445445-4a96b07b-a7a0-4373-9767-737a0ffd95f1.png)

## 6.删除tag号

git tag -d tag号



## 7.[Filename too long for git](http://wiki.ayibang.cn/display/web/Filename+too+long+for+git)(这个应该是报文件名字过长)

在[Git](http://lib.csdn.net/base/git) bash中，运行下列命令： git config --global core.longpaths true



8.设置git的快速输入命令

先找到路径

![img](https://cdn.nlark.com/yuque/0/2021/png/21426585/1627622890070-6cef9a22-3c63-4d5d-95ff-07f76a154489.png)

在gitconfig文件的最后加上：

[alias]

​    ck = checkout

​    cm = commit

​    s = status

​    pl = pull

​    ps = push

​    l = log

​    b = branch



## 8.恢复误删除的本地分支

- 查找历史提交的commit：

git reflog show--date=iso

上面命令会显示出所有的提交记录。找到你需要恢复的对应的 commit。记住对应的 commitId (前面的绿色部分)。
	***git reflog用来记录你的每一次命令，--date=iso 表示以标准时间显示。\***

![img](https://cdn.nlark.com/yuque/0/2021/png/21426585/1630462696289-701b6ca9-81ca-4c4a-a690-046ba92581b9.png)

- 查看对应 commit 的详情，确认是否是想要恢复的内容

git shou commitID

- 恢复本地分支

git checkout -b 要恢复的分支名 commitId(刚刚copy下来的)

完成

