---
title: 手把手教你Git安装、配置和使用以及博客搭建
date: 2016-12-12 15:28:38
tags: 
- git
- gitHub
- hexo
---

欢迎我的小博，我正在努力学习，我会在不久将来给你们分享更多的干货，希望你们喜欢。
## Please read happily

<!-- more -->
<The rest of contents | 余下全文>


###  需要用到的工具
![git.exe](http://upload-images.jianshu.io/upload_images/433829-b5b729f1b3dbfe38.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
### 安装Git只需要一直next就可以

1 首先去用邮箱注册[GitHub](https://github.com/)账号
2 测试git是否安装成功 启动程序GitBash
3 终端配置


## 配置Git
<br />

### 配置用户名
`
$ git config --global user.name.你的用户名
`
### 配置邮箱
`
$ git config --global user.email 你的邮箱
`
### 保存
`
$ git config --global alias.ymz(这个随意) commit
`

### 设置ssh 这个很重要哦   
`
$ ssh-keygen -c "你的邮箱" -t rsa
`

### 查看你的C盘Users/Administrator目录
1 是否有.ssh文件夹
2 文件夹中有id_rsa、id_rsa.pub文件

###  强制查看是否关联Github
```
$ ssh -T git@github.com
The authenticity of host 'github.com (192.30.253.113)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes)? yes
Warning: Permanently added 'github.com,192.30.253.113' (RSA) to the list of known hosts.
Permission denied (publickey).
```
why?为什么会这样呢？ 因为没有登录GitHub把我们刚刚生成的ssh给设置进去。

###  说到这里了，肯定是设置SSH呢
1 首先进入Git-Setting设置[SSH and GPG key](https://github.com/settings/keys)
2 将id_rsa.pub文件用记事本打开将里面所有的内容复制添加到github中的key


###  再次查看是否关联Github
```
$ ssh -T git@github.com
Warning: Permanently added the RSA host key for IP address '192.30.253.112' to the list of known hosts.
Permission denied (publickey).
```

###  妈蛋居然提示失败，我发现我复制的时候没有复制完全，纯属意外
```
$  ssh -T git@github.com
Hi gyymz1993! You've successfully authenticated, but GitHub does not provide shell access.
```
这个提示就表示成功了

###  这个命令可以查看出错信息
```
$  shh -T -v git@github.com
```

<br />
# 现在就是最实用最牛逼得部分了
<br />
###  提交本地项目步骤
1 在gitHub新建个项目（这个不会自行百度）
2 命令提交

### 增加注释文件
```
$  echo "# MstarStoreApp" >> README.md
```
第一步想当然注释告诉别人这个项目是干嘛的

### 初始化仓库
```
$  git init
```
### 添加所有文件
```
$  git add .
```

### commit
```
$  git commit -m "first commit"
```

### 你的gitHub项目的SSH路径

```
$  git remote add origin git@github.com:yourname/XXX.git
```

### 最后一步就是提交了

```
$  git push -u origin master
```

### 今天提交遇见这种错误

```
$ git push -u origin master
Counting objects: 159, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (150/150), done.
Writing objects: 100% (159/159), 521.63 KiB | 0 bytes/s, done.
Total 159 (delta 3), reused 0 (delta 0)
packet_write_wait: Connection to 192.30.253.112 port 22: Broken pipe
fatal: The remote end hung up unexpectedly
fatal: The remote end hung up unexpectedly
```

### 可能是文件过大造成的解决办法 

```
$ git config http.postBuffer 524288000
Administrator@2011-20151010QW MINGW64 /d/Git/Hexo1 (master)
$ git push -u origin master
Counting objects: 159, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (150/150), done.
Writing objects: 100% (159/159), 521.63 KiB | 0 bytes/s, done.
Total 159 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), done.
To github.com:gyymz1993/GitHubHexo.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```



### 当你修改你的项目提交

```
$  git add . 
$  git commit -m 'update'
$  git push 
```

### 当你本地删除文件后需要拉取GitHub文件执行，意思是还原和服务器同步

```
$  git checkout .
```

### 当你在gitHub服务修改文件后必须pull才能修改到本地

```
$  git pull
```

### 下载一个项目到本地

```
$  git clone git@github.com:yourname/XXX.git
```
<br />
# 更牛逼的部分，搭建自己的博客  

<br />
### 需要用到的工具[node.js.msi](http://nodejs.cn/download/) 下载   

##### 安装只需要一直next就可以

### next完后测试是否安装成功 

### 配置环境变量
```
$  找到安装目录    C:\node
   配置环境变量  path  加上  C:\node
```

### 测试方法

```
$  npm --v
```

```
$  node -v
```
#### 如果出现版本号则正确安装

###  本地博客环境创建 安装hexo 
```
$  npm install -g hexo
```

###  保存安装
```
$  npm install hexo --save
```

### 查看 hexo是否安装成功
```
$  hexo -v
```

###  初始化hexo 
```
$  hexo init 
```

###  开始本地服务
```
$  hexo s
```
再浏览器中输入 [http://localhost:4000/](http://localhost:4000/)    即可浏览

### 找到hexo目录下的D:\Git\Hexo\_config.yml文件修改项目中的ssh路径
```
$ deploy:
  type: git
  repo: git@github.com:yourname/yourname.github-io.git 
```
### 修改成这样执行  
```
$ npm install hexo-deployer-git --save
```
### 生成静态网页

```
$ hexo g
```

### 部署到服务器

```
$ hexo d
```

# 折腾（换电脑后使用） 目前自己笨方法
<br />

### 前面得操作一样，紧跟着初 ##始化hexo后用原来的博文文件替换现在的文件
1 Hexo\node_modules（这个其实就是你安装的插件什么搜索系统啊之类的）
2 _config.yml 你自己的配置文件
3 \Hexo\source 目录下你的所有博客文件
4 themes\yelee 这个是你的主题文件
当你替换好之后开始接着到

开始本地服务>后的操作

### 直到最后一步部署到服务器

```
$ hexo d
ERROR Deployer not found: git
```
这是咋回事呢？

### 重新安装deployer
```
$ npm install hexo-deployer-git
```

### 保存安装deployer
```
$ npm install hexo-deployer-git --save
```

# Hexo\node_modules（这个其实就是你安装的插件什么搜索系统啊之类的）这部分其实替换没有用，必须重新安装
# Hexo\node_modules（这个其实就是你安装的插件什么搜索系统啊之类的）这部分其实替换没有用，必须重新安装
# Hexo\node_modules（这个其实就是你安装的插件什么搜索系统啊之类的）这部分其实替换没有用，必须重新安装



