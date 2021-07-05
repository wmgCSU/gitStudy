[TOC]

首先，在使用git前，我们需要先了解git的文件结构，包含：

**工作区：**需要同步的demo。保存自己的代码。

**暂存区：**index。一般在 .git 目录下的index。

**版本库：**即目录下的 .git文件。保存仓库版本。

![image-20210704192014724](C:\Users\wmg\AppData\Roaming\Typora\typora-user-images\image-20210704192014724.png)

#### 1、git配置

```C++
# 用户信息，构建仓库repository的用户
$ git config --global user.name "wmg"
$ git config --global user.email 2622099485@qq.com
     * --global表示对本地构建的所有repository使用该信息
# 查询某个环境变量的设定
$ git config user.name
wmg
```

#### 2、创建并管理仓库repository

![image-20210704193255326](C:\Users\wmg\AppData\Roaming\Typora\typora-user-images\image-20210704193255326.png)

```C++
① 创建版本库
$ git init  //在当前目录创建.git管理代码版本
$ git init newrepo  //指定目录创建repository
② 管理工作区
  --工作区内容可以从远端仓库clone到本地
$ git clone git@github.com:wmgCSU/runoob-git-test.git
  --当然可以自己写
$ mkdir runoob-git-test
$ cd runoob-git-test
$ echo "# 菜鸟教程git测试">>README.md
$ ls 
README.md
③ 添加修改并提交
  --自己写的只是在工作区中进行了修改，需要添加修改并提交修改到版本库中。
$ git add README.md
$ git commit -m "添加README.md"  // -m 后为添加说明，
                                // -a 提交之前所有修改
④查看工作区状态
$ git status -s  //查看在上次提交commit后是否对文件有修改
AM README        //-s 参数获取简单输出结果
A  hello.php     //AM 表示有改动                
⑤比较差异 git diff
⑥回退工作区
$ git reset  //回退工作区内容到某个版本
             //git reset HEAD~3          回退到上上上个版本，数字可更改
             //git reset 052e            回退到指定版本
             //git reset HEAD~1 res.php  回退res.php到上一个版本
```

#### 3、现在联系远端仓库

```Linux
****这里是我之前一直推送不上去的原因，就是没添加SSH key
//要push代码到远端首先需要创建SSH key，并在远端仓库添加这个key，远端添加key时会需要输入github的账号密码才能添加成功。
$ ssh-keygen -t rsa -C "2622099485@qq.com"  //邮箱为github注册邮箱
//三个回车就好，不用输入密码，注意.ssh/id_rsa.pub的路径，并进去复制其中的内容。
//进入github的setting->SSH and GPG keys->new SSH key(将刚复制的内容粘贴到里面，随便起个名字，关联上本主机，保存的时候会要输入github的注册密码)
```

#### 4、测试连接的远端仓库

```C++
$ mkdir runoob-git-test  //本地新建文件夹runoob-git-test
$ cd runoob-git-test/
$ echo "# 菜鸟教程git测试">>README.md  //新建README.md并包含内容
$ ls
README.md
$ git init  //创建本地版本库
$ git add README.md  //添加更新
$ git commit -m "添加README.md"  //提交更新，并说明
$ git remote add master git@github.com:wmgCSU/runoob-git-test.git  //为远端分支添加一个master分支
$ git push -u origin master  //本地origin分支推送到远端的master分支
$ git fetch //从远端拉取最新主分支
$ git merge //将远端与本地主分支合并
```

#### 5、分支管理

```C++
①创建分支
$ git branch  //列出本地版本库分支
* master  //带*号应该为主分支
$ git branch testing  //创建一个新的分支
$ git branch
* master
  testing
$ ls
README
$ echo 'runoob.com' > test.txt
$ git add .  //添加所有更改
$ git commit -am 'add test.txt'  //提交更改 , a为提交所有更改
$ ls
README        test.txt
②切换分支
$ git checkout testing  //切换到testing分支
$ ls
README
$ git checkout -b newtest  //创建并切换到newtest分支
③删除分支
$ git branch -d newtest  //删除newtest分支
④合并分支
$ git merge testing  //将当前分支和testing分支合并
$ git branch -d testing  //合并之后便可以删除增加的分支了，保留主分支
⑤最后还得考虑合并冲突，百度解答
```

#### 6、查看提交历史

```c++
$ git log  //查看完整信息
$ git log --oneline  //查看简洁版信息
$ git log --graph  //以拓扑图的方式查看，一般使用
$ git blame <file>  //修改记录
```

