##linux 下安装 nginx及ssl,pcre,zlib,gzip##

Nginx的（发音为“引擎X ”）是一个自由的，开放源码的，高性能的HTTP服务器。 Nginx是它的稳定性，丰富的功能设置，配置简单，资源消耗低。本教程演示了如何在CentOS编译和安装Nginx

 

首先安装ssl,pcre,zlib,gzip等，使用如下命令：

yum install -y httpd-devel pcre perl pcre-devel zlib zlib-devel GeoIP GeoIP-devel
下载所需的包：
分别从这些网站下载最新稳定版：
http://www.pcre.org/
http://zlib.net/
http://openssl.org/


	cd 
	wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.10.tar.gz
	wget http://zlib.net/zlib-1.2.5.tar.gz
	wget ftp://ftp.openssl.org/source/openssl-0.9.8o.tar.gz

解压这些文件，并不需要安装：

	tar -xvf zlib-1.2.5.tar.gz
	tar -xvf pcre-8.10.tar.gz
	tar -xvf openssl-0.9.8o.tar.gz
从http://www.nginx.org上下载nginx源码包:

	cd 
	wget http://nginx.org/download/nginx-0.7.67.tar.gz
	tar -xvf nginx-0.7.67.tar.gz 
	cd nginx-0.7.67
接下来就要编译安装了：

	./configure \
	--user=nginx --group=nginx \
	--prefix=/usr/share/nginx \
	--sbin-path=/usr/sbin/nginx \
	--conf-path=/etc/nginx/nginx.conf \
	--error-log-path=/var/log/nginx/error.log \
	--http-log-path=/var/log/nginx/access.log \
	--http-client-body-temp-path=/var/lib/nginx/tmp/client_body \
	--http-proxy-temp-path=/var/lib/nginx/tmp/proxy \
	--http-fastcgi-temp-path=/var/lib/nginx/tmp/fastcgi \
	--pid-path=/var/run/nginx.pid \
	--lock-path=/var/lock/subsys/nginx \
	--with-http_ssl_module \
	--with-http_realip_module \
	--with-http_addition_module \
	--with-http_sub_module \
	--with-http_dav_module \
	--with-http_flv_module \
	--with-http_gzip_static_module \
	--with-http_stub_status_module \
	--with-http_perl_module \
	--with-mail \
	--with-mail_ssl_module \
	--with-cc-opt='-m32 -march=i386' \
	--with-openssl=/root/openssl-0.9.8o \
	--with-pcre \
	--with-pcre=/root/pcre-8.10 \
	--with-zlib=/root/zlib-1.2.5 \
	--with-http_geoip_module
注意：此配置参数中–with-pcre指向了刚才下载并解压的源码包

现在安装：

	make
	make install
启动Nginx:

>nginx /usr/local/nginx/sbin/nginx
查看进程：

> ps -ef|grep nginx

参考：https://segmentfault.com/a/1190000002797601