# Nginx 基础使用

## 目录结构

进入Nginx的主目录我们可以看到这些文件夹

![](D:\Study\自学\笔记\img\QQ截图20230601132813.png)

其中这几个文件夹在刚安装后是没有的，主要用来存放运行过程中的临时文件

- client_body_temp 
- fastcgi_temp 
- proxy_temp 
- scgi_temp

- conf——用来存放配置文件相关
- html——用来存放静态文件的默认目录 html、css等
- sbin——nginx的主程序

## 基本运行原理

![](D:\Study\自学\笔记\img\QQ截图20230601162544.png)

## Nginx配置与应用场景

### 最小配置

#### worker_processes 

worker_processes 1; 默认为1，表示开启一个业务进程

#### worker_connections 

worker_connections 1024; 单个业务进程可接受连接数 

#### include mime.types; 

include mime.types; 引入http mime类型 

#### default_type application/octet-stream; 

default_type application/octet-stream; 如果mime类型没匹配上，默认使用二进制流的方式传输。 

#### sendfile on; 

sendfile on; 使用linux的 sendfile(socket, file, len) 高效网络传输，也就是数据0拷贝。 

未开启sendfile

![](D:\Study\自学\笔记\img\QQ截图20230601162800.png)

开启后

![](D:\Study\自学\笔记\img\QQ截图20230601162822.png)

#### keepalive_timeout 65; 

keepalive_timeout 65;

### server

![](D:\Study\自学\笔记\img\QQ截图20230601162909.png)

虚拟主机配置

```
server {
    listen 80; 监听端口号
    server_name localhost; 主机名
    location / { 匹配路径
        root html; 文件根目录
        index index.html index.htm; 默认页名称
    }
    
    error_page 500 502 503 504 /50x.html; 报错编码对应页面
    location = /50x.html {
        root html;	
    }
}
```

### 虚拟主机 

原本一台服务器只能对应一个站点，通过虚拟主机技术可以虚拟化成多个站点同时对外提供服务

### servername匹配规则 

我们需要注意的是servername匹配分先后顺序，写在前面的匹配上就不会继续往下匹配了。

#### 完整匹配 

我们可以在同一servername中匹配多个域名

```
server_name vod.mmban.com www1.mmban.com;
```

#### 通配符匹配

```
server_name *.mmban.com
```

#### 通配符结束匹配

```
server_name vod.*;
```

#### 正则匹配

```
server_name ~^[0-9]+\.mmban\.com$;
```

```
worker_processes  1;
events {
    worker_connections  1024;
}
http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;
    server {
        listen       80;
        server_name  www.mmban.com;
        location / {
            root   /www/www;
            index  index.html index.htm;
        }
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }  
    }
    server {
        listen       80;
        server_name  vod.mmban.com;
        location / {
            root   /www/vod;
            index  index.html index.htm;
        }
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }  
    }	
}
```

## 域名解析相关企业项目实战技术架构

- 多用户二级域名 
- 短网址 
- httpdns

## 反向代理

![](D:\Study\自学\笔记\img\QQ截图20230604144829.png)

反向代理方式是指以代理服务器来接受Internet上的连接请求，然后将请求转发给内部网络上的服务器；并将从服务器上得到的结果返回给Internet上请求连接的客户端，此时代理服务器对外就表现为一个服务器。

反向代理服务器通常有两种模型，一种是作为内容服务器的替身，另一种作为内容服务器集群的负载均衡器。

- 作内容服务器的替身


如果您的内容服务器具有必须保持安全的敏感信息，如信用卡号数据库，可在防火墙外部设置一个代理服务器作为内容服务器的替身。当外部客户机尝试访问内容服务器时，会将其送到代理服务器。实际内容位于内容服务器上，在防火墙内部受到安全保护。代理服务器位于防火墙外部，在客户机看来就像是内容服务器。

当客户机向站点提出请求时，请求将转到代理服务器。然后，代理服务器通过防火墙中的特定通路，将客户机的请求发送到内容服务器。内容服务器再通过该通道将结果回传给代理服务器。代理服务器将检索到的信息发送给客户机，好像代理服务器就是实际的内容服务器。如果内容服务器返回错误消息，代理服务器会先行截取该消息并更改标头中列出的任何 URL，然后再将消息发送给客户机。如此可防止外部客户机获取内部内容服务器的重定向 URL。

这样，代理服务器就在安全数据库和可能的恶意攻击之间提供了又一道屏障。与有权访问整个数据库的情况相对比，就算是侥幸攻击成功，作恶者充其量也仅限于访问单个事务中所涉及的信息。未经授权的用户无法访问到真正的内容服务器，因为防火墙通路只允许代理服务器有权进行访问。

- 作为内容服务器的负载均衡器


可以在一个组织内使用多个代理服务器来平衡各 Web 服务器间的网络负载。在此模型中，可以利用代理服务器的高速缓存特性，创建一个用于负载平衡的服务器池。此时，代理服务器可以位于防火墙的任意一侧。如果 Web 服务器每天都会接收大量的请求，则可以使用代理服务器分担 Web 服务器的负载并提高网络访问效率。

对于客户机发往真正服务器的请求，代理服务器起着中间调停者的作用。代理服务器会将所请求的文档存入高速缓存。如果有不止一个代理服务器，DNS 可以采用“轮询法”选择其 IP 地址，随机地为请求选择路由。客户机每次都使用同一个 URL，但请求所采取的路由每次都可能经过不同的代理服务器。

可以使用多个代理服务器来处理对一个高用量内容服务器的请求，这样做的好处是内容服务器可以处理更高的负载，并且比其独自工作时更有效率。在初始启动期间，代理服务器首次从内容服务器检索文档，此后，对内容服务器的请求数会大大下降。

```

    server {
        listen       80;
        server_name  www.mmban.com;

        location / {
            proxy_pass http://atguigu.com/;
        }

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
  
    }
    
    # 访问www.mmban.com 会跳到尚硅谷官网
```

### 基于反向代理的负载均衡

克隆两个centos，ip分别设为192.168.203.130，192.168.203.131（网段要用自己的电脑对应）

配置静态ip

```
vi /etc/sysconfig/network-scripts/ifcfg-ens33
```

```

TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=static
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=ens33
UUID=a154d4b2-9bee-4dfe-85c7-f4c0c9deb192
DEVICE=ens33
ONBOOT=yes
IPADDR=192.168.203.129 #分别修改成130、131
NETMASK=255.255.255.0
GATEWAY=192.168.203.2
DNS1=8.8.8.8

```

接下来重启网络服务

```
systemctl restart network 
```

```
#130 nginx.conf

worker_processes  1;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;
    keepalive_timeout  65;

    server {
        listen       80;
        server_name  localhost;

        location / {
            root   html;
            index  index.html index.htm;
        }

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }

}


```

130的nginx192.168.在html目录下的index.html文件

```
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>I am from 192.168.203.130</h1>
</body>
</html>

```

131的nginx在html目录下的index.html文件

```
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>I am from 192.168.203.131</h1>
</body>
</html>
```

浏览器访问192.168.203.130、131

#### 将129代理到130

129的nginx.conf

```
worker_processes  1;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;
    keepalive_timeout  65;

    server {
        listen       80;
        server_name  www.mmban.com;

        location / {
            proxy_pass http://192.168.203.130;
        }

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }

}
#访问129
```

#### 配置101的负载均衡（轮询模式）

默认情况下使用轮询方式，逐一转发，这种方式适用于无状态请求。

```
worker_processes  1;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;
    keepalive_timeout  65;
    
    #定义一组服务器
    upstream httpds{
        server 192.168.203.130:80;
        server 192.168.203.131:80;
    }

    server {
        listen       80;
        server_name  www.mmban.com;

        location / {
            proxy_pass http://httppds;
        }

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }

}
```

#### weight(权重)

指定轮询几率，weight和访问比率成正比，用于后端服务器性能不均的情况。

```
    #定义一组服务器
    upstream httpds{
        server 192.168.203.130:80 weight=10 down; 
        server 192.168.203.131:80 weight=1;
        server 192.168.203.132:80 weight=1 backup;

    }
```

down：表示当前的server暂时不参与负载 

weight：默认为1.weight越大，负载的权重就越大。 

backup： 其它所有的非backup机器down或者忙的时候，请求backup机器。

#### 其他负载均衡策略（不常用）

- ip_hash

根据客户端的ip地址转发同一台服务器，可以保持会话，但是很少用这种方式去保持会话，例如我们当前正在使用wifi访问，当切换成手机信号访问时，会话就不保持了。

- least_conn

最少连接访问，优先访问连接最少的那一台服务器，这种方式也很少使用，因为连接少，可能是由于该服务器配置较低，刚开始赋予的权重较低。

- url_hash（需要第三方插件）


根据用户访问的url定向转发请求，不同的url转发到不同的服务器进行处理（定向流量转发）。

- fair（需要第三方插件）

根据后端服务器响应时间转发请求，这种方式也很少使用，因为容易造成流量倾斜，给某一台服务器压垮。

## 动静分离

![](D:\Study\自学\笔记\img\QQ截图20230604155449.png)
为了提高网站的响应速度，减轻程序服务器（Tomcat，Jboss等)的负载，对于静态资源，如图片、js、css等文件，可以在反向代理服务器中进行缓存，这样浏览器在请求一个静态资源时，代理服务器就可以直接处理，而不用将请求转发给后端服务器。对于用户请求的动态文件，如servlet、jsp，则转发给Tomcat，Jboss服务器处理，这就是动静分离。即动态文件与静态文件的分离。

动静分离可通过location对请求url进行匹配，将网站静态资源（HTML，JavaScript，CSS，img等文件）与后台应用分开部署，提高用户访问静态代码的速度，降低对后台应用访问。通常将静态资源放到nginx中，动态资源转发到tomcat服务器中。

### 配置反向代理

```
#配置130的反向代理
location / {
    proxy_pass http://127.0.0.1:8080;
    root html;
    index index.html index.htm;
}
#将129中的images资源删除
#重新访问130，图片访问不见了
#将images资源放在130上
worker_processes  1;
events {
    worker_connections  1024;
}
http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;
    server {
        listen       80;
        server_name  localhost;
        location / {
            proxy_pass http://192.168.203.129:8080;
        }       
        location /images {
            root   /www/resources;
            index  index.html index.htm;
        }        
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }
}

#访问130，图片回来了

```

### 增加每一个location

```
location /css {
    root /usr/local/nginx/static;
    index index.html index.htm;
}
location /images {
    root /usr/local/nginx/static;
    index index.html index.htm;
}
location /js {
    root /usr/local/nginx/static;
    index index.html index.htm;
}
```

### 使用一个location

使用正则 

location 前缀

/ 通用匹配，任何请求都会匹配到。

= 精准匹配，不是以指定模式开头

~ 正则匹配，区分大小写

~* 正则匹配，不区分大小写

^~ 非正则匹配，匹配以指定模式开头的location

```
^ ：匹配输入字符串的起始位置
$ ：匹配输入字符串的结束位置
* ：匹配前面的字符零次或多次。如“ol*”能匹配“o”及“ol”、“oll”
+ ：匹配前面的字符一次或多次。如“ol+”能匹配“ol”及“oll”、“olll”，但不能匹配“o”
? ：匹配前面的字符零次或一次，例如“do(es)?”能匹配“do”或者“does”，”?”等效于”{0,1}”
. ：匹配除“\n”之外的任何单个字符，若要匹配包括“\n”在内的任意字符，请使用诸如“[.\n]”之类的模式
\ ：将后面接着的字符标记为一个特殊字符或一个原义字符或一个向后引用。如“\n”匹配一个换行符，而“\$”则匹配“$”
\d ：匹配纯数字
{n} ：重复 n 次
{n,} ：重复 n 次或更多次
{n,m} ：重复 n 到 m 次
[] ：定义匹配的字符范围
[c] ：匹配单个字符 c
[a-z] ：匹配 a-z 小写字母的任意一个
[a-zA-Z0-9] ：匹配所有大小写字母或数字
() ：表达式的开始和结束位置
| ：或运算符  //例(js|img|css)
```

```
//location大致可以分为三类
精准匹配：location = /{}
一般匹配：location /{}
正则匹配：location ~/{}
//location常用的匹配规则：
= ：进行普通字符精确匹配，也就是完全匹配。
^~ ：表示前缀字符串匹配（不是正则匹配，需要使用字符串），如果匹配成功，则不再匹配其它 location。
~ ：区分大小写的匹配（需要使用正则表达式）。
~* ：不区分大小写的匹配（需要使用正则表达式）。
!~ ：区分大小写的匹配取非（需要使用正则表达式）。
!~* ：不区分大小写的匹配取非（需要使用正则表达式）。
//优先级
首先精确匹配 =
其次前缀匹配 ^~
其次是按文件中顺序的正则匹配 ~或~*
然后匹配不带任何修饰的前缀匹配
最后是交给 / 通用匹配

```

```
 (1）location = / {}
=为精确匹配 / ，主机名后面不能带任何字符串，比如访问 / 和 /data，则 / 匹配，/data 不匹配
再比如 location = /abc，则只匹配/abc ，/abc/或 /abcd不匹配。若 location  /abc，则即匹配/abc 、/abcd/ 同时也匹配 /abc/。

（2）location / {}
因为所有的地址都以 / 开头，所以这条规则将匹配到所有请求 比如访问 / 和 /data, 则 / 匹配， /data 也匹配，
但若后面是正则表达式会和最长字符串优先匹配（最长匹配）

（3）location /documents/ {}
匹配任何以 /documents/ 开头的地址，匹配符合以后，还要继续往下搜索其它 location
只有其它 location后面的正则表达式没有匹配到时，才会采用这一条

（4）location /documents/abc {}
匹配任何以 /documents/abc 开头的地址，匹配符合以后，还要继续往下搜索其它 location
只有其它 location后面的正则表达式没有匹配到时，才会采用这一条

（5）location ^~ /images/ {}
匹配任何以 /images/ 开头的地址，匹配符合以后，停止往下搜索正则，采用这一条

（6）location ~* \.(gif|jpg|jpeg)$ {}
匹配所有以 gif、jpg或jpeg 结尾的请求
然而，所有请求 /images/ 下的图片会被 location ^~ /images/ 处理，因为 ^~ 的优先级更高，所以到达不了这一条正则

（7）location /images/abc {}
最长字符匹配到 /images/abc，优先级最低，继续往下搜索其它 location，会发现 ^~ 和 ~ 存在

（8）location ~ /images/abc {}
匹配以/images/abc 开头的，优先级次之，只有去掉 location ^~ /images/ 才会采用这一条

（9）location /images/abc/1.html {}
匹配/images/abc/1.html 文件，如果和正则 ~ /images/abc/1.html 相比，正则优先级更高

优先级总结：
(location =) > (location 完整路径) > (location ^~ 路径) > (location ~,~* 正则顺序) > (location 部分起始路径) > (location /)

```



### location匹配顺序

- 多个正则location直接按书写顺序匹配，成功后就不会继续往后面匹配 
- 普通（非正则）location会一直往下，直到找到匹配度最高的（最大前缀匹配） 
- 当普通location与正则location同时存在，如果正则匹配成功,则不会再执行普通匹配
-  所有类型location存在时，“=”匹配 > “^~”匹配 > 正则匹配 > 普通（最大前缀匹配）

```
location ~*/(css|img|js) {
    root /usr/local/nginx/static;
    index index.html index.htm;
}
```

- 第一个必选规则

直接匹配网站根，通过域名访问网站首页比较频繁，使用这个会加速处理，比如说官网。这里是直接转发给后端应用服务器了，也可以是一个静态首页

```
location = / {
    proxy_pass http://127.0.0.1:8080/; 
}
```

- 第二个必选规则

处理静态文件请求，这是nginx作为http服务器的强项,有两种配置模式，目录匹配或后缀匹配,任选其一或搭配使用

```
location ^~ /static/ {
    root /webroot/static/;
}

location ~* \.(html|gif|jpg|jpeg|png|css|js|ico)$ {
    root /webroot/res/;
}

```

- 第三个规则

通用规则，用来转发动态请求到后端应用服务器

```
location /api/ {
    proxy_pass http://127.0.0.1:3000/api/
}
```



### alias与root

```
location /css {
    alias /usr/local/nginx/static/css;
    index index.html index.htm;
}
```

root用来设置根目录，而alias在接受请求的时候在路径上不会加上location。

 1）alias指定的目录是准确的，即location匹配访问的path目录下的文件直接是在alias目录下查找的；

 2）root指定 的目录是location匹配访问的path目录的上一级目录,这个path目录一定要是真实存在root指定目录下的； 

3）使用 alias标签的目录块中不能使用rewrite的break（具体原因不明）；另外，alias指定的目录后面必须要加上"/"符 号！！ 

4）alias虚拟目录配置中，location匹配的path目录如果后面不带"/"，那么访问的url地址中这个path目录后 面加不加"/"不影响访问，访问时它会自动加上"/"； 但是如果location匹配的path目录后面加上"/"，那么访问的url地 址中这个path目录必须要加上"/"，访问时它不会自动加上"/"。如果不加上"/"，访问就会失败！ 5）root目录配置 中，location匹配的path目录后面带不带"/"，都不会影响访问。

## UrlRewrite



### rewrite语法格式及参数语法:

```
rewrite是实现URL重写的关键指令，根据regex (正则表达式)部分内容，
重定向到replacement，结尾是flag标记。

rewrite <regex> <replacement> [flag];
关键字 	正则 		替代内容 	flag标记

关键字：其中关键字error_log不能改

正则：perl兼容正则表达式语句进行规则匹配
替代内容：将正则匹配的内容替换成replacement
flag标记：rewrite支持的flag标记
rewrite参数的标签段位置：
server,location,if
flag标记说明：
last #本条规则匹配完成后，继续向下匹配新的location URI规则
break #本条规则匹配完成即终止，不再匹配后面的任何规则
redirect #返回302临时重定向，浏览器地址会显示跳转后的URL地址
permanent #返回301永久重定向，浏览器地址栏会显示跳转后的URL地址
```

```
rewrite ^/([0-9]+).html$ /index.jsp?pageNum=$1 break;

```

优点：掩藏真实的url以及url中可能暴露的参数，以及隐藏web使用的编程语言，提高安全性便于搜索引擎收录

缺点：降低效率，影响性能。如果项目是[内网](https://so.csdn.net/so/search?q=内网&spm=1001.2101.3001.7020)使用，比如公司内部软件，则没有必要配置。

### 同时使用负载均衡 

![](D:\Study\自学\笔记\img\QQ截图20230604182649.png)

#### 应用服务器防火墙配置 

开启129的防火墙

```
systemctl start firewalld
```

重载规则

```
firewall-cmd --reload
```

查看已配置规则

```
firewall-cmd --list-all
```

指定端口和ip访问(添加之后记得重新启动防火墙)

```
firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="192.168.203.130" port protocol="tcp" port="8080" accept"
```

移除规则

```
firewall-cmd --permanent --remove-rich-rule="rule family="ipv4" source
address="192.168.203.130" port port="8080" protocol="tcp" accept"
```

网关配置

```
upstream httpds {
    server 192.168.203.130 weight=8 down;
    server 192.168.203.131:8080 weight=2;
    server 192.168.203.132:8080 weight=1 backup;
}
location / {
    rewrite ^/([0-9]+).html$ /index.jsp?pageNum=$1 redirect;
    proxy_pass http://httpds ;
}
```

## 防盗链配置

盗链是指服务提供商自己不提供服务的内容，通过技术手段绕过其它有利益的最终用户界面（如广告），直接在自己的网站上向最终用户提供其它服务提供商的服务内容，骗取最终用户的浏览和点击率。受益者不提供资源或提供很少的资源，而真正的服务提供商却得不到任何的收益。

为了模拟盗链，在这里让129为服务站点，130为网关服务器，131访问130进行盗链。

```
valid_referers none | blocked | server_names | strings ....;
```

- none， 检测 Referer 头域不存在的情况。 
- blocked，检测 Referer 头域的值被防火墙或者代理服务器删除或伪装的情况。这种情况该头域的值不以 “http://” 或 “https://” 开头。 
- server_names ，设置一个或多个 URL ，检测 Referer 头域的值是否是这些 URL 中的某一个。 在需要防盗链的location中配置

```
valid_referers 192.168.44.101;
if ($invalid_referer) {
    return 403;
}
```

使用curl测试 

```
curl -I http://192.168.44.101/img/logo.png 
```

带引用 

```
curl -e "http://baidu.com" -I http://192.168.44.101/img/logo.png
```

```
#129
worker_processes  1; #允许进程数量，建议设置为cpu核心数或者auto自动检测，注意Windows服务器上虽然可以启动多个processes，但是实际只会用其中一个

events {
    #单个进程最大连接数（最大连接数=连接数*进程数）
    #根据硬件调整，和前面工作进程配合起来用，尽量大，但是别把cpu跑到100%就行。
    worker_connections  1024;
}
http {
    #文件扩展名与文件类型映射表(是conf目录下的一个文件)
    include       mime.types;
    #默认文件类型，如果mime.types预先定义的类型没匹配上，默认使用二进制流的方式传输
    default_type  application/octet-stream;
    #sendfile指令指定nginx是否调用sendfile 函数（zero copy 方式）来输出文件，对于普通应用，必须设为on。如果用来进行下载等应用磁盘IO重负载应用，可设置为off，以平衡磁盘与网络IO处理速度。
    sendfile        on;  
     #长连接超时时间，单位是秒
    keepalive_timeout  65;
#定义一组服务器
upstream httpds{
    server 192.168.8.102 weight=10;
    server 192.168.8.103 weight=1;
}
 #虚拟主机的配置
    server {
    #监听端口
        listen       80;
        #域名，可以有多个，用空格隔开
        server_name  test80.xzj520520.cn;
	#配置根目录以及默认页面
        location / {
            proxy_pass http://httpds;
            # root   /www/test80;
            # index  index.html index.htm;
        }
	#出错页面配置
        error_page   500 502 503 504  /50x.html;
        #/50x.html文件所在位置
        location = /50x.html {
            root   html;
        }      
    } 
}
```

```

#130
worker_processes  1;



events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;

    keepalive_timeout  65;


    server {
        listen       80;
        server_name  localhost;


        location / {
            proxy_pass http://192.168.8.101:8080;
        }
        
        
        location ^~/images/ {
            root   /www/resources;
        }
       
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }

}


```

```
#131
worker_processes  1;



events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;
    keepalive_timeout  65;


    server {
        listen       80;
        server_name  localhost;

        location / {
            proxy_pass http://192.168.8.102;
        }
         
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

    }

}

```

访问131可以正常访问129上的内容

```
#修改130
worker_processes  1;



events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;


    sendfile        on;
    
    keepalive_timeout  65;


    server {
        listen       80;
        server_name  localhost;


        location / {
            proxy_pass http://192.168.8.101:8080;
        }
        
        
        
        location ^~/images/ {
            valid_referers 192.168.8.102;  #valid_referers 指令，配置是否允许 referer 头部以及允许哪些 referer 访问。192.168.8.102不是ip而是域名（去掉http:// 前缀）
            if ($invalid_referer) {  # 注意这里if后要加空格
                return 403; ## 返回错误码
            }
            
            root   /www/resources;
        }
        

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

    }


}


```

用131访问，已经加载不出图片了

```
server {
    server_name referer.test.com;
    listen 80;

    error_log logs/myerror.log debug;
    root html;
    location / {
        valid_referers none server_names
                       *.test.com www.test.org.cn/nginx/;
        if ($invalid_referer) {
                return 403; # 返回错误码
        }
        return 200 'valid\n';
    }
}

# none：表示没有 referer 的可以访问
# server_names：表示本机 server_name 也就是 referer.test.com 可以访问
# *.test.com：匹配上了正则的可以访问
# www.test.org.cn/nginx/：该页面发起的请求可以访问

```

### 配置错误提示页面

在130html目录中添加403.html

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Error</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>An error occurred.</h1>
<p>非法请求.</p>

</body>
</html>

```

```
worker_processes  1;



events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;

    keepalive_timeout  65;

    server {
        listen       80;
        server_name  localhost;

        location / {
            proxy_pass http://192.168.203.129:8080;
        }
        
        location ^~/images/ {
            valid_referers 192.168.8.102 baidu.com;
            #valid_referers 指令，配置是否允许 referer 头部以及允许哪些 referer 访问。192.168.8.102不是ip而是域名（去掉http:// 前缀）
            if ($invalid_referer) {
            
            	rewrite ^/ /images/403.png break;
                #return 403; # 返回错误码
            }
            
            root   /www/resources;
        }
        

        error_page   403  /403.html;
        location = /403.html {
            root   html;
        }
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        
    }

}


```

## 高可用配置

### 安装Keepalived 

#### 编译安装 

下载地址

```
https://www.keepalived.org/download.html#
```

使用 ./configure 编译安装 

如遇报错提示

```
configure: error:
!!! OpenSSL is not properly installed on your system. !!!
!!! Can not include OpenSSL headers files. !!!
```

安装依赖

```
yum install openssl-devel
```

#### yum安装

```
yum install keepalived
```

配置 

使用yum安装后配置文件在 

```
/etc/keepalived/keepalived.conf
```

最小配置 

- `vrrp_instance`、`authentication`、`virtual_router_id`、`virtual_ipaddress`这几个一样的机器，才算是同一个组里。这个组才会选出一个作为Master机器

第一台机器

```
! Configuration File for keepalived
global_defs {
	router_id lb111	# 名字与其他配置了keepalive的机器不重复就行
}
vrrp_instance atguigu {	#vrrp实例名可以随意取
    state MASTER 	#只能有一个默认的Master，其他写BACKUP
    interface ens33	# ip addr查看下网卡名，默认时ens33
    virtual_router_id 51
    priority 100		# 多台安装了keepalived的机器竞争成为Master的优先级
    advert_int 1		#通信时间
    authentication {
        auth_type PASS
        auth_pass 1111
    }
    virtual_ipaddress {
    	192.168.203.200		#虚拟IP
    }
}
```

第二台机器

```
! Configuration File for keepalived
global_defs {
    router_id lb110
}
vrrp_instance atguigu {
    state BACKUP
    interface ens33
    virtual_router_id 51
    priority 50
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass 1111
    }
    virtual_ipaddress {
        192.168.203.200
    }
}

```

启动服务

```
systemctl start keepalived
```

## 配置证书

购买服务器——>购买域名，并解析到这个主机——>购买证书，绑定到域名上，并且把证书文件安装到服务器，并在Nginx上配置好

这时候，这个域名就可以使用https进行访问里（`https://xxxx`），浏览器上会有一个小锁

上面的流程我比较熟悉了，就直接跳过了，这里直接写申请到证书后的Nginx配置部分

**下载证书文件**

![](D:\Study\自学\笔记\img\image-20220503192957256.png)

下载后，解压压缩包，可以看到两个文件，一个是 `xxx.key`（私钥）和`xxx.pem`（证书）

**配置**

将两个文件上传到Nginx目录中，记得放置的位置。我这里直接放在nginx.conf配置文件所在的目录（`/usr/local/nginx/conf`），所以写的都是相对路径

```shell
server {
	listen 443 ss1;
	
	ss1 certificate  xxx.pem; #这里是证书路径
	ss1_ certificate_key  xxx.key  #这里是私钥路径
}
```
