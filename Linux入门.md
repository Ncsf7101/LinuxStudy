**连接网络**

onboot=yes 具体文件自己百度

手动给虚拟机适配器vm8指定一个ip，尽量离本机ip距离近一点

DNS为8.8.8.8

vm网络恢复默认

或者直接去B站找springcloud收藏视频

**常用指令**

pwd	显示当前所在目录

clear	清屏[Ctrl + L]

**创建指令**

mkdir -p aaa/bbb	创建双层目录

touch a.txt	创建一个空文件

vim cc.txt	若文件为空，保存创建；否则修改

cat aa.txt > bb.txt	复制aa内容至不存在的bb; 若存在则修改 (重定向)

cat aa.txt >> bb.txt	复制aa内容至不存在的bb; 若存在则追加 (重定向)

**复制指令**

cp xxx.xx a.txt	复制某文件

cp xxx.xx /aa	复制到某目录

**删除指令**

rm	 删除空目录及文件

rm -r	删除目录及文件，且询问

rm -rf	删除文件及目录，且不询问

rm -rf /*	 删除根目录下所有

**压缩与解压缩**

-c 创建新tar文件、-v 显示运行过程、-f 指定文件名、-z 压缩为gzip、-x 解压tar

打包		tar -cvf xxx.tar ./*

​				tar -zcvf xxx.tar.gz ./* （打包并压缩） 

解压		tar -xvf xxx.tar

​				tar -zxvf xxx.tar.gz -C /user/aaa

**查找指令**

find / -name aa.txt 	从根目录下查找文件

find ./ -name aa.txt	从当前目录下查找文件

find / -name aa*.txt	查找所有以aa开头的文件

grep Adress xxx.xxx	查找包含查找字符串的行

grep Adress xxx.xxx --color	查找包含查找字符串的行，并且高亮显示关键字

grep Adress xxx.xxx --color -A1 -B1	after一行，before一行

**Vim**

命令行操作： 

​				:q!	!强制退出

​				:/xxx	文件内搜索XXX字符串，如搜索8080

**进程指令**

ps -ef	查看当前运行的进程

ps -ef | grep java	管道搜索进程

kill -9 30131	强制关掉某个进程PID

**管道**	

(一个进程的输出 当成另一个进程的输入)

ps -ef | grep java	搜索进程的输出作为搜索的输入

ls --help | more	help文档的输出作为more的输入

**权限**

(分为十个字符，四个部分 - --- --- ---)

1.代表文件类型

​	- 表示文件	d 表示文件夹	l 表示链接

2.当前用户具有该文件的权限

​	r read读[4]	   w write写[2]		 x execut执行[1]

3.当前组内其他用户具有该文件的权限

​	r read读[4]	   w write写[2]		 x execut执行[1]

4.其他组的用户具有该文件的权限

​	r read读[4]	   w write写[2]		 x execut执行[1]

**修改权限**

chmod u=rwx, g=r aa.txt	u修改当前用户, g修改组内其他用户, o其他组用户权限，不写代表不修改。

chmod 755 a.txt	755为7，5，5分别代表每组用户的权限之和

**网络操作**

hostname	查看主机名

hostname xxx	临时修改主机名，下一次进入失效

​							 /etc/sysconfig/network文件	永久修改

​							 修改后为[rqiang@rqiang sysconfig] $ 

ifconfig	查看ip地址

ifconfig	enxxx	192.168.xxx.x	临时修改ip地址

​								BOOTPROTO=dhcp	自动获取ip

​								ONBOOT=yes	开机自动开启网络适配器

​							  修改 /etc/sysconfig/network-scripts/ifconfig-enxx文件
​							  TYPE=Ethernet
​							  PROXY_METHOD=none
​							  BROWSER_ONLY=no
​							  BOOTPROTO=none
​							  DEFROUTE=yes
​							  IPV4_FAILURE_FATAL=no
​							  IPV6INIT=yes
​							  IPV6_AUTOCONF=yes
​							  IPV6_DEFROUTE=yes
​							  IPV6_FAILURE_FATAL=no
​							  IPV6_ADDR_GEN_MODE=stable-privacy
​							  NAME=ensxx
​							  UUID=xxxxxxx
​							  DEVICE=ensxx
​							  ONBOOT=yes
​							  IPADDR=192.168.xxx.xxx
​							  PREFIX=24
​							  GATEWAY=192.168.xxx.xxx
​							  DNS1=8.8.8.8
​							  PEERDNS=no

service xxxx	xxx	对指定**服务**进行什么操作

service network restart	重启网络服务

​							  status	查看指定服务状态	stop/start 启动停止指定服务

serviced --status-all	查看系统所有后台服务

netstat -nltp	查看系统中网络进程的端口监听情况

vi /etc/hosts	相当于windows的**host**, 域名解析文件

​						 192.168.xxx.xxx 名称	

/etc/sysconfig/iptables	**防火墙**通过配置文件控制本机“出”“入”网络访问服务

service iptables status	查看防火墙状态

​							 stop/start	停止/启动防火墙

chkconfig iptables off	禁止防火墙自启

systemctl status firewalld.service	查看防火墙状态

systemctl stop firewalld.service	停掉防火墙

systemctl disable firewalld.service	开机不自启

**安装**

getconf LONG_BIT	查看计算机是32/64位

yum install xxx	网络安装

**文件传输**

使用**xftp**软件手动传输

yum install **lrzsz**	安装程序后，设置X/Y/Zmodem目录

​							     rz 上传，sz xxx 下载

**sftp** alt+p	直接进行linux和windows的交互

sftp> put e:/xxx	上传某个文件至当前用户操作目录	

sftp> get xxx	下载某个文件至windows文档目录

软件安装

java -version	查看linux自带或已安装的jdk版本

rpm -qa | grep java	查看jdk信息

rpm -e --nodeps java-xxx-xxx-xxx-xxx	卸载jdk

**配置环境变量**

vi /etc/profile	编辑配置文件

#set java environment	配置jdk环境
JAVA_HOME=/usr/local/jdk/jdk1.8.0_251
CLASSPATH=.:$JAVA_HOME/lib.tools.jar
PATH=$JAVA_HOME/bin:$PATH
export JAVA_HOME CLASSPATH PATH

source /etc/profile	加载配置文件

**Mysql安装**

rpm -ivh xxx	ivh中， i-install安装；v-verbose进度条；h-hash哈希校验

rpm -e xxx --nodeps	强制卸载，忽略依赖nodeps

mysqld --initialize --console	初始化mysql

chown -R mysql:mysql /var/lib/mysql	设置权限

systemctl start mysqld	初始化

cat /var/log/mysqld.log | grep localhost	查看初始密码

mysql -uroot -p 回车+初始密码	登录mysql

alter user 'root'@'localhost' identified by '123456';	在mysql界面修改初始密码

grant all privileges on *.* to 'root' @'%' identified by 'password';	开放远程访问权限, 刷新生效 flush privileges

service iptables stop	停掉防火墙

systemctl stop firewalld.service	停掉防火墙

https://blog.csdn.net/cjl836735455/article/details/112069647

https://www.bilibili.com/video/BV1qS4y1h77S?spm_id_from=333.337.search-card.all.click&vd_source=08d10ec13fe1fbc69be6c86b513435ab

**Tomcat**

./startup.sh	虚拟机ip:8080看到首页

**Zookeeper**

/opt/zookeeper/	安装至此目录

tar -zxvf apache-zookeeper-3.7.1-bin.tar.gz 	解压

cp zoo_sample.cfg zoo.cfg	修改conf下的zoo_sample.cfg为zoo.cfg配置文件

dataDir=/opt/zookeeper/zkdata	修改配置zookeeper的存储数据位置

vi	vi bin/zkEnv.sh	在该文件添加如下

​			export JAVA_HOME=/usr/local/jdk/jdk1.8.0_251

./zkServer.sh start/stop/status	bin目录下对zookeeper启动/停止/查看状态

