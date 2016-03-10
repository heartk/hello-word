
在家可以用 

ssh -T git@github.com

但是在公司不可以

找了一个设置动态代理的方式

http://www.zwitterion.org/software/ssh-https-tunnel/ssh-https-tunnel

4. 创建ssh的config文件，如：
vi ~/.ssh/config
内容为：
Host github.com   
 ProxyCommand ~/.ssh/ssh-https-tunnel %h %p ~/.ssh/proxyauth  
 Port 443  
 Hostname ssh.github.com  

这里你可以看到第二行最后有一个~/.ssh/proxyauth。这是因为我单位的代理有口令，所以要再生成一个proxyauth文件，格式就是：username:password。如果你没有，去掉它就行了。

同时Hostname的目的是为了创建一个别名，其实我们使用的是ssh.github.com，但是因为平时都使用git@github.com，所以为了不进行修改，创建一个别名。
5. 下载ssh-https-tunnel，可以从  http://zwitterion.org/software/ssh-https-tunnel/ssh-https-tunnel      ，保存到你的git的~/.ssh目录下  
同时要打开这个文件进行修改，将：
 
my $proxy      = "";
my $proxy_port = ;
改成你的实际的代理服务器地址。

6. 使用ssh git@github.com 来测试

Hi limodou! You've successfully authenticated, but GitHub does not provide shell  
  access.  
 Connection to ssh.github.com closed.  

这里的难点一个是代理认证的配置，这是我在网上搜到的。还有就是GIT_SSH的设置。如果安装了TortoiseSVN，选择了ssh客户端，那么有可能ssh的代理设置通过，但是git使用时会出错，因为它会去看环境变量。



来源： http://www.chenyudong.com/archives/use-git-or-github-in-company-local-net.html

在公司的局域网使用git或github 设置代理

2014 年 1 月 30 日 / 东东东 / 2 COMMENTS
目录 [hide]
1 生成SSH Key
2 git使用http访问
3 git使用ssh进行访问
在公司这样的局域网环境中，向要走网络必须走HTTP代理出去。不能直接访问外面的服务，所以这样安全了些，但是也提供了不便的地方。因此需要设置一些代理才能使用。

常用的代理有：

HTTP、HTTPS代理 许多程序支持http代理
SOCKS代理 不是所有的程序都支持socks代理，但是常用的软件都支持
github上的仓库支持ssh、https、git三种协议的chekout（clone）操作。

生成SSH Key

参考http://www.chenyudong.com/archives/ssh-using-private-public-key-no-password.html进行SSH密钥的生产

git使用http访问

github上可以使用https进行访问。

1 $ git config --global http.proxy http://web-proxy.oa.com:8080
但是这样可以clone了。但是如果要push代码，那就麻烦了。每次都需要输入密码。

git使用ssh进行访问

使用ssh协议不仅可以访问github，还可以访问我们自己的git私有仓库，可以参考文章通过SSH创建私有git仓库。

首先，Windows用户先下载一个mysgit客户端，下个portable版的就好了，https://github.com/msysgit/msysgit/releases里面有git程序。Linux用户跳过。

第二步，配置ssh。Windows用户运行mysgit中的git-bash.bat来启动终端。编辑vim ~/.ssh/config ，将下面的内容写入到文件中

1 Host github.com *.github.com
2    ProxyCommand connect -H web-proxy.oa.com:8080 %h %p   #设置代理
3    IdentityFile ~/.ssh/privatekey/id_rsa.github
3    User git
ProxyCommand说明了设置代理，其中connect是个程序，Windows用户下载了mysgit，里面有这个程序，Linux用户可能没有，需要安装sudo apt-get install connect-proxy。

如果你使用corkscrew，那么解压缩附件，把corkscrew.exe和cygwin1.dll拷贝到mysgit的bin目录中。附：corkscrew.zip

第三步，测试

1 ssh -T git@github.com
2 Hi username! You've successfully authenticated, but GitHub does not provide shell access.
