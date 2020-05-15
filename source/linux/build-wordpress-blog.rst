------------------------
Wordpress 博客系统搭建
------------------------

**Wordpress** 是由 **PHP** 开发的所以要想其能工作，还是有一些需要安装的依赖。

本文是基于 ``wordpress4.9.8`` 版本搭建的,依赖 ``php7.2`` 以上和 ``mysql5.6`` 或者 ``mariaDB10.0`` ， 还有 WEB 容器。

关于 **Nginx** 的安装请参考 : `Install Nginx on CentOS <./install-nginx-centos.html>`_

关于 **MariaDB** 的安装请参考 `Install MariaDB on CentOS <./install-mariadb-centos.html>`_

PHP7.2
---------------------------------------

CentOS7 上PHP的默认版本是5.6，而我们需要的是7.2。
当然可以使用源码编译安装，但是对于只是搭建一个博客而言的话，可以选择直接源安装：

.. code-block:: bash
	:linenos:

	yum install epel-release -y

	rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
	
安装 php72w 相关的库

.. code-block:: bash
	:linenos:

	yum -y install php72w 

	yum -y install php72w-cli php72w-fpm php72w-common php72w-devel php72w-embedded php72w-gd php72w-mbstring php72w-mysqlnd php72w-opcache php72w-pdo php72w-xml

配置 php-fpm
---------------------------------------

确保你已近安装 Nginx 最新版本，查找 Nginx 的用户和用户组

.. code-block:: bash
	:linenos:
	
	egrep '^(user|group)' /etc/nginx/nginx.conf
	
会有如下的简单输出

.. code-block:: text
	:linenos:
	
	user nginx;
	
编辑 `vim /etc/php-fpm.d/www.conf` 设置用户和用户组为 nginx

.. code-block:: text
	:linenos:
	
	user = nginx
	group = nginx
	
保存文件，并启动 php-fpm

.. code-block:: bash
	:linenos:
	
	systemctl start php-fpm
	
配置 nginx
---------------------------------------

添加并编辑