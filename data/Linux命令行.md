<a id="catalog">目录</a>

[TOC]

# LINUX学习笔记（初期）

## 一、引言

[目录](#catalog)

### 1.1	笔记随想

​		今天，世界已经截然不同了。计算机遍布各个领域，从小手表到大型数据中心，及大小介于它们之间的每件东西。除了随处可见的计算机之外，人还有一个无处不在的连接所有计算机的网络。这已经开创了一个奇妙的，个人授权和创作自由的新时代，但是在过去的二三十年里，一些事情一直在发生着。

​		一个大公司不断地把它的管理权强加到世界上绝大多数的计算机上，并且决定用户对计算机的操作权力。幸运地是，来自世界各地的 $programuserr$，正积极努力地做些事情来改变这种境况。

​		通过编写自己的软件，$programuserr$ 一直在为维护电脑的管理权而战斗着，建设着 Linux。

### 1.2	这本笔记在做什么？

​		这本笔记是为了记录生存在 Linux 命令行的世界所需知识。主要记录 ubantu20.04的Linux 命令行相关知识。

### 1.3	笔记适用范围

​		这本笔记是笔者因从其它平台移民到 Linux 系统而记录的。完全是新手做的笔记，很难成体系。

​		幸好Markdown支持页内跳转，规划好锚点，应是可以观看复习，后期整理。



## 二、$Shell$​​ 的重要相关知识

[目录](#catalog)

### 2.1	终端仿真器

​		当使用图形用户界面时，需要另一个和 shell 交互的、叫做终端仿真器的程序。

​		在ubantu20.04，鼠标右键浏览一下菜单，会找到一个`在终端打开`。

​		虽然在菜单里它可能都被简单地称为“terminal”。

​		如果提示符的最后一个字符是“#”, 而不是“$”, 那么这个终端会话就有超级用户权限。
​		这意味着，以 root 用户的身份登录，或者是选择的终端仿真器提供超级用户（管理员）权限。

[目录](#catalog)

### 2.2	命令历史

​		试着键入字符吧。

​		在提示符下敲入一些像下面一样的乱七八糟的字符：`kaekfjaeifj`	

​		如果按**<font color=red>上箭头按键</font>**，或在ubantu的Linux终端输入`history`，会看到输入的命令重新出现在提示符之后。
这就叫做命令历史。		

​		按**<font color=red>下箭头按键</font>**，先前输入的命令就消失。

[目录](#catalog)

### 2.3	运行一些简单命令

​		第一个命令是 date。命令显示系统当前时间和日期。

```shell
user@linux:~$ date
2021年 07月 31日 星期六 23:00:14 CST
```

​		一个相关联的命令，cal，它默认显示当前月份的日历。

```shell
user@linux:~$ cal
      七月 2021         
日 一 二 三 四 五 六  
             1  2  3  
 4  5  6  7  8  9 10  
11 12 13 14 15 16 17  
18 19 20 21 22 23 24  
25 26 27 28 29 30 31         
```

​		查看磁盘剩余空间的数量，输入 df。

```shell
user@linux:~$ df
文件系统            1K-块       已用      可用 已用% 挂载点
udev              8071032          0   8071032    0% /dev
tmpfs             1624300       2452   1621848    1% /run
/dev/sda8        48951972   12449268  33986328   27% /
tmpfs             8121484       8476   8113008    1% /dev/shm
tmpfs                5120          4      5116    1% /run/lock
tmpfs             8121484          0   8121484    0% /sys/fs/cgroup
/dev/loop0          56832      56832         0  100% /snap/core18/1988
/dev/loop1         222208     222208         0  100% /snap/code/70
/dev/loop3         101888     101888         0  100% /snap/core/11420
```

​		同样地，显示空闲内存的数量，输入命令 free。

```shell
user@linux:~$ free
              总计         已用        空闲      共享    缓冲/缓存    可用
内存：    16242972     2417232     1781620      296276    12044120    13187392
交换：    19999740        2840    19996900
```

[目录](#catalog)

### 2.4	结束终端会话

​		可以通过关闭终端仿真器窗口，或者是在 shell 提示符下输入 exit 命令来终止一个终端会话。

```shell
user@linux:~$ exit
```

[目录](#catalog)

### 2.5	幕后控制台

​		即使终端仿真器没有运行，在后台仍然有几个终端会话运行着。它们叫做虚拟终端或者是虚拟控制台。

​		在大多数 Linux 发行版中，这些终端会话都可以通过按下 Ctrl-Alt-F1 到Ctrl-Alt-F6 访问。

​		**（笔者的ubantu是通过按下 Ctrl-Alt-F2 到Ctrl-Alt-F7 访问）**

当一个会话被访问的时候，它会显示登录提示框，人需要输入用户名和密码。要从一个虚拟控制台转换到另一个，按下 Alt 和 F1-F6（中的一个）。

​		**返回图形桌面，按下Alt-F7（笔者的ubantu是通过按下 Ctrl-Alt-F1）。**

## 三、文件系统中跳转

[目录](#catalog)

#### 重点

​		<font color=red>• pwd —打印出当前工作目录名</font>

​		<font color=red>• cd —更改目录</font>

<font color=red>		• ls —列出目录内容</font>

[目录](#catalog)

### 3.1	理解文件系统树

​		类似于 Windows，一个“类 Unix”的操作系统，比如说 Linux，以分层目录结构来组织所
有文件。这就意味着所有文件组成了一棵树型目录（有时候在其它系统中叫做文件夹），这个
目录树可能包含文件和其它的目录。文件系统中的第一级目录称为根目录。根目录包含文件和
子目录，子目录包含更多的文件和子目录，依此类推。
​		注意 (类 Unix 系统) 不像 Windows ，每个存储设备都有一个独自的文件系统。类 Unix 操
作系统，比如 Linux，总是只有一个单一的文件系统树，不管有多少个磁盘或者存储设备连接
到计算机上。根据负责维护系统安全的系统管理员的兴致，存储设备连接到（或着更精确些，
是挂载到）目录树的各个节点上。

[目录](#catalog)

### 3.2	当前工作目录

![image-20210801001357850](Linux命令行.assets/image-20210801001357850.png)

<center>图 1: 由图形化文件管理器显示的文件系统树</center>

​		如图 1 所示描述文件系统树的图形文件管理器。

​		注意，通常这是一棵倒置的树，也就是说，树根在最上面，而各个枝干在下面展开。

​		然而，命令行没有图片，所以人需要考虑用不同的方法，在文件系统树中跳转。

​		把文件系统想象成一个迷宫形状，就像一棵倒立的大树，人站在迷宫的中间位置。

​		在任意时刻，人处于一个目录里面，能看到这个目录包含的所有文件，以及通往上面目录（父目录）的路径，和下面的各个子目录。

​		<font color=red>人所在的目录则称为当前工作目录。</font>

​		使用pwd（print working directory(的缩写)）命令，来显示当前工作目录。

```shell
user@linux:$ pwd
/home/me
```

​		首次登录系统（或者启动终端仿真器会话）后，当前工作目录是我们的家目录。每个用户都有他自己的家目录，当用户以普通用户的身份操控系统时，家目录是唯一允许用户对文件进行写入的地方。

[目录](#catalog)

### 3.3	列出目录内容

​		列出一个目录包含的文件及子目录，使用 ls 命令。

```shell
user@linux:$ ls
公共的  视频  文档  音乐  NewDisk          snap
模板    图片  下载  桌面  PycharmProjects
```

​		实际上，用 ls 命令可以列出任一个目录的内容，而不只是当前工作目录的内容。

​		ls 命令还能完成许多事情。

[目录](#catalog)

### 3.4	更改当前工作目录

​		要更改工作目录（此刻站在树形迷宫里面），用 cd 命令。

​		输入 cd， 然后输入想要去的工作目录的路径名。路径名就是沿着目录树的分支到达想要的目录期间所经过的路线。

​		路径名可通过两种方式来指定，一种是绝对路径，另一种是相对路径

[目录](#catalog)

### 3.5	绝对路径

​		绝对路径开始于根目录，紧跟着目录树的一个个分支，一直到达所期望的目录或文件。

​		例如，系统中有一个目录，大多数系统程序都安装在这个目录下。

​		这个目录的路径名是/usr/bin。它意味着从根目录（用开头的“/``表示）开始，有一个叫''usr'' 的目录包含了目录"bin”。

```shell
user@linux:~$ cd /usr/bin
user@linux:/usr/bin$ pwd
/usr/bin
user@linux:/usr/bin$ ls
...Listing of many, many files ...
```

​		把工作目录转到/usr/bin 目录下，里面装满了文件。

​		注意 shell 提示符的改变，为了方便，通常终端提示符自动显示工作目录名。

[目录](#catalog)

### 3.6	相对路径

<a id="3.6">联动4.1	ls乐趣</a>

​		绝对路径从根目录开始，直到它的目的地，而相对路径开始于工作目录。

​		为了做到这个（用相对路径表示），在文件系统树中用一对特殊符号来表示相对位置。

​		这对特殊符号是 “<font color=red>.</font>”(点) 和 “<font color=red>..</font>” (点点)

​		符号 “.” 指的是工作目录，”..” 指的是工作目录的父目录。

​		把工作目录切换到/usr/bin：

```shell
user@linux:/usr/bin$ cd /usr/bin
user@linux:/usr/bin$ pwd
/usr/bin
```

​		比方说想更改工作目录到/usr/bin 的父目录/usr。

​		可以通过两种方法来实现。

​		可以使用绝对路径名：

```shell
user@linux:/usr/bin$ cd /usr
user@linux:/usr$ pwd
/usr
```

​		或者，也可以使用相对路径：

```shell
user@linux:/usr$ cd /usr/bin
user@linux:/usr/bin$ cd ..
user@linux:/usr$ pwd
/usr
```

​		同样地，从目录/usr/ 到/usr/bin 也有两种途径。

​		可以使用绝对路径：

```shell
user@linux:/usr$ cd /usr/bin
user@linux:/usr/bin$ pwd
/usr/bin
```

​		或者，也可以使用相对路径：

```shell
user@linux:/usr$ cd ./bin
user@linux:/usr/bin$ pwd
/usr/bin
```

​		有一件很重要的事，必须指出来：在几乎所有的情况下，可以省略 “./”。

​		它是隐含地输入：

```shell
user@linux:/usr/bin$ cd /usr
user@linux:/usr$ cd bin
user@linux:/usr/bin$ pwd
/usr/bin
```

[目录](#catalog)

### 3.7	有用的快捷键

​		在表 3-1 中，列举出了一些快速改变当前工作目录的有效方法。

![image-20210801062936388](Linux命令行.assets/image-20210801062936388.png)

### 3.8	关于文件名的重要规则

1. **以 “.” 字符开头的文件名是隐藏文件。这仅表示，ls 命令不能列出它们，用 ls-a 命令就可以了。当你创建帐号后，几个配置帐号的隐藏文件被放置在你的家目录下。稍后，我们会仔细研究一些隐藏文件，来定制你的系统环境。另外，一些应用程序也会把它们的配置文件以隐藏文件的形式放在你的家目录下面。**
2. **文件名和命令名是大小写敏感的。文件名“File1”和“file1”是指两个不同的文件名。**
3. **Linux 没有“文件扩展名”的概念，不像其它一些系统。可以用你喜欢的任何名字来给文件起名。文件内容或用途由其它方法来决定。虽然类 Unix 的操作系统，不用文件扩展名来决定文件的内容或用途，但是有些应用程序会。**
4. **虽然 Linux 支持长文件名，文件名可能包含空格，标点符号，但标点符号仅限使用“.”，“－”，下划线。最重要的是，不要在文件名中使用空格。如果你想表示词与词间的空格，用下划线字符来代替。过些时候，你会感激自己这样做。**



## 四、探究操作系统

[目录](#catalog)

#### 重点

<font color=red>• ls —列出目录内容</font>

<font color=red>• file —确定文件类型</font>

<font color=red>• less —浏览文件内容</font>

### 4.1	$ls$ 乐趣

​		ls 可能是用户最常使用的命令。

​		通过它，可以知道目录的内容，以及各种各样重要文件和目录的属性。

​		只要简单的输入 ls 就能看到在当前目录下所包含的文件和子目录列表。

```shell
user@linux:~$ ls
公共的  视频  文档  音乐  NewDisk          snap
模板    图片  下载  桌面  PycharmProjects
```

​		除了当前工作目录以外，也可以指定要列出内容的目录，就像这样：

```shell
user@linux:~$ ls /usr
bin    include  lib32  libexec  local  share
games  lib      lib64  libx32   sbin   src
```

​		甚至可以列出多个指定目录的内容。

​		在这个例子中，将会列出用户家目录（用字符“∼”代表）和/usr 目录的内容：

```shell
user@linux:~/NewDisk$ ls ~ /usr
/home/user:
公共的  视频  文档  音乐  NewDisk          snap
模板    图片  下载  桌面  PycharmProjects

/usr:
bin    include  lib32  libexec  local  share
games  lib      lib64  libx32   sbin   src
```

​		还有些与第三节[联动用法](#3.6)：

```shell
user@linux:~/NewDisk$ ls ~/NewDisk/py
方程求解      有限元MATLAB程序编写  python作图
计算流体力学  有限元Python程序编写  venv
漫画python    python视频下载        vscode_python
user@linux:~/NewDisk$ ls ../learning_materials
ls: 无法访问 '../py': 没有那个文件或目录
user@linux:~/NewDisk$ ls  ./learning_materials
'basis of computer engineering'   CSDN             MATLAB_mathematical_modeling
 CFD                              finite_element   python
 crawler                          Linux_book      'system dynamics'
```

​		也可以改变输出格式，来得到更多的细节：

```shell
user@linux:~/NewDisk$ ls -l
总用量 24
drwxrwxr-x 11 user user  4096 8月   1 05:42 learning_materials
drwx------  2 root     root     16384 7月  31 07:43 lost+found
drwxrwxrwx 12 user user  4096 7月  31 08:44 py
```

​		使用 ls 命令的“-l”选项，则结果以长模式输出。

[目录](#catalog)

### 4.2	选项和参数

​		命令名经常会带有一个或多个用来更正命令行为的选项，更进一步，选项后面会带有一个或多个参数，这些参数是命令作用的对象。

​		所以大多数命令看起来像这样：

```shell
command -option arguments
```

​		大多数命令使用的选项，是由一个中划线加上一个字符组成。

​		例如，“-l”，但是许多命令，包括来自于 GNU 项目的命令，也支持长选项。

​		长选项由两个中划线加上一个字组成。

​		当然，许多命令也允许把多个短选项串在一起使用。

​		下面这个例子，ls 命令有两个选项，“l”选项产生长格式输出，“t”选项按文件修改时间的先后来排序。

```
user@user:~$ ls -lt
总用量 44
drwxr-xr-x 4 user user 4096 8月   1 18:53 图片
drwxrwxrwx 5 root     root     4096 8月   1 05:23 NewDisk
drwxr-xr-x 3 user user 4096 7月  31 16:26 音乐
drwxr-xr-x 7 user user 4096 7月  31 11:49 snap
drwxr-xr-x 2 user user 4096 7月  31 10:44 下载
drwxrwxr-x 3 user user 4096 7月  30 23:53 PycharmProjects
drwxr-xr-x 3 user user 4096 7月  30 23:12 桌面
drwxr-xr-x 2 user user 4096 7月  30 12:10 模板
drwxr-xr-x 2 user user 4096 7月  30 10:28 公共的
drwxr-xr-x 2 user user 4096 7月  30 10:28 视频
drwxr-xr-x 2 user user 4096 7月  30 10:28 文档
```

​		加上长选项“–reverse”，则结果会以相反的顺序输出：

```shell
user@user:~$ ls -lt --reverse 
总用量 44
drwxr-xr-x 2 user user 4096 7月  30 10:28 文档
drwxr-xr-x 2 user user 4096 7月  30 10:28 视频
drwxr-xr-x 2 user user 4096 7月  30 10:28 公共的
drwxr-xr-x 2 user user 4096 7月  30 12:10 模板
drwxr-xr-x 3 user user 4096 7月  30 23:12 桌面
drwxrwxr-x 3 user user 4096 7月  30 23:53 PycharmProjects
drwxr-xr-x 2 user user 4096 7月  31 10:44 下载
drwxr-xr-x 7 user user 4096 7月  31 11:49 snap
drwxr-xr-x 3 user user 4096 7月  31 16:26 音乐
drwxrwxrwx 5 root     root     4096 8月   1 05:23 NewDisk
drwxr-xr-x 4 user user 4096 8月   1 18:53 图片
```

​		ls 命令有大量的选项。表 4-1 列出了最常使用的选项。

![image-20210801191525937](Linux命令行.assets/image-20210801191525937.png)

[目录](#catalog)

### 4.3	深入研究长格式输出

​		"-l"选项导致 ls 的输出结果以长格式输出。

​		这种格式包含大量的有用信息。

​		下面的例子目录来自于 Ubuntu 系统：

```shell
drwxr-xr-x 2 user user 4096 7月  30 10:28 文档
drwxr-xr-x 2 user user 4096 7月  30 10:28 视频
drwxr-xr-x 2 user user 4096 7月  30 10:28 公共的
drwxr-xr-x 2 user user 4096 7月  30 12:10 模板
drwxr-xr-x 3 user user 4096 7月  30 23:12 桌面
-rw-r--r-- 1 root root 32059 2007-04-03 11:05 oo-cd-cover.odf
-rw-r--r-- 1 root root 159744 2007-04-03 11:05 oo-derivatives.doc
-rw-r--r-- 1 root root 27837 2007-04-03 11:05 oo-maxwell.odt
-rw-r--r-- 1 root root 98816 2007-04-03 11:05 oo-trig.xls
-rw-r--r-- 1 root root 453764 2007-04-03 11:05 oo-welcome.odt
-rw-r--r-- 1 root root 358374 2007-04-03 11:05 ubuntu Sax.ogg
```

​		选一个文件，来看一下各个输出字段的含义：

![3](Linux命令行.assets/3.png)

[目录](#catalog)

### 4.4	确定文件类型

​		将用 file 命令来确定文件的类型。

​		在 Linux 系统中，并不要求文件名来反映文件的内容。

​		然而，一个类似“picture.jpg”的文件名，一般会期望它包含 JPEG 压缩图像，但 Linux 却不这样要求它。

​		可以这样调用 file 命令：`file filename`

​		当调用 file 命令后，file 命令会打印出文件内容的简单描述。例如：	

​		

```
user@linux:~$ cd ./图片
user@linux:~/图片$ ls
1.jpeg  2000张  2..jpeg  3.png  screen_shot
user@linux:~/图片$ file 3.png
3.png: PNG image data, 589 x 451, 8-bit/color RGB, non-interlaced
```

​		有许多种类型的文件。

​		事实上，在类 Unix 操作系统中比如说 Linux 中，有个普遍的观念就是“一切皆文件”。

[目录](#catalog)

### 4.5	用 less 浏览文件内容

​		less 命令是一个用来浏览文本文件的程序。

​		纵观 Linux 系统，有许多人类可读的文本文件。less 程序为检查文本文件提供了方便。

```html
	什么是“文本”
	在计算机中，有许多方法可以表达信息。所有的方法都涉及到，在信息与一些数字之间确立一种关系，而这些数字可以用来代表信息。毕竟，计算机只能理解数字，这样所有的数据都被转换成数值来表示。
	有些数值表达法非常复杂（例如压缩的视频文件），而其它的就相当简单。最早也是最简单的一种表达法，叫做 ASCII 文本。ASCII（发音是 “As-Key”）是美国信息交换标准码的简称。这是一个简单的编码方法，它首先被用在电传打字机上，用来实现键盘字符到数字的映射。
	文本是简单的字符与数字之间的一对一映射。它非常紧凑。五十个字符的文本翻译成五十个字节的数据。文本只是包含简单的字符到数字的映射，理解这点很重要。它和一些文字处理器文档不一样，比如说由微软和 OpenOffice.org 文档编辑器创建的文件。这些文件，和简单的 ASCII 文件形成鲜明对比，它们包含许多非文本元素，来描述它的结构和格式。普通的 ASCII 文件，只包含字符本身，和一些基本的控制符，像制表符，回车符及换行符。纵观 Linux 系统，许多文件以文本格式存储，也有许多 Linux 工具来处理文本文件。甚至 Windows 也承认这种文件格式的重要性。著名的 NOTEPAD.EXE 程序就是一个 ASCII 文本文件编辑器。
```

​		许多包含系统设置的文件（叫做配置文件），是以文本格式存储的，阅读它们可以更深入的了解系统是如何工作的。

​		另外，许多系统所用到的实际程序（叫做脚本）也是以这种格式存储的。

​		学习怎样编辑文本文件，可以做到修改系统设置，编写自己的脚本文件.
​		less 命令是这样使用的：`less filename`

​		一旦运行起来，less 程序允许用户前后滚动文件。

​		例如，要查看一个定义了系统中全部用户身份的文件，输入以下命令：

```shell
user@linux:~/图片$ less /etc/passwd
```

​		一旦 less 程序运行起来，用户就能浏览文件内容了。

​		如果文件内容多于一页，那么用户可以上下滚动文件。

​		按下“q”键，退出 less 程序。

​		下表列出了 less 程序最常使用的键盘命令：

<img src="Linux命令行.assets/IMG_20210801_201707.jpg" alt="IMG_20210801_201707" style="zoom:20%" />

​		less 程序是早期 Unix 程序 more 的改进版。

​		less 属于 “页面调度器” 程序类，这些程序允许通过页方式，在一页中轻松地浏览长长的文本文档。然而 more 程序只能向前分页浏览，而 less 程序允许前后分页浏览，它还有很多其它的特性。

[目录](#catalog)

### 4.6		Linux系统空间旅行指南

​		Linux 系统中，文件系统布局与类 Unix 系统的文件布局很相似。实际上，一个已经发布的标准，叫做 Linux 文件系统层次标准，详细说明了这种设计模式。不是所有 Linux 发行版都根据这个标准，但大多数都是。

​		下一步，在文件系统中游玩，来了解 Linux 系统的工作原理。

​		发现很多有趣的文件都是普通的可读文本。

​		将开始旅行，记住以下常用命令和游玩操作：

​		<font color=red>1. cd 到给定目录</font>

<font color=red>		2. 列出目录内容 ls -l</font>

​		<font color=red>3. 如果看到一个有趣的文件，用 file 命令确定文件内容</font>

<font color=red>		4. 如果文件看起来像文本，试着用 less 命令浏览它</font>

​		表 4-4 列出了一些用户可以浏览的目录：

<img src="Linux命令行.assets/IMG_20210801_204044.jpg" style="zoom: 53%;" />

[目录](#catalog)

### 4.8	符号链接

​		到处查看时，可能会看到一个目录，列出像这样的一条信息：

```shell
lrwxrwxrwx 1 root root 11 2007-08-11 07:34 libc.so.6 -> libc-2.6.so
```

​		注意看，这条信息第一个字符是“l”，并且有两个文件名。

​		这是一个特殊文件，叫做符号链接（也称为软链接或者 symlink ）。

​		在大多数“类 Unix”系统中，有可能一个文件被多个文件名所指向。虽然这种特性的意义并不明显，但它真地很有用。

​		描绘一下这样的情景：一个程序要求使用某个包含在名为“foo”文件中的共享资源，但是foo”经常改变版本号。这样，在文件名中包含版本号，会是一个好主意，因此管理员或者其它相关方，会知道安装了哪个“foo”版本。

​		这又会导致一个问题。如果更改了共享资源的名字，那么必须跟踪每个可能使用了这个共享资源的程序，当每次这个资源的新版本被安装后，都要让使用了它的程序去寻找新的资源名。这听起来就很麻烦。

​		这就是符号链接存在至今的原因。比方说，安装了文件“foo”的 2.6 版本，它的文件名是“foo-2.6”，然后创建了叫做“foo”的符号链接，这个符号链接指向“foo-2.6”。这意味着，当一个程序打开文件“foo”时，它实际上是打开文件“foo-2.6”。大大简化了上面的问题。

​		依赖于“foo”文件的程序能找到这个文件，并且能知道安装了哪个文件版本。当升级到“foo-2.7”版本的时候，仅添加这个文件到文件系统中，删除符号链接“foo”，创建一个指向新版本的符号链接。这不仅解决了版本升级问题，而且还允许在系统中保存两个不同的文件版本。

​		假想“foo-2.7”有个错误，那得回到原来的版本。一样的操作，只需要删除指向新版本的符号链接，然后创建指向旧版本的符号链接就可以了。

​		在上面列出的目录（来自于 Fedora 的/lib 目录）展示了一个叫做“libc.so.6”的符号链接，这个符号链接指向一个叫做“libc-2.6.so”的共享库文件。这意味着，寻找文件“libc.so.6”的程序，实际上得到是文件“libc-2.6.so”。



## 五、操作文件和目录

[目录](#catalog)

#### 重点

​		<font color=red>• cp —复制文件和目录</font>

<font color=red>		• mv —移动/重命名文件和目录</font>

​		<font color=red>• mkdir —创建目录</font>

​		<font color=red>• rm —删除文件和目录</font>

<font color=red>		• ln —创建硬链接和符号链接</font>

##  5.1	通配符

​		因为 shell 频繁地使用文件名，shell 提供了特殊字符来帮助你快速指定一组文件名。这些特殊字符叫做通配
符。使用通配符（也以文件名代换著称）允许你依据字符类型来选择文件名。

​		下表列出这些通配符以及它们所选择的对象：

![image-20210801212937848](Linux命令行.assets/image-20210801212937848.png)

​		表 5-2 列出了最常使用的字符类：

![image-20210801213007632](Linux命令行.assets/image-20210801213007632.png)

​		借助通配符，为文件名构建非常复杂的选择标准成为可能。

​		下面是一些类型匹配的范例：

![image-20210801213052210](Linux命令行.assets/image-20210801213052210.png)

​		接受文件名作为参数的任何命令，都可以使用通配符。

[目录](#catalog)

### 5.2	mkdir 创建目录

​		mkdir 命令是用来创建目录的。它这样工作：

```shell
mkdir directory...
```

​		注意表示法：在描述一个命令时（如上所示），当有三个圆点跟在一个命令的参数后面，这意味着那个参数可以重复，就像这样：

```shell
mkdir dir1
```

​		会创建一个名为 “dir1” 的目录，而

```shell
mkdir dir1 dir2 dir3
```

​		会创建三个目录，名为 dir1, dir2, dir3。

[目录](#catalog)

### 5.3	cp 复制文件和目录

​		cp 命令，复制文件或者目录。它有两种使用方法：

```shell
cp item1 item2
```

​		复制【单个文件或目录 “item1”】<font color=red>到</font>【文件或目录”item2”】，和：

```shell
cp item... directory
```

​		复制【多个项目（文件或目录）】<font color=red>到</font>【一个目录】下。

​		这里列举了 cp 命令一些有用的选项（短选项和等效的长选项）：

<img src="Linux命令行.assets/IMG_20210801_214806.jpg" alt="IMG_20210801_214806" style="zoom:23%;" />

![image-20210801214923771](Linux命令行.assets/image-20210801214923771.png)

[目录](#catalog)

### 5.4	mv 移动和重命名文件

​		mv 命令可以执行文件移动和文件命名任务，这依赖于你怎样使用它。

​		任何一种情况下，完成操作之后，原来的文件名不再存在。

​		mv 使用方法与 cp 很相像：

```shell
mv item1 item2
```

​		把【文件或目录“item1”】<font color=red>移动或重命名为</font>【“item2”】, 或者：

```shell
mv item... directory
```

​		把【一个或多个条目】<font color=red>从</font>【一个目录】<font color=red>移动到</font>【另一个目录中】。

​		mv 与 cp 共享了很多一样的选项：

![image-20210801215240068](Linux命令行.assets/image-20210801215240068.png)

![image-20210801215256667](Linux命令行.assets/image-20210801215256667.png)

### 5.5	rm 删除文件和目录

​		rm 命令用来移除（删除）文件和目录：

```shell
rm item...
```

​		“item” 代表一个或多个文件或目录。

​		下表是一些普遍使用的 rm 选项和实例：

![image-20210801215408828](Linux命令行.assets/image-20210801215408828.png)

![image-20210801215430906](Linux命令行.assets/image-20210801215430906.png)

```html
	谨慎使用 rm!
	类 Unix 的操作系统，比如说 Linux，没有复原命令。一旦你用 rm 删除了一些东西，它就消失了。
	尤其要小心通配符。思考一下这个经典的例子。
	假如说，只想删除一个目录中的 HTML 文件。输入：rm *.html
	这是正确的，如果不小心在“*”和“.html”之间多输入了一个空格，就像这样：rm * .html
	这个 rm 命令会删除目录中的所有文件，还会警报没有文件叫做“.html”。
	无论什么时候，rm 命令用到通配符（除了仔细检查输入的内容外！），用 ls 命令来测试通配符。
	这会看到要删除的文件列表。然后按下上箭头按键，重新调用刚刚执行的命令，用 rm 替换 ls。
```

### 5.6 ln 创建链接

