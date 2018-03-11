---
title: Github自身踩到的坑
date: 2017-07-28 23:36:05
tags:
---
![image.png](http://upload-images.jianshu.io/upload_images/4340772-4134778cdc246b6f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>用Github有一两年了，是时候总结一下以前踩得坑了，这些坑开始时还真把自己摔得不轻！！！！！
小插曲：自己以前用hexo搭建的博客，每次写博客都要新建.md文件等初始化步骤,然后提交，有些繁琐，再加上自己又换了台电脑，又要部署hexo（虽然不需要重新部署），但还是有些步骤，索性用简书写，方便快捷些！
<!-- more -->
### git pull时`ssh: Could not resolve hostname github.com: Name or service not known, fatal: Could not read from remote repository.`

```
$ git pull
ssh: Could not resolve hostname github.com: Name or service not known
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```
**这个错误好醉，是因为没网了，就很皮**


### git本地仓库首次push到远程仓库出现错误 ! [rejected] master -> master (fetch first)

新建好本地的仓库和远程仓库之后，

经过
`git add . `
然后
`git commit -m "......"`
最后想推送到远程仓库的时候

`git push -u origin master`
出现下图错误


![image.png](http://upload-images.jianshu.io/upload_images/4340772-92f06947d40a738d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

解决很简单，使用强制推送
使用下面的命令
`git push -f origin master `

*附上git push 的说明*
```
NAME

git-push - Update remote refs along with associated objects

SYNOPSIS

git push [--all | --mirror | --tags] [--follow-tags] [--atomic] [-n | --dry-run] [--receive-pack=<git-receive-pack>]
       [--repo=<repository>] [-f | --force] [--prune] [-v | --verbose]
       [-u | --set-upstream]
       [--[no-]signed|--sign=(true|false|if-asked)]
       [--force-with-lease[=<refname>[:<expect>]]]
       [--no-verify] [<repository> [<refspec>…​]]

-f  --force
Usually, the command refuses to update a remote ref that is not an ancestor of the local ref used to overwrite it. Also, when --force-with-lease option is used, the command refuses to update a remote ref whose current value does not match what is expected.

This flag disables these checks, and can cause the remote repository to lose commits; use it with care.

Note that --force applies to all the refs that are pushed, hence using it with push.default set to matching or with multiple push destinations configured with remote.*.push may overwrite refs other than the current branch (including local refs that are strictly behind their remote counterpart). To force a push to only one branch, use a + in front of the refspec to push (e.g git push origin +master to force a push to the master branch). See the<refspec>... section above for details.
```

### github上传时出现error: src refspec master does not match any

如下：

![image.png](http://upload-images.jianshu.io/upload_images/4340772-ee916947d8e430af.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


**引起该错误的原因是，目录中没有文件，空目录是不能提交上去的**

解决方法:**先提交文件`git add . git commit -m ""`**
例如下：
```
touch README
git add README 
git commit -m 'first commit'
git push origin master
```
###  fatal： unable to create '../../.git/index.lock':File exists
  
  ![mark](http://upload-images.jianshu.io/upload_images/4340772-427e594cf0d5fe04.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  解决方法：**把文件index.lock删掉**

###Permission denied (publickey).
fatal: The remote end hung up unexpectedly

错误原因：github上没有配置公钥
解决方法：配置公钥，并放到github上
GitHub设置公钥在windows下面

1. 安装git，从程序目录打开 "Git Bash" 
2. 键入命令：ssh-keygen -t rsa -C "email@email.com"
  "email@email.com"是github账号
3. 提醒你输入key的名称，输入如id_rsa
如果执行成功。返回

Generating public/private rsa key pair.
Enter file in which to save the key (/home/forwhat.cn/.ssh/id_rsa): 
在这里就是设置存储地址了.反正我是直接按的回车，一直回车

4. 在C:\Documents and Settings\Administrator\下产生两个文件：id_rsa和id_rsa.pub
5. 把4中生成的密钥文件复制到C:\Documents and Settings\Administrator\.ssh\ 目 录下。
6. 用记事本打开id_rsa.pub文件，复制内容，**在github.com的网站上到ssh密钥管理页面，添加新公钥，随便取个名字例如你的电脑名**

需要注意步骤2中产生的密钥文件在当前用户的根目录，必须把这两个文件放到当前用户目录的“.ssh”目录下才能生效。

坑不会踩完的，但会一直进步着，大家加油......