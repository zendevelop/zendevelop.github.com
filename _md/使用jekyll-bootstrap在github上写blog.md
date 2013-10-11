##使用Jekyll-Bootstrap在Github上写blog##

最近开始markdown的学习，发现这个东西简单易容，非常方便的就可以写出格式比较好的文章，于是萌发了写一些原创blog的念头（之前在csdn,cnblogs上基本都是转载），对自己study的过程做一个记录，方便以后查询、与大家交流；同时也是对所study内容的一个梳理和巩固。  

写好了第一篇objective-c stduy记录的markdown以后，发现发布成了一个很大的问题，在cnblogs和csdn上发布出来都有问题，于是在不断的探索中发现了Github + Jekyll来写blog的方式，一切尽在掌握的感觉实在太符合极客的标准了，于是折腾了一阵，算是可以正常发布blog了，大致步骤如下：  

1. 准备好Github账号（如果你好没有，那还有什么好说的，赶快申请）；  
2. 在Github上创建一个${username}.github.com的repository；  
3. 添加SSH key；  
4. checkout Jekyll，commit到刚创建的repository；
5. 使用markdown编写blog，按照规则放入repository;
6. 使用 http://${username}.github.com来访问你的blog；  
7. 本地安装Jekyll，预览blog；
8. 为blog中的代码添加语法高亮；__[进阶]__  

现在把几个比较重要的步骤详细描述一下：
###添加SSH key###
* $ ssh-keygen -t rsa -C "test@example.com"  
按照提示一步一步进行，最后就可以在~/.ssh/下生成id_ras和id_rsa.pub文件  
* 登陆github，打开“accout setting“->"SSH Keys"->"Add SSH Key",将id_rsa.pub中的内容粘贴到“Key” Section中(__注意“Title”要留空，否则后续测试会失败__)；  
*  $ ssh -T git@github.com  
如果出现  
“Hi ${username}! You've successfully authenticated, but GitHub does not provide shell access.”  
的提示，说明添加SSH key已经成功。

###checkout Jekyll,commit到自己的repository###
{% highlight sh %}  
$ git clone https://github.com/plusjade/jekyll-bootstrap.git USERNAME.github.com  
$ cd USERNAME.github.com  
$ git remote set-url origin git@github.com:USERNAME/USERNAME.github.com.git  
$ git push origin master  
{% endhighlight %}  
执行完上述命令后，就已经成功把Jekyll导入到你自己的repository中了，过10分钟左右，你就可以通过  
__http://USERNAME.github.com__  
来访问自己的blog了。  

###编写blog，放入Jekyll  
使用markdown编写好自己的blog以后，需要按照一定的规则放入Jekyll的目录：  

* blog都放在_posts的目录下，文件名需要遵循 __YEAR-MONTH-DATE-title.suffix__的格式，例如：__2013-10-09-test.html__
看到Jekyll支援markdown，我原本的目的时在此目录下直接放*.md文件，实际测试发现中文会出现乱码，目前暂时未找到解决方法，所以暂时采用html代替；  
* blog中使用到的图片都放在__assets/images/posts/__目录下，在编写md文件时，图片链接路径为__/assets/images/posts/__;

###本地安装Jekyll，预览blog
将编写好的blog push到github以后，需要过一段时间才能预览到，为了在有修改以后，很快做预览，在本地安装Jekyll是很有必要的，安装步骤如下： 
 
1. Jekyll是基于ruby的，所有首先安装ruby；  
2. 通过ruby gem安装： __gem install jekyll__;  
3. 进入本地Jekyll的目录，使用 "__$ jekyll serve__"来启动服务器；
4. 在browser中输入“__http://localhost:4000__”来预览blog；  

(在mac os环境下，为了像linux一下可以进行软件包的安装，可能需要先安装MacPorts)