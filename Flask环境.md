Flask坏境配置 centos

安装nginx
---------

安装nginx之前先要安装gcc编译器和相关工具，使用yum安装，非常方便。
sudo yum -y install gcc gcc-c++ make autoconf automake

nginx的一些模块需要第三方库的支持，例如gzip需要zlib，rewrite模块需要pcre库，ssl功能需要openssl库。
sudo yum -y install zlib zlib-devel openssl openssl-devel pcre pcre-devel

sudo yun install nginx

安装uwsgi
---------

wget http://projects.unbit.it/downloads/uwsgi-2.0.10.tar.gz

tar -zxv -f uwsgi-2.0.10.tar.gz

cd uwsgi-2.0.10

python setup.py install

安装flask
---------

wget http://pypi.python.org/packages/source/F/Flask/Flask-0.10.1.tar.gz

tar -zxv -f Flask-0.10.1.tar.gz

cd Flask-0.10.1

sudo python setup.py install

新建flask项目，就一个程序文件app.py，内容如下：

.. code:: python

	from flask import Flask
	app = Flask(__name__)
	 
	@app.route("/")
	def hello():
		return "Hello World!"
	 
	if __name__ == "__main__":
		app.run()

确保用flask自带的web服务器能够运行。

配置nginx和uwsgi
---------------

编辑nginx.conf
.. code:: nginx
	location / {
	    include uwsgi_params;
	    uwsgi_pass 127.0.0.1:3031;
	    root  html;
	    index  index.html index.htm;
	}
	$ sudo /usr/local/nginx/sbin/nginx -t -c /usr/local/nginx/conf/nginx.conf

然后重启nginx
nginx -s reload

创建文件夹
---------

var/www/blackgolds
把app.py 拿过来
再次创建文件app_config.xml，内容如下

.. code:: html
	<uwsgi>
	<pythonpath>/var/www/blackgolds</pythonpath>
	<module>app</module>
	<callable>app</callable>
	<socket>127.0.0.1:3031</socket>
	<master/>
	<processes>4</processes>
	<memory-report/>
	</uwsgi>

其中个参数表示：
pythonpath表示项目目录

module表示项目启动模块，如上例为app.py，这里就为app

callable表示flask项目的实例名称，上例代码中app = Flask(__name__)，所以这里为app

socket表示和nginx通信的地址和端口，和nginx配置里的uwsgi_pass一致。

processes表示开启多少个子进程处理请求。

sudo /usr/local/bin/uwsgi -x /var/www/blackgolds/app_config.xml

其中-x参数表示加载的配置文件路径。

这时候在浏览器里访问http://localhost，看到输出Hello World!就大功告成了。

如果需要让uwsgi以守护进程的方式运行，使用-d参数并指明日志路径就可以了。

sudo /usr/local/bin/uwsgi -x /srv/blackgolds/app_config.xml -d /var/log/uwsgi/uwsgi.log

uwsgi -x /srv/blackgolds/app_config.xml

停止uwsgi
---------
killall -9 uwsgi
pkill -HUP uwsgi









