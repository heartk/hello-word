## githug在win7下的安装过程记录

文／takamashiro（简书作者）
原文链接：http://www.jianshu.com/p/3eef3a543680
著作权归作者所有，转载请联系作者获得授权，并标注“简书作者”。

http://wiki.jikexueyuan.com/project/git-54-stage-clear/

#githug简介：

【原文】Githug is designed to give you a practical way of learning git. 
        It has a series of levels, each requiring you to use git commands to arrive at a correct answer.githug

#正文--githug安装记录

为了学习并熟练使用git操作，我打算安装githug，之前已经安装了git的windows环境，这里就我们就不谈论git的安装，
给大伙一个git的window安装教程地址如何在windows下安装GIT和Window7下Git和Github的环境配置。

虽然在githug上已经写明了how to instal,但是对安装过程中如果遇到问题，没有介绍，这里我来记录并与大家分享。

安装githug上的介绍,他支持Mac OS,Linux和windows平台，前提是安装ruby,ruby版本大于1.8.7或更高，
通过rubyinstaller网站下载安装即可。安装过程中切记要勾选 “将安装路径添加到环境变量中”（Add Ruby executables to your PATH）
不然到时候运行ruby的命令或找不到的，这和java安装很类似，只有添加了环境变量，才不需要每次都要告诉运行程序的路径。

关键到了，win+R,输入cmd，打开命令窗口后ruby --version开ruby安装好后，版本没问题，继续敲击gem install githug，
这个时候我跪了，弹出错误,

遇到问题了，这个时候我都是百度，谷歌（要科学上网）的搜，一折腾没找到要的，突然想起自己在Mac OS下gem命令时候，
第一次都要修改source，因为在国内访问不了ruby gem的默认地址，改gem source走起。修改方法[RubyGems 镜像](http://blog.csdn.net/hshl1214/article/details/49175223 "RubyGems 镜像2") 镜像。



PS:地址记得要是https:开头的http的淘宝镜像已停止。

总结：运行ruby gem 命令时候首先看gem source -l，大多数网络错误及其可能是你被墙了。


