# git入门

## 1.安装后

~~~shell
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
~~~

## 2.初始化版本库

~~~shell
git init
~~~

## 3.添加文件到版本库

~~~shell
git remote add origin 仓库地址(https://···或者ssh://····)  # 绑定远程仓库
git add 文件名
git commit -m "修改说明"
~~~

## 4.仓库状态

~~~shell
git status
~~~

## 5.查看历史版本记录

~~~shell
git log # 查看所有历史记录
git log --prettry=oneline # 以更简洁的方式查看历史记录
~~~

## 6.回退历史版本

~~~python
git log --pretty=oneline # 先查看历史记录的版本号
git reset --hard 版本号的id
~~~

## 7.显示所有的历史操作记录(真)

~~~shell
git reflog
~~~

## 8.撤销修改

### 撤销工作区的修改

~~~shell
git checkout -- 文件名
~~~

### 撤销暂存区的修改

即，add命令后

#### 第一种(建议)

~~~shell
git checkout 版本的id 文件名
~~~

####第二种

1.将暂存区的文件撤回到工作区去

> git reset --hard 版本的id

2.如有必要可以再撤销工作区的文件

~~~shell
git checkout -- 文件名
~~~

## 9.删除操作

### 删除文件

~~~shell
rm 文件名（此时删除工作区的，git会记录你的删除动态）
~~~

### 确定删除

~~~shell
git rm 文件名
git commit -m "删除说明"
~~~

### 取消删除

~~~shell
git checkout -- 文件名
~~~

## 10.git分支

### 创建分支

~~~shell
git checkout -b dev
~~~

### 切换到主分支

~~~shell
git checkout master
~~~

### 合并分支

首先需要切换到主分支，再进行合并

~~~shell
git merge dev
~~~

### 删除分支

~~~shell
git branch -d dev
~~~

### 查看分支

~~~shell
git branch
~~~

注意：dev分支须在提交后，切换到master分支时才能看到与master中不一样的地方，否则在master中看到的和在dev中的没有区别

##11.推送到远程仓库

~~~shell
git push -u origin master
git push
~~~

## 12.删除本地绑定的远程仓库

~~~shell
git remote remove origin
~~~

## 13.拉取代码或更新代码

~~~shell
git clone 地址(https://····)
git pull origin master
git pull
~~~

## 14.使用ssh方式免密登录

> 1.创建秘钥
>
> `ssh-keygen -t rsa -C "youremail@example.com"`
>
> 将生成秘钥的公钥添加到github里settings中的ssh设置中

# git远程仓库问题

## 本地版本库与远程版本库的冲突

~~~markdown
git pull 将远程仓库的代码拉取到本地
在本地手动解决冲突
git push 解决完成后再次推送到远程仓库
解决冲突后，使用这两个命令： git add    git commit
~~~

## 提交dev分支到远端仓库

~~~shell
git checkout -b dev   # 创建dev分支

git add 文件名
git commit -m "提交说明"

git push origin dev   # 这个时候没有合并到master分支，单独保存dev分支

------以上为上传dev分支到远端------

git checkout master   # 切换到master分支，准备进行合并
git merge dev   # 合并dev分支到master
git branch -D dev   # 删除本地dev分支
git push -d origin dev   # 删除远程分支
~~~

# git暂存区

假如我在一个git_test文件夹下执行了`git init`命令，那么会在该文件夹下新建一个 **.git** 的隐藏文件，此时，git_test目录下就是整个工作区，而**.git**文件夹即为版本库，其中**index**即为暂存区（或者成为stage），其中还包含了git为我们自动创建的第一个master分支，以及指向master的一个指针**HEAD**（该指针为一个概念性的指针，非C/C++中的指针）。

使用**git add**指令时会将文件从工作区复制到暂存区，再使用**git commit**指令时会将文件从暂存区提交到一个新建的master版本分支中，同时指针HEAD更改为当前新的master版本分支的地址（HEAD中存储的为当前master的版本id）。

每一次的修改和删除并没有进行真正的修改或删除，而是新生成一个文件，即为添加一个状态。

![仓库的说明](D:\abc_python2\git\img\仓库的说明.png)

