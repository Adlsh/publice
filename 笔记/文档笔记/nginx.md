nginx优点：

​	并发连接高

​	内存消耗少

​	配置简单

​	成本低廉

​	支持rewrite重写规则

​	内置健康检查功能

​	节省带宽

​	稳定性高

​	模块化设计，可以动态编译

​	支持热部署

​	支持时间驱动，AIO，mmap等性能优化

​	

http事务： request <-----> response

​	request

​		<method> <url> <version>

​		

​	response

​	

method

​	get：请求资源

​	head：只响应首部信息

​	post：提交表单

​	put：上传资源

​	delete：删除资源

​	trace：跟踪资源

​	options：查看请求资源信息

​	

status

​	1** 2** 3** 4** 5**

status状态码

200：成功

301：请求的url指向的资源已被删除，但在响应报文中指明了资源现在所处的位置；（永久重定向）

302：与301相似，响应报文中指明了资源临时的位置；（临时重定向）

304：客户端发出了条件式请求，上次请求后资源未发生改变

401：需要输入账号密码认证才能访问资源；

403：请求被禁止

404：服务器无法找到客户端请求的资源

500：服务器内部错误；

502：代理服务器从后端服务器收到了一条伪响应 

pv：打开的资源页面 

uv：独立ip量



特性：

​	模块化设计，较好的扩展性

​	高可靠

​		master-->worker

​	低内存消耗

​	支持热部署

​		不停机更新配置文件，日志文件滚动，升级程序版本

​	支持时间驱动，AIO mmap

​	

基本功能

​	静态资源的web服务器，能缓存打开的文件描述符

​	http，smtp，pop3协议的反向代理服务

​	缓存加速，负载均衡

​	支持fastCGI（fpm，lnmp）

​	模块化（非dso机制），过滤器zip，SSI及图像的大小调整

​	ssl

nginx的基本架构

​	一个master 生成多个worker进程

​	事件驱动：epoll（边缘触发）

​		复用器：select，poll，rt signll

​	支持sendfile，sendfile64

​	支持AIO

​	支持mmap

​	

工作模式：

​	非阻塞，事件驱动，有一个master进程生成多个worker线程，每个worker响应n个请求

主配置段指令

​	user：	指定运行worker进程的用户和组；

​	pid：	指定nginx守护进程的pid文件；

​	worker_rlimit_nofile:	指定所有worker进程所能够打开的最大文件句柄数；

​	

性能优化相关的配置

​	worker_processes:	worker进程的个数；通常少于cpu物理核心数

​	worker_cpu_affinity cpumask：提升缓存命中率

​	timer_resolution:	计时器解析度；降低此值，可减少gettimeofday（）系统调用的次数

​	worker_priority:指明worker进程的nice值

​				-20，19

​				100，139

​			

事件相关的配置

​	accept_mutex:

​	lock_file file:accept_mutex用到的锁文件路径

​	use：#[ epoll | rtsig | select | poll ]

​		指明使用的事件模型，建议让nginx自行选择；

​	worker_connections：设定单个worker进程所能够处理的最大并发连接数量

nginx作为web服务器时使用的配置

​	http{}；由ngx_http_core_module模块引入；

​	

​	配置框架

​		http{

​		upstream{

​			...

​		}

​	

​	可以有多个server

​		server {

​			location

​			...

​		}

由安装httpd程序自动安装的程序

htpasswd -c -m /path/to/.somefile  username

​	-c:首次创建使用

​	-m：使用md5加密