#### 绝对路径和相对路径

```bash
绝对路径
	以正斜杠开始
	完整的文件的位置路径
	可用于任何想指定一个文件名的时候
相对路径名
	不以斜线开始
	指定相对于当前目录或某目录的位置
	可以作为一个简短的形式指定一个文件名
基名：basename 
目录名：dirname
```

#### ls

```bash
列出当前目录的内容或指定目录
用法：ls [options][files_or_dirs]
示例：
ls -a :包含隐藏文件
ls -l:显示额外的信息
ls -R:目录地柜通过
ls -ld:目录和符号链接信息
ls -1:文件分行显示
ls -S:按从大到小排序
ls -t:按mtime排序
ls -u:配合-t选项，显示n并按atime从新到旧排序
ls -U:按目录存放顺序显示
ls -X:按文件后戳排序
```

#### 文件通配符

```bash
*：匹配零个或多个字符
?:匹配任何单个字符
~:当前用户家目录
~mang:用户mang家目录
~+:当前工作目录
~-:前一个工作目录
[0-9]:匹配数字范围
[a-z]:字母
[A-Z]:字母
[wang]:匹配列表中的任何的一个字符
[^wang]:匹配列表中所有字符以外的字符

预定义的字符类：#man 7 glob
[:digit:]:任意数字，相当于0-9
[:lower:]：任意大小写字母
[:upper:]:任意大写字母
[:alpha:]:任意大小写字母
[:alnum:]:任意数字或字母
[:blank:]:水平空白字符
[:space:]:水平或垂直空白字符
[:punct:]:标点符号
[:print:]:可打印字符
[:cntrl:]:控制(非打印字符)
[:graph:]:图形字符
[:xdigit:]:十六进制字符
/5/6/4-2-14
```

#### touch命令：

```bash
touch [OPTION]..FILE...
	-a 仅改变 atime和ctime
	-m 仅改变 mtime和ctime
	-t [[CC]YY]MMDDhhmm[.ss]
			指定atime和mtime的时间戳
	-c 如果文件不存在，则不予创建	
```

#### CP命令

```bash
cp [OPTION]...[-T]SOURCE DEST
cp [OPTION]...SOURCE...DIRECTORY
cp [OPTION]...-t DIRECTORY  SOURCE...
cp SRC  DEST
SRC 是文件：
	如果目标不存在：新建DEST，并将SRC中内容填充至DEST中
	如果目标存在：
			如果DEST是文件：将SRC中的内容覆盖至DEST中
				基于安全，建议为cp命令使用-i选项
			如果DEST是目录：在DEST下新建与原文件同名的文件，并将SRC中内容填充至新文件中	
-i：覆盖前提示  -n:不覆盖，注意两者顺序
-r,-R：递归赋值目录及内部的所有内容
-a：归档，相当于(备份)-dR --preserv=all
-d: --no-dereference --preserv=links 不复制原文件，只复制链接名
--preserv[=ATTR_LIST]
	mode :权限
	ownership:属主属组
	timestamp:
	links
	xattr
	context
	all
-p :等同于--preserv=mode,ownership,timestamp
-v: --verbose
-f:--force
```

#### mv命令

```bash
mv [OPTION]...[-T]SOURCE DEST
mv [OPTION]... SOURCE... DIRECTORY
mv [OPTION]... -t DIRECTORY  SOURCE...
常用选项：
	-i:交互式
	-f:强制

rename  '.txt' '.bak'  *.txt
#*.txt:当前目录下所有的txt文件，  .txt:重命名文件的后缀    .bak:新的后缀
```

#### rm命令

```bash
rm [OPTION]...FILE...
常用选项：
	-i:交互式
	-f:强制删除
	-r:递归删除
	--no-preserve-root
lsof /etc/test
#lsof：查看test哪个用户在使用
#正确删除大文件方式:
>test.txt
#删除文件使其难以恢复
shred -zuvn5 1.txt
```

#### 目录操作

```bash
tree 显示目录树
		-d:只显示目录
		-L level(1) :指定显示的层级数目
		-P pattern:只显示由指定pattern匹配到的路径
mkdir:创建目录
	-p:存在于不报错，且可自动创建所需的各目录
	-v:显示详细信息
	-m MODE:创建目录时直接指定权限
rmdir:删除空目录
	-p:递归删除父空目录
	-v:显示详细信息
rm -r:递归删除目录树
```

#### 确定文件内容

```bash
文件可以包含多种类型的数据
检查文件的类型，然后确定适当的打开命令或应用程序使用
file [options] <filename>....
常用选项：
	-b:列出文件辨识结果时，不显示文件名称
	-f filelist列出文件filelist中文件名的文件类型
	-F 使用指向分隔符号替换输出文件名后默认的“：”分隔符
	-L 查看对应软连接对应文件的文件类型
	--help 显示命令在线帮助
```

#### 用户和组的配置文件

```bash
Linux用户和组的主要配置文件
/etc/passwd:用户及其属性信息(名称、UID、主组ID等)
/etc/group:组及其属性信息
/etc/shadow:用户密码及其相关属性
/etc/gshadow：组密码及其相关属性
```

#### 用户创建

```bash
useradd [options] LOGIN
-u UID:[UID_MIN,UID_MAX]定义在/etc/login.defs
-o 配合-u选项，不检查UID的唯一性
-g GID:知名用户所属基本组，可为组名，也可以GID
-c "COMMENT":用户的注释信息
-d HOME_DIR:以指定的路径(不存在)为家目录
-s SHELL：指明用户的默认shell程序
	可用列表在/etc/shells文件中
-G GROUP1[GROUP2,...]：为用户指明福家族，组须事先存在
-N:不创建私用组做主组，使用users组做主组
-r:创建系统用户Centos 6 : id<500  , Centos7:ID<1000 
```

