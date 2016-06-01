---
layout: post
title: Git命令使用一些总结
date: 2016-05-13 22:00
comments: true
categories: [工具]
tags: featured
keywords: GIT
---
author:[kobepeng](http://yipeng.info)  
程序员天生喜欢敲命令舒适感，还有就是GIT实在太火了，不会GIT都不好意思说自己是程序员。
<!-- more -->
### 查看今天代码量
```
git diff --shortstat "@{0 day ago}"
```

### 查看提交
git查看上一次提交内容
``` 
git log -n 1
```    

查看最近一次提交的所有更改细节，可以使用
```
 git log -n 1 -p
```   
  
查看最近一次提交所有更改文件
```
 git log -n 1 --stat
```

### 合并多次提交
合并多次提交，可以使用如下命令，n代表合并提交的次数
```
git rebase –i HEAD~n
```  

合并到指定位置可以使用
```
git rebase -i f7d0bd75c8dabe127d8cbd2c1d70ff188ff83392
```  
接下来会进入vim模式，除第一个 pick 外，其余的全部修改成 squash，也可以缩写为 s，保存即可。
具体使用可以参考这篇文章，说得还是比较详细的：http://blog.csdn.net/yangcs2009/article/details/47166361

### 强制更新覆盖
```
git fetch --all
git reset --hard origin/master
```
### 本地删除github文件或文件夹
```
git rm -r --cached some-directory
```

### 撤销
1. 已修改未提交的文件
```
git checkout file-name
```

2. 撤销某次操作
```
// 撤销前一次 
git revert HEAD   
// 撤销前前一次 
git revert HEAD^            
// 撤销指定的版本 
git revert commit-id 
```

### 解决冲突
1.  确认本地修改无用，直接reset，见强制更新覆盖
2.  本地修改有用，则直接一个一个文件看，修正冲突再提交
3. 想直接忽略合并
```
git reset --hard HEAD
```

### 排除文件(.gitignore )  

```
#忽略gitignore文件  
.gitignore  
#忽略后缀名为.o和.a的文件  
*.[oa]  
#显示指定忽略名称为main的文件  
main  
```

### Mac：git提交代码至github
```
// 1 检查是否已经有 SSH Key。
cd ~/.ssh
// 2 生成新ssh
ssh-keygen -t rsa -C “email"
// 3 会生成: id_rsa , id_rsa.pub，把id_rsa.pub的内容复制到github  
Settings--> SSH keys --> new SSH key
//4  测试
ssh -T git@github.com
// 5 配置账户
git config --global user.name "username"
git config --global user.email “email"
// 6 初始化项目
git init
git add .
git commit -m 'here we go!’
git remote add origin git@github.com:qindongliang/Demo.git 
git push -u origin master
```  
报错1:  
```
"![rejected] master -> master (fetch first)"
```
解决办法：执行git fetch
  
报错2:  
```
src refspec master does not match any
```
解决办法: 本地版本库为空, 空目录不能提交 (只进行了init, 没有add和commit)  
报错3:   
```
non-fast-forward
```
解决办法: 
```
git config branch.master.remote origin  
git config branch.master.merge refs/heads/master 
git pull 
```

### windows配置Git
1. 下载，最好去官网，百度推荐的是64位的(也没个提示)，下载下来后才发现不能用。  
2. 利用GitBash生成public ssh key
```
cd ~
ssh-keygen -t rsa
```
会提示输入文件名与密码
3. 在*C:\Users\lenovo\.ssh*（我的路径）生成
 * id_rsa
 * id_rsa.pub


### 安装git服务端
参考1: [使用gitosis](http://rangochen.blog.51cto.com/2445286/1394340) ：基于CentOS  
参考2: [使用Gitolite](http://blog.chinaunix.net/uid-15174104-id-3843570.html)：本人未测试  
参考3: http://www.lifeba.org/arch/git_gitosis.html  ：如何添加新的客户端  
 错误1   
```
gitosis.init.InsecureSSHKeyUsername: Username contains not allowed characters 
```
stackoverflow上的解释都是用户名不合法，当然，提示信息也是这么说的。主要原因是*@*后的第一个字母不能为数字。  
错误2  
```
gitosis.serve.main:Repository read access denied
```  
解决办法:   
1. 原因1 ：gitosis.conf中的members与keydir中的用户名不一致  
办法：改为一致  
2. gitosis.conf配置问题
```
[group gitosis-admin]
writable = gitosis-admin 
members = lenovo@kobepeng
[group git-test]
writable = git-test
members = lenovo@kobepeng
```
改为【待究】
```
[group gitosis-admin]
writable = gitosis-admin git-test
members = lenovo@kobepeng
```
3. 以上两种必须更新到服务端才有效

### 修改Git配置文件
```
cd .git
vim config 
```

### 参考
颜海镜 http://yanhaijing.com/git/2014/11/01/my-git-note/  
http://xiezefan.me/2014/10/05/tip-git/  