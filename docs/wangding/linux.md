# linux基本操作

## 目录
- /根目录 系统的起始目录
- /bin 保存了管理员和普通用户的命令
- /sbin 只有管理员可以执行的命令
- /boot 引导目录独立的分区 
  - /dev/sda1具有内核启动菜单还有驱动盘
- /dev device设备，设备文件存放目录 
  - 文件存放目录/dev/sda
- /etc 配置文件存放目录
- /home普通用户的家目录
- /root 超级管理员的家
- /media 媒体光驱默认挂载目录
- /mnt mount 临时设备挂载目录（U盘等外接设备）
- /proc 进程状态存放目录（存放在内存空间，不占硬盘空间）
  - 文件目录下的数字为进程序号
- /tmp 临时文件存放目录
- /usr GNU社区软件的默认安装目录
- /var 常变文件存放目录日志文件邮件。
- /lib 这个目录里存放着系统最基本的动态连接共享库，其作用类似于Windows里的DLL文件。几乎所有的应用程序都需要用到这些共享库。

**颜色**
代表文件类型
- 蓝色字体代表目录
- 黑色代表普通文件
- 红色指压缩文件
- 浅蓝色指符号链接（类似于快捷方式），符号链接并不是文件的本身，后面的箭头指向的是真正的文件
- 黑底黄字指设备文件
- 紫色指图片文件和模块文件

## 命令

命令基于centos

- ls 列出当前目录内容
  - ls -l列出详情
  - ls -lh列出详情
  - ll -l列出的是所有文件，包括隐式文件
- cd 切换文件目录
  - cd ../回到前一级目录
  - cd 开头加斜杠/代表绝对路径，不加代表相对路径
  - cd ~代表该用户的家目录
- pwd 显示当前目录
- 括号中的内容含义：[root@echos dev]#,root是用户，echos是电脑名，dev为当前目录，#代表用户身份，代表超级管理员，$代表普通用户身份
- cat concatenate，连接到文件并打印输出，concatenate files and print on the standard output
  - cat -n显示行数
- man 查看命令详情
  - man cat查看cat命令详情
- touch 创建空文件或者修改文件的时间标记（只能建立文件不能建立目录）
  - touch一个存在的目录或者文件，就会更新文件的时间
  - touch一个不存在的文件，可以创建文件
- echo 输出当前输入(默认命令行)
  - 符号>代表重定向
  - echo "how are you" > doc.txt 覆盖文件内容
  - echo "how are you" >> doc.txt 追加内容
- mkdir 创建文件夹
  - 注意，在同一个文件夹下建立同名的文件(linux可以不带后缀)和文件夹会有冲突
  - mkdir -p可以递归创建文件夹，发现父目录不存在，就会创建父目录 例如 mkdir -p /tmp/1/2/3
- mv 移动，剪切，重命名
- cp 拷贝
  - cp -r递归复制，即文件夹下全部复制
- rm 删除
  - rm -f不提示直接强制删除
  - rm -r递归删除
  - rm -rf直接全部删除目录以及目录所有内容
- ln 链接
  - ln -s a a.link创建一个文件链接
- find 这个命令会在给定位置搜寻与条件匹配的文件。你可以使用
  - find-name的-name选项来进行区分大小写的搜寻
  - find-iname来进行不区分大小写的搜寻。
  - find 目录 -size +100M，找到大于100M的文件，同样减号代表小于100M
  - find / -size +100M寻找当前目录下的100M以上的文件
- ping ping通过发送数据包ping远程主机（服务器），常用与检测网络连接和服务器状态。
- su 即Switch User su用于切换不同的用户。即使没有使用密码，超级用户也能切换到其它用户。
- file 文件详情
- dd 使用dd这个linux命令可以创建一定大小文件， 
  - if=输入目录，
  - of=输出目录，
  - bs=大小 c
  - count=输出数目，即将if目录下的内容以1M为单位重复100次
  - eg：dd if=/dev/zero of=hello.txt bs=100M count=100
- hexdump 十六进制输出
**压缩命令：**
- tar tar命令能创建、查看和提取tar压缩文件。
  - tar -cvf 是创建对应压缩文件
  - tar -tvf 来查看对应压缩文件
  - tar -xvf 来提取对应压缩文件
  - -j 使用bzip2压缩工具压缩，后缀名写.tar.bz2
  - -z 使用gzip压缩工具压缩，后缀名写.tar.gz
  - -c create创建
  - -f 后面跟新建的文件名
  - -t 不解压缩查看文件内容
  - tar -xf 1901class.tar.gz -C /opt
  - -x 解压缩并解包
  - -C 指定解压路径
- gzip 压缩，对应unzip为解压缩
- bzip2 压缩 对应bunzip2为解压缩

**VIM命令**
命令行：
- gg 跳转
- dd 删除行
- set nu显示行号
- /bzip2 搜索关键字bzip2
- 65G 跳转到65行，
- w 另存为
- 21.42 d删除21-42行
- 27G,15x 跳转27行并删除15个字符

## 用户管理
### linux用户概述
Linux系统是一个多用户多任务的分时操作系统，任何一个要使用系统资源的用户，都必须首先向系统管理员申请一个账号，然后以这个账号的身份进入系统。

用户的账号一方面可以帮助系统管理员对使用系统的用户进行跟踪，并控制他们对系统资源的访问；另一方面也可以帮助用户组织文件，并为用户提供安全性保护。

每个用户账号都拥有一个唯一的用户名和各白的口令。用户在登录时键入正确的用户名和口令后，就能够进入系统和自己的主目录。实现用户账号的管理，要完成的工作主要有如下几个方面：用户账号的添加、剔除与修故，用户口气的管理。用户组的管理

用户账号的管理工作主要涉及到用户账号的添加、修改和删除。
添加用户账号就是在系统中创建一个新账号，然后为新账号分配用户号、用户组、主目录和登录Shell等资源。
刚添加的账号是被锁定的，无法使用。

### 用户命令行操作
- id 查看账号属性
- su 切换用户
- useradd 创建用户
  - useradd 选项 用户名 实例
  - useradd -d /home/sam -m sam 
    - 此命令创建了一个用户sam，其中-d和-m选项用来为登录名sam产生一个主目录/home/sam（/home为默认的用户主目录所在的父目录）。
    - 增加用户账号就是在/etc/passwd文件中为新用户增加一条记录，同时更新其他系统文件如/etc/shadow，/etc/group等。Linux提供了集成的系统管理工具userconf，它可以用来对用户账号进行统一管理。
- usermod 修改帐号
  - 修改用户账号就是根据实际情况更改用户的有关属性，如用户号、主目录、用户组、登录Shell等。
  - usermod -s /bin/ksh -d/home/z -g developer sam此命令将用户sam的登录Shell修改为ksh，主目录改为/home/z，用户组改为developer。
  - 常用的选项包括-c，-d-m.-g，-6.-s.-u以及-。等，这些选项的意义与useradd命令中的选项一样，可以为用户指定新的资源值。
  - 另外，有些系统可以使用选项：-l新用户名
  - 如果默认用户名，则修改当前用户的口令。
- passwd
  
  0ld password:****** |New password:******

  Re-enter new password:*******

  如果是超级用户，可以用下列形式指定任何用户的口令：

  passwd samr 

  New password；*******

  Re-enter new password:******

  普通用户修改自己的口令时，passwd命令会先询问原口令，验证后再要求用户输入两遍新口令，如果两次输入的口令一致，则将这个口令指定给用户；而超级用户为用户指定口令时，就不需要知道原口令。

  为用户指定空口令时，执行下列形式的命令：

    - passwd -d sam此命令将用户sam的口令删除，这样用户sam下一次登录时，系统就不再允许该用户登录了。
  
  passwd 命令还可以用-l（lock）选项锁定某一用户，使其不能登录，例如：
    - passwd-lsam

### 用户组

每个用户都有一个用户组，系统可以对一个用户组中的所有用户进行集中管理。不同Linux系统对用户组的规定有所不同，如Linux下的用户属于它同名的用户组，这个用户组在创建用户时同时创建。

用户组的管理涉及用户组的添加、删除和修改。

组的增加、删除和修改实际上就是对/etc/group文件的更新。

### 用户组的相关命令行

- groupadd 增加一个新的用户组
  - groupadd 选项用户组
  - 可以使用的选项有：
    - -g GID指定新用户组的组标识号（GID）。
    - -o 一般与 -g 选项同时使用，表示新用户组的GID可以与系统已有用户组的GID相同。
  - groupadd group1 此命令向系统中增加了一个新组group1，新组的组标识号是在当前已有的最大组标识号的基础上加1。
  - groupadd -g 101 group2此命令向系统中增加了一个新组group2，同时指定新组的组标识号是101。
- groupmod 修改用户组参数
  - groupmod-g 102 group2此命令将组group2的组标识号修改为102。
  - groupmod-g 10000 -n group3 group2此命令将组group2的标识号改为10000，组名修改为group3。
- newgrp
  
  如果一个用户同时属于多个用户组，那么用户可以在用户组之间切换，以便具有其他用户组的权限。用户可以在登录后，使用命令newgrp切换到其他用户组，这个命令的参数就是目的用户组。
  - newgrp root
  
    这条命令将当前用户切换到root用户组，前提条件是root用户组确实是该用户的主组或附加组。类似于用户账号的管理，用户组的管理也可以通过集成的系统管理工具来完成。

## 权限管理
如何查看权限
![img](/img/wangding/20200103202757493.png)
| d    | rwx                  | r-x                  | r-x            |
| ---- | -------------------- | -------------------- | -------------- |
| 目录 | root（文件的所属者） | root（文件的所属组） | 其他用户的权限 |

| -    | rw-                  | r—                   | r-             |
| ---- | -------------------- | -------------------- | -------------- |
| 文件 | root（文件的所属者） | root（文件的所属组） | 其他用户的权限 |

字段1：表示文件的类型 d 目录 -文件 l 符号链接c 字符型设备b block块设备

字段2：文件所属者的权限
|      | r            | w                    | x          |
| ---- | ------------ | -------------------- | ---------- |
| 目录 | 列出目录内容 | 添加删除目录中的文件 | 进入该目录 |
| 文件 | 读           | 写                   | 执行       |
字段3：文件所属组的权限

字段4：其他用户的权限（既不是文件的所属者，也不在文件的所属组中）

- chmod 修改文件权限
  - chmod a= —目录
  - chmod g=rwx 目录
  - chmod o=rx 目录
  - chmod 对象 运算符号 限文件或者目录 修改文件属性
    - 对象：u（user所属者）g（group所属组）o（other其他）a（all所有）
    - 运算符号：+赋权 -撤权 =指定权限
  - 八进制赋权法
    r=4 w=2 x=1

    | rwxr-xr-x | rw-r-r- |
    | --------- | ------- |
    | 755       | 644     |

    | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
    | --- | --- | --- | --- | --- | --- | --- | --- |
    | 000 | 001 | 010 | 011 | 100 | 101 | 110 | 111 |
    | —   | -x  | -w- | -wx | r—  | r-x | rw- | rwx |

    - t粘滞位（只对目录有效）在目录中建立的文件只有文件的所属者可以删除。
      - chmod 777 /tmp/test; chmod o+t /tmp/test 对不在该组的其他用户设粘滞位
      - chmod 1777 /tmp/test 用1777指定也可以

    - sgid（只对目录有效）在目录中建立的文件或者目录属组会继承父目录的属组
      - chmod 777 /tmp/test; chmod g+s /tmp/test 
      - chmod 2777 /tmp/test 
      - 解释：suid（只对可执行文件有效）当一个可执行文件具有suid权限，无论谁运行该文件，谁就具有该文件所属者的权限。