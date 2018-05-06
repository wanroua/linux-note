####  date显示日期和时间

```bash
Linux的两种时钟
系统时钟：由Linux内核通过CPU的工作频率进行的
硬件时钟：主板
hwclock,clock:显示硬件时钟
	-s, --hctosys 以硬件时钟为准，校正系统时钟
	-w, --systohc 以系统时钟为准，校正硬件时钟
时区：/etc/localtime
存放时区目录：/usr/share/zoneinfo 
查看所有时区：timedatectl  list-timezones 
设置时区：timedatectl set-timezone Asia/Shanghai
year month day
#年   月    日
```

#### 关机

```bash
关机：halt , poweroff
重启：reboot
	-f:强制，不调用shutdown
	-p:切断电源
关机或重启：shutdown
	shutdown [OPTION].... TIME[MESSAGE]
	-r: reboot
	-h: halt
	-c: cancel
	TIME:无指定，默认相当于+1
		now: 立刻，相当于+0
		+m: 相对时间表示法，几分钟之后：例如+3
		hh:mm: 绝对时间表示，知名具体时间
```

#### screen

```bash
 screen命令：
	创建新screen会话
		screen -S [会话名称]
	加入screen会话
		screen -x [会话名称]
	退出并关闭screen会话
		exit
	剥离当前screen会话
		Ctrl+a,d
	显示所有已经打开的screen会话
		screen -ls
	恢复某screen会话
		screen -r [会话名称]
	删除一个会话
		screen  -X -S [会话编号] quit
```

#### echo

```bash
echo命令：
功能：显示字符
语法：echo[-neE][字符串]
说明：echo会将输入的字符串送往标准输出。输出的字符串间以空白字符隔开，并在最后加上换行符号
选项：
	—E: (默认不支持)\解释功能
	-n: 不自动换行
	-e：启用\字符的解释功能
显示变量
	echo "$VAR_NAME" 变量会替换，弱引用
	echo '$VAR_NAME' 变量不会替换，强引用 

启用命令选项-e，若字符串中出现以下字符，则特别加以处理，而不会将它当成一般文字输出
\a：发出警告声
\b:退格键
\c:最后不加上换行符号
\n:换行且光标移至行首
\r:回车，即光标移至行首，但不换行
\t:插入tab
\\插入\\字符
\Onnn插入nnn(八进制)所代表的ASCII字符
```

#### whatis

```bash
显示命令的剪短描述
使用数据库
刚安装后不可立即使用
makewhatis(centos6) | mandb(centos7)制作数据库
使用实例：
	whatis ls 或 man -f ls
```

#### 帮助命令

```bash
内部命令：help COMMAND
		man bash
外部命令：(1)COMMAN --help
		   COMMAND -h
		(2)使用手册(manual)
			man COMMAND
		(3)信息页
			info COMMAND
		(4)程序自身的帮助文档
			README
			INSTALL
			ChangeLog
		(5)程序官方文档
			官方站点：Documentation
		(6)发行版的官方文档
		(7)Google
#5/5/3-2
```

#### man

```bash
提供命令帮助的文件
手册页存放在/usr/share/man
几乎每个Ingles都有man的“页面”
man页面分组为不同的"zhangjie "
统称为Linux手册
man命令的配置文件：/etc/man.config | man_db.conf
	MANPATH /PATH/TO/SOMEWHERE:指明man文件搜索位置
man -M /PATH/TO/SOMEWHERE COMMAND :到指定位置下搜索
COMMAND命令的手册页并显示
中文man需要安装包man-pages-zh-CNw

man帮助段落说明
NAME：名称及简要说明
SYNOPSIS：用法格式说明
[] :可选内容
<> :必选内容
a|b:二选一
{} :分组
...:同一内容可出现多次
DESCRIPTION：详细说明
OPTIONS：选项说明
EXAMPLES：示例
FILES：相关文件
AUTHOR：作者
COPYRIGHT：版本信息
REPORTING：BUGS bug信息
SEE ALSO：其它帮助参考

参看man手册页
	man [章节号] keyword
列出所有帮助
	man -a keyword
搜索man手册
	man -k keyword ：列出所有匹配的页面
	使用whatis 数据库
相当于whatis
	man -f keyword
打印man帮助文件的路径
	man -w [章节] keyword
	
网站和搜索
http://tldp.org
http://www.slideshare.net
http://www.google.com
	openstack  filetype:pdf
	rhca site:redhat.com/docs
```

#### 命令行历史

```bash
重复前一个命令，有4中方法
重复前一个命令使用上下方向键，并回车执行
按!!并回车执行
输入!-1并回车执行
按Ctrl+p并回车执行
!:0执行前一条命令(去除参数)
Ctrl+n显示当前历史中的下一条命令，但不执行
Ctrl+j执行当前命令
!n执行history命令输出对应序列号n的命令
!-n执行history历史中倒数第n个命令

history:
-c：清空命令历史
-d offset:删除历史中指定的第offset个命令
n:显示最近的n条历史
-a:追加本次会话新执行的命令历史列表至历史文件
-n:读历史文件中未度过的行到历史列表
-r:读历史文件中附加到历史列表
-w:保存历史列表到指定的历史文件
-p:展开历史参数成多行，但不存在历史列表中
-s:展开历史参数成一行，附加在历史列表后

echo $HISTSIZE
/etc/profile

命令历史相关环境变量
HISTSIZE：命令历史记录的条数
HISTFILE:指定历史文件，默认为~/.bash_history
HISTFILESIZE：命令历史文件记录历史的条数
HISTTIMEFORMAT=“%F %T”：显示时间
HISTIGNORE="str1:str2*:..."忽略str1命令，str2开头的历史
控制命令历史的记录方式：
环境变量：HISTCONTROL
	ignoredups 默认，忽略重复的命令，连续且相同为“重复”
	ignorespace 忽略所有以空白开头的命令
	ignoreboth 相当于ignoredups,ignorespace的组合
	erasedups  删除重复命令
export 变量名="值"
存放在/etc/profile或~/.bash_profile 
```

#### bash的快捷键

```bash
Ctrl + a 光标移到命令行首，相当于Home
Ctrl + e 光标移动到命令行尾，相当于end
Ctrl + f 光标向右移动一个字符
Ctrl + b 光标向左移动一个字符
Ctrl + xx 光标在命令行首和光标之间移动
Ctrl + u 从光标处删除至命令行首
Ctrl + k 从光标处删除至命令行尾
Alt + f 光标向右移动一个单词尾
Alt + b 光标向左移动一个单词尾
Alt + r 删除当前整行
```

#### 命令历史回放

```bash
script -t  2> time.log  -a  cmd.log
#-t：时间 ，-a:命令文件
scriptreplay  time.log  cmd.log 
#播放，需要用到时间日志和命令日志
```

##### 虚拟机触发新添加的磁盘

```bash
echo '- - -' > /sys/class/scsi_host/host2/scan
```

#### 文件系统结构

```bash
/boot:引导文件存放目录，内核文件(vmlinuz)、引导加载器(bootloader,grub)都存放于此目录
/bin:供所有用户使用的基本命令，不能关联至独立分区，OS启动即会用到的程序
/sbin:管理类的基本命令，不能关联至独立分区，OS启动即会用到的程序
/lib:启动时程序依赖的基本共享库文件以及内核模块文件(/lib/modules)
/lib4:专用于x86_64系统上的辅助共享库文件存放位置
/etc:配置文件目录
/home/USERNAME:普通用户家目录
/root:管理员的家目录
/media:便携式移动设备挂载点
/usr:
	bin:保证系统拥有完整功能而提供的应用程序
	sbin:
	lib:32位使用
	lib64:只存在64位系统
	include:C程序的头文件(header files)
	share:结构化独立的数据，例如：doc,man等
	local:第三方应用程序的安装位置
		bin  sbin lib lib64  etc share

 /var:
 cache:应用程序缓存数据目录
 lib:应用程序状态信息数据
 local:专用于为/usr/local/下的应用数据程序存储可变数据
 lock:锁文件
 log:日志目录及文件
 opt:专用于为/opt下的应用程序存储可变数据
 run:运行中的进程相关数据，通常用于存储进程pid文件
 spool:应用程序数据池
 tmp:保存系统两次重启之间产生的临时数据
 /proc:用于输出内核进程信息相关的虚拟文件系统
 /sys:用于输出当前系统上硬件设备相关信息虚拟文件系统
 /selinux:security enhanced Linux,selinux相关的安全策略等信息的存储位置
 二进制程序：/bin /sbin /usr/bin  /usr/sbin
 /usr/local/bin/  /usr/local/sbin
 库文件：/lib, /lib64,/usr/lib, /usr/lib64
 /usr/local/lib  /usr/local/lib64
 配置文件：/etc, /etc/DIRECTORY，/usr/local/etc
 帮助文件：/usr/share/man, /usr/share/doc
 /usr/local/share/man , /usr/local/share/doc
```

