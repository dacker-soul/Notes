Scrapy指南 Mac版本

安装pip工具包
------------
下面这行命令敲进去执行：

	wget https://bootstrap.pypa.io/get-pip.py

接下来安装pip：

	sudo python get-pip.py

pip源修改（如果有你有vpn，请跳过此步骤）	
-----------------------------------

首先创建配置文件，默认情况下Mac端好像是没有pip的配置文件的，我们需要自行创建。
打开终端，在HOME下创建.pip目录：

	mkdir .pip

接下来创建配置文件pip.conf：
	
	touch pip.conf

打开pip.conf文件，输入以下两行：	

	[global]
	index-url = http://pypi.mirrors.ustc.edu.cn/simple

国内目前的pipy镜像主要有以下几个：

http://pypi.douban.com/ 豆瓣

http://pypi.hustunique.com/ 华中理工大学

http://pypi.sdutlinux.org/ 山东理工大学

http://pypi.mirrors.ustc.edu.cn/ 中国科学技术大学

http://pypi.v2ex.com/ V2EX社区

大家可以看自己需要选择，用法都一样，只需要替换配置文件当中index-url的值即可。但不要忘记后面的/simple目录！



安装Scrapy
---------

	sudo pip install Scrapy

解决ImportError:cannot import name xmlrpc_client问题
---------------------------------------------------

	sudo rm -rf /Library/Python/2.7/site-packages/six*
	
	sudo rm -rf /System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/six*

	sudo pip install six

	搞定。








