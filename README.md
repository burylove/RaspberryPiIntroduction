[TOC]

# 一、开始使用树莓派:
## 1. 操作系统的安装与启动:
#### 1.1 windows电脑烧录:
- 使用树莓派官网推荐的Win32 Disk Image
#### 1.2 Mac os X烧录:
- 首先,列出挂载的所有存储设备:
```shell
$diskutil list
```
- 找到对应的Micro SD卡设备,记录路径,使用dd命令吧镜像文件写入SD卡:(SD卡路径:/dev/disk3; 镜像路径: ./raspian.image)
```shell
$sudo dd if=/dev/disk3 of=./raspian.image
```
#### 1.3 linux烧录:
- 首先,列出挂载的所有存储设备:
```shell
$sudo fdisk -l
```
- 找到对应的Micro SD卡设备,记录路径,使用dd命令吧镜像文件写入SD卡:(SD卡路径:/dev/disk3; 镜像路径: ./raspian.image)
```shell
$sudo dd if=/dev/disk3 of=./raspian.image
```
#### 1.4 NOOBS:
NOOBS是一种更加简便的安装方式。NOOBS（New Out Of Box Software）是一个简便的操作系统安装程序。首先准备一个格式化为 FAT格式的Micro SD卡，然后把解压缩后的NOOBS文件直接复制到SD卡中即可。随后，将此卡插入树莓派中，即可根据图形化界面提醒安装 想要使用的操作系统。

## 2. scratch:
Scratch是由麻省理工学院开发的一款图形化编程软件。这个软件已经预装在Raspbian中，在"菜单"中找到后点 击它，就可以打开.

## 3. KTurtle:
这款软件有一个 图形化界面。整个界面分为左右两栏.我们通过左边填写的程序，来控制右栏小海龟的移动。移动的小海龟会在画面上留下行动的轨迹，从而绘制出各种各样的图形。在绘图过程中，小海龟不断移动，左侧程序栏中也会用黄色标明执行到哪一行了，非常有趣
- 下载安装:
```shell
$sudo apt-get update
$sudo apt-get install -y kturle
```
- 常见的控制海龟行动的命令如下:

|命令|说明|
|-|-|
|reset|清空画面。|
|pencolor|设置画笔颜色。|
|forward|小海龟前进，后面跟一个数字，表示前进的距离。 |
|backward|小海龟后退，后面跟一个数字，表示后退的距离。 |
|turnleft|左转，后面跟一个数字，表示左转的角度。 |
|turnright|右转，后面跟一个数字，表示右转的角度。 |
|go|让小海龟瞬移到某个位置。后面跟两个数字，表示位置。 |
|print|在屏幕上打印文字。|
|repeat|重复某些动作。后面跟数字和花括号，数字表示重复次数，而花括号中的内容表示重复的动作。|
|reset|清空画面(设置命令)。|
|pencolor|设置画笔颜色(设置命令)。|
|fontsize|设置字体大小(设置命令)。|

# 二、shell:
Linux提供了一种更易与树莓派互动的方式-----Shell
## 1. 常用命令:
### 1.1 通用查询命令:

|命令|说明|
|-|-|
|date|date用于日期时间的相关功能|
|lscpu|来查询CPU的信息|
|free -h|内存的使用状况(-h: h是human readable)|
|sudo fdisk -l|fdisk用于显示磁盘信息。选项-l表示列出所有磁盘|
|lsusb|所有的USB外设|
|uname -a|出操作系统的信息(-a: 所有相关信息)|
|echo $SHELL|查看shell类型|
|ifconfig|来查看网络接口|
*注: ifconfig*
> 其中eth0代表了以太网接口，wlan0代表了Wi-Fi接口，而lo是虚拟 出来的本地接口，用来表示本机。在连接上网的接口中，我们可以看到该接口的IP地址等信息。例如wlan0的IP地址是192.168.0.108。因为没有插网线，所以eth0并没有IP地址

### 1.2 树莓派专用查询命令:
vcgencmd命令，用于和树 莓派硬件直接互动
|命令|说明|
|-|-|
|vcgencmd measure_temp|将返回CPU的温度(temp=51.5℃)|
|vcgencmd measure_volts core|测量树莓派的核心电压(volt=1.2000v)|

### 1.3 如何了解一个陌生的命令:
每一个Linux系统都带有一套完善的文档用于解释每个命令的用途。你可以用下面三个命令来调用某个命令的文档信
- whatis:
    whatis命令的作用是用很简短的一句话来介绍命令。  
    ```shell
    $ whatis ls
    ```
- man:
    ```shell
    $ man ls
    ```
    man会返回命令的帮助手册.
- info:
    ```shell
    $ info ls
    ```
    info将返回更详细的帮助信息。    

### 1.4 shell小窍门:
- 命令补齐:
    - Tab键
- 文件名补齐:
    - Tab键
- 历史命令:
    ```shell
    $ history
    ```
- 终止与暂停:
    - 终止: Ctrl+C
    - 暂停: Ctrl+Z
# 三、编辑器:

## 1. 图形化的文本编辑器:
(没啥好记的)
## 2. nano:
### 2.1 启用:
```shell    
$ nano test.txt
```
nano后面跟着想要修改的文件名。如果当前文件夹下存在名为test.txt的文件，则该命令将打开这个文件。否则，命令nano会创建一 个新文件。

### 2.2 常用操作:
|操作|说明|
|-|-|
|Ctrl+O|保存文件|
|Ctrl+X|退出编辑, 关闭nano|
|M-\ |把光标移到文本开始。|
|M-/ |把光标移到文本结尾。|
|M-A|开始选择文本块。|
|^K|剪切所在行或选定的文本块。 |
|M-6|复制所在行或选定的文本块。|
|^U|粘贴。|
|^G|帮助。|
*注:*
在提示中，^表示Ctrl键，M表示Alt键。因此，^G表示的就是同时 按下Ctrl键和G键。下面是一些常用的功能键。 

### 2.3 语法高亮:
nano可以支持语法高亮，从而更好地服务于编程。为了使语法高 亮，首先要安装语法高亮文件
```shell
$ git clone https://github.com/nanorc/nanorc.git
$ cd nanorc
$ make install
```
安装完成后，可以看到~/.nano/syntax下多了很多语法高亮文件.
每个文件代表了对一种语言的语法高亮支持。比如python.nanorc， 就包含了对Python语言的语法高亮支持。将语法高亮文件添加 到~/.nanorc中，就能让nano启动对相应语言的语法高亮支持




