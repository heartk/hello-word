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


=========== 2016年6月14日12:44:54 ========================

http://www.oschina.net/news/71749/taobao-gems-ruby-china

最近发现taobao的gem源不好使，各种找不到对应版本的包之类的错误。在他们的issue提了bug后，维护者回复了这样的一段话：

新的Gems源由腾讯云赞助

整个 gems.ruby-china.org 的架构：

```
                    |
                          [CDN 1] [CDN 2] [CDN 3] ... [CDN N]
                                           |
                           {Load Balance us.gems.ruby-china.org}
                                           |
                         [us0.gems.ruby-china.org]  ... us1 .. us2
                                           |
                                        [Nginx]
                                           | -------------------------------------------------- |                           |                    |
    {/gems, /quick, *.4.8, *.4.8.gz}       {/}                 {/api}
               |                            |                     |
  [rubygems.global.ssl.fastly.net]      [app server]         [rubygems.org]
```

新的方案的特点

实时的，不再有同步耗时的问题；
全球 400+ CDN 节点（据腾讯官方所说 ~~）为 Gem 下载加速；
更加简单有效的架构，稳定性更高；
背后有两台国外服务器，确保稳定性，确保 CDN 汇源能获取到数据；
使用方式

https://gems.ruby-china.org/

在那边的页面有介绍了，和之前 ruby.taobao.org 的方式也是一样的

项目源代码

https://github.com/ruby-china/rubygems-mirror



