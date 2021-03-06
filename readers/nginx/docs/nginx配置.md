Nginx 可以用做负载均衡，使用
	
	upstream POOL_NAME{
		server xxx1;
		server xxx2;
	}
	
也可以连接PHP\JSP	

##Nginx相关配置

###指定配置文件
	
	启动
	./nginx -c /usr/local/nginx/conf/nginx.conf
	
	重新加载配置文件
	./nginx -s reload
	
	查看nginx的版本和编译信息
	./nginx -V
注意点：

1.	配置文件必须是绝对路径。
2.	配置文件，类似php语法规则，需要分号结尾。

nginx的主要配置格式为:

	XXXX
	
	events{
	
	}
	
	http{
		server{
		}
		
		server{
		}
	}
	

###配置pid目录
pid PATH

###基础配置
1.	user USER GROUP 指定用户名和用户组
2.	worker_processes N 指定工作进程数
3.	error_log FILE LEVEL 指定日志目录和错误级别 debug info notice warn error crit
4.	log_format 格式名称 日志格式 ，只能配置在http level
5.	access_log 日志路径 格式名称
6.	env 重新定义环境变量
7.	daemon 是否为daemon 经常
8.	include 包含配置文件，支持通配符
9.	server_tokens off 关闭nginx的版本信息
9.	servername

###关闭日志

	error_log /dev/null crit;



###网络I/O模型
	
	events{
		use epoll;
		worker_connections N;
	}
MAX_CLIENTS = worker_connections * worder_process


###server配置

	server{
	}

1.	listen ip和端口
2.	error_page code uri
3.	keepalive_timeout SECOND
4.	keepalive_requests NUMBER


###location 指定格式或者路径 的配置

	location ~ 区分大小写匹配
	
	location ~* 不区分大小写匹配

	location / {
		
	}
	
###location 正则表达式 的配置

	location ~  \.(php|gif) {
	}

检查gzip是否开启成功

	 curl -I -H "Accept-Encoding: gzip, deflate" "http://localhost:1180/index.html"