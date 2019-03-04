---
layout:     post
title:      IntelliJ IDEA—SVN的配置及使用
subtitle:   IntelliJ_IDEA SVN
date:       2019-03-01
author:     BY
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - IDEA
    - SVN
---

# IntelliJ IDEA—SVN的配置及使用


##安装服务端(如何你有SVN地址就不需要这一步)

windows下，这里选择VisualSVN-Server，下一步，下一步安装 

![](https://img-blog.csdn.net/20180601084338777?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTA3NTg0MTA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

安装成功后打开软件，创建仓库。 

![](https://img-blog.csdn.net/20180601084540430?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTA3NTg0MTA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

![](https://img-blog.csdn.net/20180601084714345?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTA3NTg0MTA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

##安装客户端（准备好连接步骤)

既然要使用svn，那么首先我们需要下载一个 svn的客户端，可以到这里下载对应的安装程序：
[http://subversion.apache.org/packages.html#windows](http://subversion.apache.org/packages.html#windows)

建议使用TortoiseSVN(小乌龟)，下载后安装 ，然后记住安装路径，我安装的是64位的。

TortoiseSVN的下载地址 ： [https://tortoisesvn.net/downloads.html](https://tortoisesvn.net/downloads.html)

![](https://img-blog.csdn.net/20180601084910971?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTA3NTg0MTA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

在安装svn客户端的时候一定要勾选，**否则在idea上集成svn的时候会找不到 svn.exe 而报错。**

如果安装时忘记勾选了的话，安装包重新运行，选择modify，然后勾选command line client tools项就行了。 

![](https://img-blog.csdn.net/20180601084946389?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTA3NTg0MTA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)


##idea配置svn

安装好svn客户端后，想启用idea的SVN插件还需要在idea配置一下，file - setting 按钮打开设置界面 或者（Ctrl + Alt + S）快捷键 ，如下图所示： 
![](https://img-blog.csdn.net/20180601085144370?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTA3NTg0MTA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

###方法一：直接检出
重启一下你的IntelliJ Idea，然后从svn库中下载项目： 

![](https://img-blog.csdn.net/20180601085614232?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTA3NTg0MTA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

点击绿色加号，输入svn的地址，然后输入svn的账号与密码就可以愉快的使用SVN了。 
 
![](https://img-blog.csdn.net/20180601085657301?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTA3NTg0MTA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

![](https://img-blog.csdn.net/20180601085732621?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTA3NTg0MTA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

###方法二：添加仓库 → 检出
![](https://img-blog.csdn.net/20180601093027314?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTA3NTg0MTA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

--------------------- 
作者：木子木泗 

来源：CSDN 

原文：[https://blog.csdn.net/u010758410/article/details/80532992](https://blog.csdn.net/u010758410/article/details/80532992) 

版权声明：本文为博主原创文章，转载请附上博文链接！


    分享文档，经供参考。切勿用于商业用途。
    如果你有好的文章可以投递到博主邮箱:2627045617@qq.com
