---
layout:     post
title:      Intellij IDEA SVN使用一 导入、更新、提交、解决冲突
subtitle:   Intellij IDEA SVN
date:       2019-03-04
author:     BY
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - IDEA
    - SVN
---

# Intellij IDEA SVN使用一 导入、更新、提交、解决冲突

原文地址链接：

从 Eclipse 入坑 IDEA(一)：IDEA 导入 SVN 项目：[https://juejin.im/entry/582fd444a0bb9f0067b99cd3](https://juejin.im/entry/582fd444a0bb9f0067b99cd3)

使用svn 在idea中导入，更新，提交代码：[https://blog.csdn.net/xusheng_Mr/article/details/77964519](https://blog.csdn.net/xusheng_Mr/article/details/77964519)

#### 从SVN导出项目

1.选择Check out from Version Control -> Subversion

![](https://user-gold-cdn.xitu.io/2016/11/29/2e5218bcbf2efde8b5a33b1fde754926.png)

2.添加SVN仓库地址

![](https://user-gold-cdn.xitu.io/2016/11/29/a6c271f1e7c7bb9e5b9195058716e5e4.png)

3.选择刚才添加的仓库，选择Checkout

![](https://user-gold-cdn.xitu.io/2016/11/29/0e6e41fea09f1d6829d277c9b4b81c73.png)

4.选择一个路径存放导出的文件

![](https://user-gold-cdn.xitu.io/2016/11/29/b040dd60d1d7818481e177f19601b1f8.png)

5.选择具体路径与一些其他选项

![](https://user-gold-cdn.xitu.io/2016/11/29/539182ab93ee60ca1039333d1ec2d77e.png)

6.选择JDK版本

![](https://user-gold-cdn.xitu.io/2016/11/29/05b81672319f1038de1d471e9ccea0c4.png)

7.然后开始漫长的等待

![](https://user-gold-cdn.xitu.io/2016/11/29/8f40856197064873dd4ee82f213af211.png)

8.最后这里弹出已经引入项目,是否打开.选NO

![](https://user-gold-cdn.xitu.io/2016/11/29/108e80a81a85dec4826f045b91ac1ddb.png)

9.点击Import Project

![](https://user-gold-cdn.xitu.io/2016/11/29/49364a068d0d0162474082da70497b0b.png)

10.选择刚才导出的路径

![](https://user-gold-cdn.xitu.io/2016/11/29/a586db2d03e9cd3b3c226685b152db9f.png)

11.然后一直next

![](https://user-gold-cdn.xitu.io/2016/11/29/9108a7e9b1948da9cc3dad7929f870e4.png)

>到此,导入Eclipse项目结束.

### 更新代码
选中项目，右击
>就这么简单粗暴的更新代码了

![](https://alonemou.github.io/file/image/20170913113108977.png)

### 提交代码
>commit message 里边写提交的信息，这是一个良好的习惯
<img src="https://img-blog.csdn.net/20170913113711243">
<img src="https://img-blog.csdn.net/20170913113724219">

### 解决冲突
1.开发人员B对工程代码进行修改，提交；
![](https://alonemou.github.io/file/image/20181105172448287.png)

2.开发人员A在没有更新版本的情况下，修改代码提交，会出现冲突，因为A的工程版本相比SVN库中低了一个版本（开发人员B做出了修改，svn库中版本号提升）；
![](https://alonemou.github.io/file/image/20181105172605138.png)

3.冲突出现
![](https://alonemou.github.io/file/image/20181105172644987.png)

4.这时候解决冲突，A需要update更新操作;
![](https://alonemou.github.io/file/image/20181105173005673.png)

5.如图操作
![](https://alonemou.github.io/file/image/20181105173109631.png)

6.如图操作
![](https://alonemou.github.io/file/image/20181105173132770.png)

7.更新了
![](https://alonemou.github.io/file/image/20181105174638204.png)

8.更新完成提交；
![](https://alonemou.github.io/file/image/20181105174711450.png)

9.提交
![](https://alonemou.github.io/file/image/20181105174836968.png)

>已解决冲突；

![](https://alonemou.github.io/file/image/20181105174907935.png)



    分享文档，经供参考。切勿用于商业用途。
    如果你有好的文章可以投递到博主邮箱:2627045617@qq.com