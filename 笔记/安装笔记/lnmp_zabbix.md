yum groupinstall "Development tools" -y

yum -y install gcc gcc-c++ autoconf automake make openssl openssl-devel pcre-devel zlib-devel libcurl-devel libevent-devel fping libxml2-devel libjpeg-devel libpng-devel freetype-devel libmcrypt-devel expat-devel bzip2-devel curl-devel gmp-devel libc-client-devel recode-devel net-snmp-devel libtidy-devel readline-devel libxslt-devel libicu-devel libzip ncurses-devel  bison-devel cmake wget ncurses libaio bison perl perl-devel 

tar xf /data/soft/jdk1.8.0_121.tar.gz -C /usr/local/

mv /usr/local/jdk1.8.0_121/ /usr/local/jdk

vim /etc/profile

export JAVA_HOME=/usr/local/jdk

export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar

export PATH=$JAVA_HOME/bin:$PATH

export PATH=/usr/local/mysql/bin:$PATH

export PATH=/usr/local/php/sbin:/usr/local/php/bin:$PATH

export PATH=/usr/local/nginx/sbin:$PATH

export PATH=/usr/local/zabbix/sbin:/usr/local/zabbix/bin:$PATH

####################################nginx##########################################

\#安装nginx：

useradd -s /sbin/nologin nginx

cd /data/soft/ && tar xf nginx-1.8.0.tar.gz && cd nginx-1.8.0

./configure --prefix=/usr/local/nginx --user=nginx --group=nginx  --with-http_ssl_module --with-http_realip_module --with-http_flv_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_stub_status_module

\#sed -i 's/\#user  nobody/user  nginx/' /usr/local/nginx/conf/nginx.conf

/usr/local/nginx/sbin/nginx 

netstat -ntlp

###################################mysql###################################################

\#安装mysql：

yum -y install wget gcc gcc-c++ make cmake ncurses ncurses-devel libaio bison bison-devel perl perl-devel perl perl-devel 

\#下载mysql （百度网盘）

wget https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-boost-5.7.20.tar.gz

groupadd mysql && useradd -g mysql mysql

tar zxvf mysql-boost-5.7.20.tar.gz -C /usr/local/&& cd /usr/local/mysql-5.7.20

mkdir -p /data/mysql       #创建mysql数据库存放目录

 chown -R mysql:mysql /data/mysql    #设置mysql数据库目录权限

cmake . -DCMAKE_INSTALL_PREFIX=/usr/local/mysql \ -DSYSCONFDIR=/etc \ -DMYSQL_DATADIR=/data/mysql \ -DMYSQL_USER=mysql \ -DMYSQL_UNIX_ADDR=/usr/loacal/mysql/mysql.sock \ -DMYSQL_TCP_PORT=3306 \ -DWITH_MYISAM_STORAGE_ENGINE=1 \ -DWITH_INNOBASE_STORAGE_ENGINE=1 \ -DWITH_MEMORY_STORAGE_ENGINE=1 \ -DWITH_PARTITION_STORAGE_ENGINE=1 \ -DDEFAULT_CHARSET=utf8 \ -DDEFAULT_COLLATION=utf8_general_ci \ -DEXTRA_CHARSETS=all \ -DENABLED_LOCAL_INFILE=1 \ -DWITH_BOOST=boost

make -j 4 && make install

chown -R mysql:mysql /usr/local/mysql  #设置目录权限

\#初始化数据库 /usr/local/mysql/bin/mysqld --initialize-insecure --user=mysql --basedir=/usr/local/mysql --datadir=/data/mysql

cat >  /etc/my.cnf << EOF

[client]

port = 3306

default-character-set=utf8

socket = /usr/local/mysql/mysql.sock

[mysql]

port = 3306

default-character-set=utf8

socket = /usr/local/mysql/mysql.sock

[mysqld]

user = mysql

basedir = /usr/local/mysql

datadir = /data/mysql

log-bin = /usr/local/mysql/binlog

port = 3306

skip-name-resolve

character_set_server=utf8

pid-file = /usr/local/mysql/mysqld.pid

socket = /usr/local/mysql/mysql.sock

lower_case_table_names = 1

max_connections = 1000

server-id = 1

sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES,NO_AUTO_CREATE_USER,NO_AUTO_VALUE_ON_ZERO,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,PIPES_AS_CONCAT,ANSI_QUOTES

EOF

\#复制启动文件到开机自动启动

cp /usr/local/mysql/support-files/mysql.server  /etc/rc.d/init.d/mysql    

chmod 755 /etc/init.d/mysql  #增加执行权限

chkconfig --add mysql        #添加到启动服务里

chkconfig mysql on          #加入开机启动

\#编辑启动文件加入下面两行

#vim /etc/rc.d/init.d/mysql       

​	basedir = /usr/local/mysql  #mysql程序安装路径

​	datadir = /data/mysql  #Mysql数据库存放目录

systemctl start mysql            #启动服务

#####################################php######################################################

\#安装php

groupadd -r www && useradd -g www -r -s /sbin/nologin www

tar xf /data/soft/libzip-1.2.0.tar.gz -C /data/soft && cd /data/soft/libzip-1.2.0 && ./configure && make -j4 && make install

cp /usr/local/lib/libzip/include/zipconf.h /usr/local/include/zipconf.h

cat > /etc/ld.so.conf << EOF

/usr/local/lib64

/usr/local/lib

/usr/lib

/usr/lib64

EOF

ldconfig -v

tar xf /data/soft/php-7.3.24.tar.gz -C /data/soft/&& cd /data/soft/php-7.3.24 

./configure --prefix=/usr/local/php --disable-rpath --enable-fpm --with-fpm-user=www --with-fpm-group=www --with-litespeed --enable-phpdbg --enable-phpdbg-webhelper --with-config-file-path=/usr/local/php/etc --with-config-file-scan-dir=/usr/local/php/etc/php.d --enable-sigchild --enable-libgcc --disable-ipv6 --enable-dtrace --with-libxml-dir --with-openssl --with-kerberos --with-pcre-regex --with-zlib --with-zlib-dir --enable-bcmath --with-bz2 --enable-calendar --with-curl --enable-exif --disable-fileinfo --with-pcre-dir --enable-ftp --with-openssl-dir --with-gd --with-jpeg-dir --with-png-dir --with-freetype-dir --with-gettext --with-mhash --enable-intl --enable-mbstring --enable-mbregex --with-mysqli=mysqlnd --with-mysql-sock=/usr/local/mysql/mysql.sock --enable-pcntl -with-pdo-mysql=mysqlnd --with-readline --with-recode --enable-shmop --with-snmp --enable-soap --enable-sockets --enable-sysvmsg --enable-sysvsem --enable-sysvshm  --enable-wddx --with-xmlrpc --with-iconv-dir --with-xsl --enable-zip --with-libzip --enable-mysqlnd --with-pear

make  -j 6&&make install

\#配置php.ini php-fpm.conf文件

cp /data/soft/php-7.3.24/php.ini-production /usr/local/php/etc/php.ini

cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php//etc/php-fpm.conf

cp /usr/local/php/etc/php-fpm.d/www.conf.default /usr/local/php/etc/php-fpm.d/www.conf

sed -i "s/listen = 127.0.0.1:9000/listen = 192.168.225.129:9000/" /usr/local/php/etc/php-fpm.d/www.conf

\#配置通过systemctl管理服务

cp php-7.3.24/sapi/fpm/php-fpm.service /usr/lib/systemd/system/

php-fpm -t && systemctl start php-fpm && systemctl enable php-fpm

\#nginx整合php：

vim /usr/local/nginx/conf/nginx.conf

​        location / {

​            root   html;

​            index  index.php index.html index.htm;

​        }

​        location ~ \.php$ {

​                root          html;

​                fastcgi_pass   192.168.206.131:9000;

​                fastcgi_index  index.php;

​                fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;

​                include       fastcgi_params;

}

![img](C:\Users\Administrator\AppData\Local\YNote\data\qq6BD5FDEA7FE23473B47429AFB105C10E\dc36215abae64b849e04f56ada47c9c8\clipboard.png)

![img](C:\Users\Administrator\AppData\Local\YNote\data\qq6BD5FDEA7FE23473B47429AFB105C10E\5cc160421b8e4a6d94e9baf43e78f0ae\clipboard.png)

![img](C:\Users\Administrator\AppData\Local\YNote\data\qq6BD5FDEA7FE23473B47429AFB105C10E\cc3f5cbb465b45ba984e131419b72fc5\clipboard.png)

\#zabbix

\#添加zabbix用户

groupadd -r zabbix && useradd -g zabbix -r -s /sbin/nologin zabbix

tar xf /data/soft/zabbix-4.0.26.tar.gz -C /data/soft/ && cd /data/soft/zabbix-4.0.26

./configure --prefix=/usr/local/zabbix --enable-server --enable-proxy --enable-agent --enable-java --with-mysql=/usr/local/mysql/bin/mysql_config --with-libxml2 --with-net-snmp --with-zlib --with-libevent --with-openssl --with-libcurl

make && make install

ln -sv /usr/local/mysql/lib/libmysqlclient.so.20 /usr/lib64/libmysqlclient.so.20

\#登录mysql创建zabbix并导表

create database zabbix character set utf8 collate utf8_bin;

create user 'zabbix'@'%' identified by 'zabbix2020!@';

grant all on zabbix.* to 'zabbix'@'%';

flush privileges;

use zabbix;

source /data/soft/zabbix-4.0.26/database/mysql/schema.sql

source /data/soft/zabbix-4.0.26/database/mysql/images.sql 

source /data/soft/zabbix-4.0.26/database/mysql/data.sql 

\#修改zabbix_server.conf文件

cp /usr/local/zabbix/etc/zabbix_server.conf /usr/local/zabbix/etc/zabbix_server.conf.bak

sed -i "s/\# DBHost=localhost/DBHost=192.168.225.129/;s/\# DBPassword=/DBPassword=lshanhua/;s/\# ListenIP=127.0.0.1/ListenIP=192.168.206.131/" zabbix_server.conf

chown -R zabbix.zabbix /usr/local/zabbix

\#启动zabbix设置开机启动

zabbix_server

echo "/usr/local/zabbix/sbin/zabbix_server" >>/etc/rc.d/rc.local

\#创建Zabbix网页存放目录

mkdir -p /usr/local/nginx/html/zabbix

cp -a /data/soft/zabbix-4.0.26/frontends/php/* /usr/local/nginx/html/zabbix/

vim /usr/local/php/etc/php.ini

​	post_max_size   = 16M

​	max_execution_time   = 300

​	max_input_time   = 300

​	date.timezone   = Asia/Shanghai

\#sed -i "s#post_max_size = 8M#post_max_size = 16M#;s#max_execution_time = 30#max_execution_time = 300#;s#max_input_time = 60#max_input_time = 300#;s#\;date.timezone \=#date.timezone   \= Asia\/Shanghai#" /usr/local/php/etc/php.ini

\#修改配置后重启php-fpm：systemctl restart php-fpm

![img](C:\Users\Administrator\AppData\Local\YNote\data\qq6BD5FDEA7FE23473B47429AFB105C10E\4d7d1b7295e342bf902c52481ec02e34\clipboard.png)

![img](C:\Users\Administrator\AppData\Local\YNote\data\qq6BD5FDEA7FE23473B47429AFB105C10E\f7d023ad4ad64a1fb68ad857d4dbaa84\clipboard.png)

按提示下载zabbix.conf.php文件上传到：/usr/local/nginx/html/zabbix/conf/

chown nginx.nginx /usr/local/nginx/html/zabbix/conf/zabbix.conf.php

![img](C:\Users\Administrator\AppData\Local\YNote\data\qq6BD5FDEA7FE23473B47429AFB105C10E\221a729273f3419ba5c78e1181d799a6\clipboard.png)

![img](C:\Users\Administrator\AppData\Local\YNote\data\qq6BD5FDEA7FE23473B47429AFB105C10E\046a0473cd3a4053a46d221b8b34e155\clipboard.png)

![img](C:\Users\Administrator\AppData\Local\YNote\data\qq6BD5FDEA7FE23473B47429AFB105C10E\0b8944aad8704e95a8d1d05b63d0aff9\clipboard.png)

\#####################################################################

\#####################################################################

zabbix修改字体：

window（C:\Windows\Fonts）找到字体上传到/usr/local/nginx/html/zabbix/assets/fonts

![img](C:\Users\Administrator\AppData\Local\YNote\data\qq6BD5FDEA7FE23473B47429AFB105C10E\b3df777213f04f24ba7cd9b4f7584fad\clipboard.png)

/usr/local/nginx/html/zabbix/include/defines.inc.php    #72行

![img](C:\Users\Administrator\AppData\Local\YNote\data\qq6BD5FDEA7FE23473B47429AFB105C10E\640a36f2d4244ea9bfd839d6779a4f5c\clipboard.png)

![img](C:\Users\Administrator\AppData\Local\YNote\data\qq6BD5FDEA7FE23473B47429AFB105C10E\07ef642fd4bc45009bdd40c1f17824f4\clipboard.png)

\##########################################################################

zabbix-agent安装：

wget http://repo.zabbix.com/zabbix/4.0/rhel/7/x86_64/zabbix-agent-4.0.26-1.el7.x86_64.rpm

rpm -ivh [zabbix-agent-4.0.26-1.el7.x86_64.rpm](http://repo.zabbix.com/zabbix/4.0/rhel/7/x86_64/zabbix-agent-4.0.26-1.el7.x86_64.rpm)

vim /etc/zabbix/zabbix_agentd.conf

![img](C:\Users\Administrator\AppData\Local\YNote\data\qq6BD5FDEA7FE23473B47429AFB105C10E\e239b754772e43a98bed8f8fcb156eed\clipboard.png)

![img](C:\Users\Administrator\AppData\Local\YNote\data\qq6BD5FDEA7FE23473B47429AFB105C10E\d002b96058a545a583595ea0b311e4f6\clipboard.png)

启动agent端：

systemctl start zabbix-agent && systemctl enable zabbix-agent

web端添加主机：

![img](C:\Users\Administrator\AppData\Local\YNote\data\qq6BD5FDEA7FE23473B47429AFB105C10E\b87f9579cf5046dfaa6263b6dcf5abb2\clipboard.png)

![img](C:\Users\Administrator\AppData\Local\YNote\data\qq6BD5FDEA7FE23473B47429AFB105C10E\9479252a3e554e198d33fe040f7f77f1\clipboard.png)