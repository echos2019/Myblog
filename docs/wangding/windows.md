# windows基本操作

## DOS基本命令与批处理

### DOS命令
- /?可以查询命令flag用法

- md 创建文件夹
  
- cls 清空

- attrib 修改属性 +h加隐藏(dir 看不到) +s提升至系统保护文件 +a加只读，减号相反

- dir 显示目录

- shutdown 关机等操作，-s -t 200，200秒后关机，-a恢复

- cd定位文件夹

- copy拷贝 copy \abc\b\haha.txt .\(从第一个目录到第二个目录)

- move移动。类似拷贝

- ping 

    Ping命令是专用于TCP/IP协议的探测工具，它对测试网络连接状况以及信息包发送和接收状况非常有用，这是TCP/IP协议中最有用的命令之一。它给另一个系统发送一系列的数据包，该系统本身又发回一个响应，这条实用程序对查找远程主机很有用，它返回的结果表示是否能到达主机，宿主机发送一个返回数据包需要多长时间。

    -t表示将不间断向目标IP发送数据包，直到我们强迫其停止。

    -1定义发送数据包的大小，默认为32字节，我们利用它可以最大定义到65500字节。-n定义向目标IP发送数据包的次数，默认为3次。如果网络速度比较慢，3次对我们来说也浪费了不少时间，因为我们的目的仅仅是判断目标IP是否存在，那么就定义为一次吧。

    说明一下，如果-t参数和-n参数一起使用，ping命令就以放在后面的参数为标准，比如“ping IP-t-n3”，虽然使用了-t参数，但并不是一直ping下去，而是只ping3次。另外，ping命令不一定非得ping IP，也可以直接ping主机域名，这样就可以得到主机的IP。

- netstat命令：
  
    这是一个用来查看网络状态的命令，操作简便功能强大。

    -a查看本地机器的所有开放端口，可以有效发现和预防木马，可以知道机器所开的服

    -r列出当前的路由信息，告诉我们本地机器的网关、子网掩码等信息。

    -n以数字形式显示地址和端口号

- ipconfig命令：
  
    ipconfig可用于显示当前的TCP/IP配置的设置值

    ipconfig/a11：显示本机TCP/IP配置的详细信息；

    ipconfig/release:DHCP客户端手工释放IP地址；

    ipconfig/renew:DHCP客户端手工向服务器刷新请求；

    ipconfig/flushdns：清除本地DNS缓存内容；ipconfig/displaydns：显示本地DNS内容；

### 批处理

.bat文件可以批处理

- echo  显示命令，例：
    ```bat
    @echo off ::关闭回显，即关闭命令行的执行，直接显示结果%
    echo ===================
    echo hello
    pause ::让命令框暂停，防止一闪即过
    ```
- :  区块的开始,只是区分区块，配合goto命令完成跳转
    ```bat
    ::下面程序在系统打开时直接开始快速堆叠命令行框
    copy doc.bat %userprofile%\开始菜单\程序\启动
    :a
    start ::显示命令行
    goto a
    ```
- title 修改命令框名字
- %num% 得到num的值
- \p 得到用户输入结果
- set  设定变量
    ```bat
    @echo off 
    title 小程序
    color 0a
    :menu 
    cls 
    echo ============= 
    echo 菜单
    echo 1，定时关机
    echo 2.取消定时
    echo 3.退出
    echo =============
    set/p nun=your choice：
    if"%num%"=="1"goto 1
    if"%num%："=="2"goto 2
    if"%num%"=="3"goto 3
    :1
    set /p a=please input time（s）
    shutdown -s -f -t%a%
    goto menu
    :2
    shutdown -a 
    goto nenu
    :3
    exit
    ```
### Powershell
PowerShell中内置的命令称为cmdlets，cmdlet实现具有以下特点：

- 统一的命令形式
- 支持管道功能
- 输出易于管理的对象，支持面向对象的概念

在PowerShell中有一个内置的变量：$profile ;这个变量指示了PowerShell用户自定义配置文件。
可以在PowerShell中输入 $profile。
#### PowerShell中内置的命令

help 可以得到命令结果

cd命令现在用setlocation命令替代

dir命令用get-childitem命令替代

通过：set-alias命令来设置命令别名。

gal查询

get—command 得到命令

set-command 设置命令别名
```powershell
set-alias new new-objector set-alias iexplorer'c:\program files\internet explorer\iexplorer.exe'
```
#### 获取指定命令的帮助信息

eg: get-command get-process利用通配符进行搜索

PowerShe11支持通配符搜索，这一功能的完美支持，完全可以媲美linux下的正则表达式。
```powershell
get-command *char*
//例如搜索带动词get的命令：
get-command -verb 
//get搜索带名词service的命令：
get-command -noun service 
```
#### cmdlets一致的命令接口模式

PowerShe11采用一种称为cmdlets的命令接口模式，所有的命令都遵循这样的命令模式：

动词-名词，如：get-command命令，get就是动词，而command就是名词  get-process/get-eventlog

#### 管道

管道的最大特点就是：前一个命令的输出作为后一个命令的输入。cmd、bash均支持管道管道的概念

在PS中，继承了cmd管道符号的表示方法：表管道；但是PS与cmd的管道有本质的区别，cmd中的管道传递的是文本信息，而PS中传递的是对象，因此PS中的管道更加易于使用和管理。

## 用户与组管理

服务器系统版本介绍:
  
windows服务器系统：win2000 win2003 win2008 win2012

linux服务器系统：Redhat Centos 

### 用户管理
#### 用户概述

每一个用户登录系统后，拥有不同的操作权限。每个账户有自己唯一的SID（安全标识符）

- 用户SID:S-1-5-21-426206823-2579496042-14852678-500 UID
- 系统SID:S-1-5-21-426206823-2579496042-14852678
  - windows系统管理员administrator的UID是500
  - 普通用户的UID是1000开始
  - 不同的账户拥有不同的权限，为不同的账户赋权限，也就是为不用账户的SID赋权限！
  
查看sid值：whoami /user

账户密码存储位置：C:\windows\system32\config\SAM

windows系统上，默认密码最长有效期42天


