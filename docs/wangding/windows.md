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

#### 内置账户
给人使用的账户：

>administrator#管理员账户
>
>guest#来宾账户

计算机服务组件相关的系统账号

>system  #系统账户==权限至高无上
>
>local services  #本地服务账户==权限等于普通用户
>
>network services  #网络服务账户==权限等于普通用户
#### 配置文件

每个用户都有自己的配置文件（家目录），在用户第一次登录时自动产生，路径是：

>win7/win2008  c:\用户\
>
>xp/win2003 c:\Documents and Settings\

#### 账户赋权

普通用户的权限较低，需要赋权才能完成关机，修改系统时间等操作

在系统管理员账户下，我们可以进行修改用户密码等操作

#### 命令

- net 创建账户，(下面命令是关于用户名是user的操作)
  - net user
  - net user user查看账号信息
  - net user user 121121 修改密码至121121
  - net user user1 121121 /add 创建账户user1并添加密码
  - net user user1 /del 删除
  - /add net user 用户名/del #删除一个用户
  - net user 用户名/active:yes/no #激活或禁用账户

### 组管理
#### 组概述
组的作用：简化权限的赋予。赋权限方式：

- 用户--组-—-赋权限·
- 用户-—-赋权限
#### 内置组
内置组的权限默认已经被系统赋予。

- administrators #管理员组
- guests #来宾组
- users #普通用户组，默认新用户都属于该组
- network #网络配置组
- print #打印机组
- Remote Desktop #远程桌面组

#### 命令

- net localgroup  #查看组列表

- net localgroup  组名  #查看该组成员

- net localgroup 组名 /add  #创建一个新组

- net localgroup 组名 用户名 /add #添加用户到组

- net localgroup 组名 用户名 /del #从组中删除用户

- net localgroup 组名 /del #删除组

## NTFS安全权限

### NTFS权限概述
- 通过设置NTFS权限，实现不同的用户访问不同对象的权限
- 分配了正确的访问权限后，用户才能访问其资源
- 设置权限防止资源被篡改、删除

### 文件系统概述
文件系统即在外部存储设备上组织文件的方法常见的的文件系统：
- FAT windows
- NTFS windows
- EXT linux常见

### NTFS
#### NTFS的簇
簇的大小，越大的话，在一个簇占不满的时候浪费空间更多

簇的大小越小，要用的指针就会越多，导致速度变慢
#### NTFS特点
- 提高磁盘读写性能
- 可靠性。
  - 加密文件系统
  - 访问控制列表（设置权限）(ACL表)
- 磁盘利用率压缩，磁盘配额
- 支持单个文件大于4个G

#### NTFS权限修改
- 取消权限继承
  - 因为子目录的属性由父目录决定，所以如果要修改权限要取消继承
  - 作用：取消后，可以任意修改权限列表了。
  - 方法：文件夹右键属性-—-安全-—-高级-——取消父类继承

- 权限累加
  
    当用户同时属于多个组时，权限是累加的！

    用户a同时属于IT组与HR组，IT组对文件夹jimi可以读取，HR组可以对jimi文件夹写入，则a用户最终的权限为读取和写入。
- 拒绝最大
  
    当用户权限累加时，如遇到拒绝权限，拒绝最大！意思就是累加时如果有拒绝有允许，直接拒绝

    用户a属于财务部组，财务部组成员为10个用户，财务部组拥有对文件夹xxx访问权限，现要求a用户不能脱离财务部组，同时要求a没有访问文件夹xxx的权限。就直接给a个拒绝，这样就会拒绝最大，a就不能访问了
- 取得所有权
  
    默认只有administrator有这个权限！

    作用：可以将任何文件夹的所有者改为administrator用户a已离职，但xxx文件夹的属主是a，由于a用户对xxx文件夹做过权限修改，导致其他用户对xxx文件夹没有任何权限，现需要管理员administrator用户将xxx文件夹重新修改权限。

- 特殊权限
  
    即为查看安全列表的权限

- 强制继承
    - 作用：对下强制继承父子关系！

    - 方法：文件夹右键属性一安全一高级一勾上第二个对号，即可！
    
    - 案例：xx文件夹下有多个子文件夹及文件，由于长时间的权限管理，多个子文件夹的权限都做过不同限修改，现需要xxx下的所有子文件及文件夹的权限全部统一。
- 文件复制对权限的影响
  
    文件复制后，文件的权限会被目标文件夹的权限覆盖。

    唯一不被覆盖的是同分区下**移动**文件