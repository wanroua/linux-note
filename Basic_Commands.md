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

