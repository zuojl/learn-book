---------------------------------
Install Nginx on CentOS
---------------------------------

`Nginx <https://www.nginx.com/resources/wiki/start/topics/tutorials/install/>`_ is one of a handful of servers written to address the `C10K problem <http://www.kegel.com/c10k.html>`_. Unlike traditional servers, **Ngnix** doesn’t rely on threads to handle requests. Instead it uses a much more scalable event-driven (asynchronous) architecture. This architecture uses small, but more importantly, predictable amounts of memory under load. Even if you don’t expect to handle thousands of simultaneous requests, you can still benefit from NGINX’s high-performance and small memory footprint. *Nginx* scales in all directions: from the smallest VPS all the way up to large clusters of servers.

Step 1 - Add Nginx Yum Repository
----------------------------------------------------

To add **Nginx** yum repository, create a file named ``/etc/yum.repos.d/nginx.repo`` and paste one of the configurations below:

**CentOS:**

.. code-block:: text
    :linenos:

    [nginx]
    name=nginx repo
    baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
    gpgcheck=0
    enabled=1

**RHEL:**

.. code-block:: text
    :linenos:

    [nginx]
    name=nginx repo
    baseurl=http://nginx.org/packages/rhel/$releasever/$basearch/
    gpgcheck=0
    enabled=1

Due to differences between how CentOS, RHEL, and Scientific Linux populate the ``$releasever`` variable, it is necessary to manually replace ``$releasever`` with either 5 (for 5.x) or 6 (for 6.x), depending upon your OS version.

Step 2 - Install Nginx
----------------------------------------------------

.. code-block:: shell
    :linenos:

    sudo yum install nginx

Step 3 - Run Nginx
----------------------------------------------------

.. code-block:: shell
    :linenos:

    sudo systemctl enable nginx # run at server boot time
    sudo systemctl start nginx # Start nginx command
    sudo systemctl stop nginx # Stop nginx command
    sudo systemctl restart nginx # Restart nginx command
    sudo systemctl status nginx # Find status of nginx server command

Step 4 - Open port 80 and 443 using firewall-cmd
----------------------------------------------------

.. code-block:: shell
    :linenos:

    sudo firewall-cmd --permanent --zone=public --add-service=http
    sudo firewall-cmd --permanent --zone=public --add-service=https
    sudo firewall-cmd --reload


Fire a web browser and type the ip address.