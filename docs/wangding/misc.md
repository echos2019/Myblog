# misc杂项
Misc是英文Miscellaneous的前四个字母，杂项、混合体、大杂烩的意思。
通常分为四个小块

- Recon（信息搜集）主要介绍一些获取信息的渠道和一些利用百度、谷歌等搜索引擎的技巧
- Encode（编码转换）主要介绍在CTF比赛中一些常见的编码形式以及转换的技巧和常见方式
- Forensic&&Stego（数字取证&&隐写分析）隐写取证是Misc中最为重要的一块，包括文件分析、隐写、内存镜像分析和流量抓包分析等等，涉及巧妙的编码、隐藏数据、层层嵌套的文件中的文件，灵活利用搜索引擎获取所需要的信息等等。

## Recon 信息搜集
不会单独出。

*google hacking*语法知识

分析网站内容以及利用开发者工具
- 科学上网
- 目标Web网页、地理位置、相关组织
- 组织结构和人员、个人资料、电话、电子邮件
- 网络配置、安全防护机制的策略和技术细节
- 通过搜索引擎查找特定安全漏洞或私密信息的方法
- Google Hacking Database
  
## 编码转换
### 进制码
#### 进制
进制也就是进位计数制，是人为定义的带进位的计数方法（有不带进位的计数方法，比如原始的结绳计数法，唱票时常用的“正”字计数法，以及类似的tally mark计数）。对于任何一种进制一x进制，就表示每一位置上的数运算时都是逢x进一位。十进制是逢十进一，十六进制是逢十六进一，二进制就是逢二进一，以此类推，x进制就是逢x进位。

在CTF比赛中，常见进制为二进制、八进制、十进制、十六进制。

b代表二进制，o八进制，d十进制，x16进制(是C语言中格式化代表的内容)
#### 二进制
- 二进制转10进制 python函数 bin() hex(),将10进制转化为对应进制
- 给出一串字符，如果长度为平方数，可以联系着转为图片
- 也可以将二进制转换为字符串等做法
- 还有可以通过字符串表示出图像，离远一点就能看出来

### BASE64
Base64是一种编码方式，是一种可逆的的编码方式，编码后的数据是一个字符串，包含的字符为*A-Z，a-z，0-9，+/*共64个字符：26+26+10+1+1=64，不过其实是65个字符，”=”是填充字符

**编码方法**
1. 字符对应ASCII转换成八位二进制
    base64的基础单位是3 * 8bit的二进制，若是不够3 * 8bit则在后面添加0字节（padding）直至满足3 * 8bit的二进制转换成4*6bit的二进制
2. 4*6bit的二进制转换成十进制
3. 对照base64表把十进制转换成字符
**解码方法**
1. 检查base64编码后面有几个等于号
2. 把字符串按照base64表转换成4*6的倍数位数二进制
3. 删除等于号的个数*8的bit
4. 按照6个bit一组转成字符
![img](/img/wangding/base64.bmp)

**变种：**
- BASE58，相比Base64，Base58不使用数字”0”，字母大写”0”，字母大写”I”，和字母小写”1”，以及”+”和”/”符号。
- BASE32，32个可打印字符，A~Z、2~7、32个可打印字符，“=”符号用作后缀填充
- BASE16，16个可打印字符，A~F、0-9，16个可打印字符
使用python的base64包
API:
```python
import base64
base64.b64encode();
base64.b32encode();
base64.b16encode();
base64.b58encode();
```
**二进制异或操作；**

将字符串转化为ASCII进行异或操作之后再转换回字符串，ord()将字符转化为ASCII，chr()再转化回去

**base64转化图片：**

转码之后直接转化为图片

**base64套娃**

多次base64编码之后的结果

### 图片码
- 条形码（barcode）
    是将宽度不等的多个黑条和空白，按照一定的编码规则排列，用以表达一组信息的图形标识符。常见的条形码是由反射率相差很大的黑条（简称条）和白条（简称空）排成的平行线图案。
- 二维码
    维条码/二维码（2-dimensional bar code）是用某种特定的几何图形按一定规律在平面（二维方向上）分布的、黑白相间的、记录数据符号信息的图形；在代码编制上巧妙地利用构成计算机内部逻辑基础的“0”、“1”比特流的概念，使用若干个与二进制相对应的几何形体来表示文字数值信息，通过图象输入设备或光电扫描设备自动识读以实现信息自动处理：它具有条码技术的一些共性：每种码制有其特定的字符集；每个字符占有一定的宽度；具有一定的校验功能等。同时还具有对不同行的信息自动识别功能、及处理图形旋转变化点。

**工具：010editer**

**题型：**

- 二维码读取内部文件，观察编码，观察最大的数，如果比8小，可能就是8进制(判断思路)
- 二维码反色（黑变白）
- 二维码修补，可以使用PS进行修补（比如把三个标识码来进行遮挡，修补就可以用PS）
- PDF417码（结合反色处理，观察白条宽度过大就可能是反色）

### ASCII
ASCII是基于拉丁字母的一套电脑编码系统，主要用于显示现代英语和其他西欧语言。它是最通用的信息交换标准，到目前为止共定义了128个字符。

0-31、127为ascii控制字符，32-126为ascii显示字符。

测试链接：https://www.soison.com/ascii.html

ASCII特征：\u接四个字符

### Unicode

Unicode是计算机科学领域里的一项业界标准，包括字符集、编码方案等。它为每种语言中的每个字符设定了统一并且唯一的二进制编码，以满足跨语言、跨平台进行文本转换、处理的要求。

-工具：http:/Atool.chinaz.com/Tools/Unicode.aspx

&#为编码标志

### Quoted-printable

Quoted-printable可打印字符引用编码”、“使用可打印字符的编码”，我们收邮件，查看信件原始信息，经常会看到这种类型的编码。

一个等号”=”后跟随两个十六进制数字（0-9或A-F）表示该字节的数值。

测试链接：http://web.chacuo.net/charsetquotedprintable


### 摩尔斯电码

摩尔斯电码是一种早期的数字化通信形式，但是它不同于现代只使用零和一两种状态的二进制代码，它的代码包括五种：点、划、点和划之间的停顿、每个字符之间短的停顿、每个词之间中等的停顿以及句子之间长的停顿。

二进制编码常出摩尔斯编码，结合音视频文件来判断

![img](/img/wangding/morse.bmp)

### 敲击码

敲击码（Tap code）是一种以非常简单的方式对文本信息进行编码的方法。因该编码对信息通过使用一系列的点击声音来编码而命名，敲击码是基于5×5方格波利比奥斯方阵来实现的，不同点是是用K字母被整合到C中，敲击的次数表示在表中的坐标，比如.. .表示2，1即为F

![img](/img/wangding/1.bmp)

### UUENCODE
uuencode是将二进制文件转换为文本文件的过程，转换后的文件可以通过纯文本e-mail进行传输，在接收方对该文件进行uudecode，即将其转换为初始的二进制文件。

特点是不常见字符比如]，#，*，:,``等较多

测试链接：http://web.chacuo.net/charsetuuencode

### url

是一种浏览器用来打包表单输入的格式。浏览器从表单中获取所有的name和其中的值，将它们以name/value参数编码（移去那些不能传送的字符，将数据排行等等）作为URL的一部分或者分离地发给服务器。

URL编码的特征为%，所有的URL编码都是由%XX组成的。

### XXencode

XXencode，也是一个二进制字符转换为普通打印字符方法。跟UWencode编码原理方法很相似，唯独不同的是可打印字符不同。

特征为字符串最后的++

测试链接：http://tool.chinaz.com/Tools/Unicode.aspx 


### shellcode

shellcode是一段用于利用软件漏洞而执行的代码，shellcode为16进制的机器码，因为经常让攻击者获得shell而得名。shellcode常常使用机器语言编写。可在暂存器eip溢出后，塞入一段可让CPU执行的shellcode机器码，让电脑可以执行攻击者的任意指令。

工具可以自己去网上找

### 曼彻斯特编码

从低到高为1，从高到低为0，结合音频视频以及二进制

### Npiet

特点文档是像素点的图片

测试链接：https://www.bertnase.de/npiet/npiet-execute.php

### Ook

密文由(OOk,OOk!,OOk?)组成

### brainfork

密文由+ .〈〉[] ’ && ‘ ！. ？或者 ’ + - . <> []’等构成

### jother
密文为8个字符！+()[]{}

在浏览器中console执行即可
### jsfuck

用6个字符（）[]！+来对JavaScript进行编码

测试链接：https://www.bugku.com/tools/jsfuck/

### jjencode/aaencode

由颜文字组成
### VBScript.Encode混淆加密
VBScript.Encode解码器

测试链接：http://www.cftea.com/tools/online/vbscriptDecode/

### CSS/js混淆加密

测试链接：http://tool.chinaz.com/js.aspx

有function等关键字

### php混淆加密

测试链接：https://www.toolfk.com/tool-convert-php

有时候可以直接进行代码审计，有时候就要运行调试

## 数字取证以及隐写

**常见取证对象**
1. PCAP流量包分析
   - 普通的网络流量（最为常见）wireshark
   - 蓝牙数据包USB数据包（鼠标，键盘数据包）…
   - XNUCA的投影仪数据包…
2. 各种图片文件
    JPG PNG
3. 音频，视频
    MP3，WAV，AVI
4. 压缩包
    RAR，ZIP，7z
5. 磁盘文件
   img
6. 内存镜像
7. PDF，WORD
8. ...

### 综述
- 目的一般为发现文件中包含的隐藏字符串（代表需要取证的机密信息）
- 通常夹杂着文件修复
- 而这些搜寻的字符串常常又与隐写加密结合在一起
- 对文件中的特殊编码要有一定的敏感度
- 对文件16进制的熟悉

### 工具
- file
    命令根据文件头（魔法字节）去识别一个文件的文件类型,linux自带工具(由于有些文件可能没有文件后缀)

- Strings
    打印文件中可打印的字符，经常用来发现文件中的一些提示信息或是一些特殊的编码信息，常常用来发现题目的突破口。
    - 可以配合grep命令探测指定信息 strings test|grep -i XXCTF
    - 也可以配合`-o`参数获取所有ASCII字符偏移
- foremost
    进行文件分离
    c：> foremost[-v|-V|-h|-T|-Q|-q|-a|-w-d][-t <type>][-s <blocks>][-k <size>]
    [-b <size>][-c <fi1e>][-o <dir>][-i <file>]
    - -V-显示版权信息并退出
    - -t-指定文件类型.（-tjpeg，pdf...）
    - -d-打开间接块检测（针对UNIX文件系统）
    - -i-指定输入文件（默认为标准输入）
    - -a-写入所有的文件头部，不执行错误检测（损坏文件）
    - -w-向磁盘写入审计文件，不写入任何检测到的文件
    - -o-设置输出目录（默认为./output）
    - -c-设置配置文件（默认为foremost.conf）
    - -q-启用快速模式，在512字节边界执行搜索。
    - -Q-启用安静模式，禁用输出消息。
    - -V-详细模式。向屏等上记录所有消息。

- winhex
    Winhex是一个专门用来对付各种日常紧急情况的工具。它可以用来检查和修复各种文件、恢复删除文件、硬盘损坏造成的数据丢失等。同时它还可以让你看到其他程序隐藏起来的文件和数据。

    总体来说是一款非常不错的16进制编辑器

- 010editer
    010是一个非常好用的工具，除了是一个查看和修改文件的编译器外，还有很多自带的脚本可以帮助我们辅助分析文件格式
- pngcheck
    可以检查png中的数据块
- stegsolve 
    提取图片信道信息
- stegdetect
  - -q仅显示可能包含隐藏内容的图像。
  - -n启用检查JPEG文件头功能，以降低误报率。如果启用，所有带有批注区域的文件将被视为没有被嵌入信息。如果JPEG文件的JFIF标识符中的版本号不是1.1，则禁用outGuess检测。
  - -s修改检测算法的敏感度，该值的默认值为1。检测结果的匹配度与检测算法的敏感度成正比，算法敏感度的值越大，检测出的可疑文件包含敏感信息的可能性越大。
  - -d打印带行号的调试信息。
  - -t设置要检测哪些隐写工具（默认检测jopi），可设置的选项如下：
  - j检测图像中的信息是否是用jsteg嵌入的。
  - o检测图像中的信息是否是用outguess嵌入的。
  - p检测图像中的信息是否是用jphide嵌入的。
  - i检测图像中的信息是否是用invisible secrets嵌入的。
  - 然而我们并不知道密码是啥，这时可以用stegdetect下的stegbreak字典破解，同样图片和stegbreak.exe在同一目录下，命令 stegbreak.exe -r rules.ini -f password.txt -r p hide.jpg 破解密码
- jphs
- steghide
  ![img](/img/wangding/steghide.bmp)

### 常见文件特征

- jpg,jpeg
  - 文件头：FF D8 FF DB
  - FF D8 FF E0 00 10 4A 46 49 46 00 01 
  - FF D8 FF E1 ?? ?? 45 78 69 66 00 00
  - 标记码：由两个字节构成，第一个字节是固定值0xFF，后一个字节则根据不同意义有不同数值压缩数据：前两个字节保存整个段的长度，包括这两个字节
  - JPG基本数据结构为两大类型：“段”和经过压缩编码的图像数据。
  - 一些常见的段类型：0xffd8&&0xffd9为JPG文件的开始结束的标志
- GIF
  - 文件头：47 49 46 38 37 61,47 49 46 38 39 61
- png
  - 89 50 4E 47 0D 0A 1A 0A
  - 对于一个PNG文件来说，其文件头总是由位固定的字节来描述的，剩余的部分由3个以上的PNG的数据块（Chunk）按照特定的顺序组成
  - 文件头+标准数据块（+辅助数据块+数据块…
  - PNG定义了两种类型的数据块，一种是称为关键数据块（critical chunk），这是标准的数据块，另一种叫做辅助数据块（ancillary chunks），这是可选的数据块。关键数据块定义了4个标准数据块，每个PNG文件都必须包含它们，PNG读写软件也都必须要支持这些数据块。
  - 文件头数据块IHDR（header chunk）：它包含有PNG文件中存储的图像数据的基本信息，由13子节组成，并要作为第一个数据块出现在PNG数据流中，而且一个PNG数据流中只能有一个文件头数据块(CRC码可以使用python解码,zlib.crc32())
  ![img](/img/wangding/IHDR.bmp)
  - 调色板数据块PLTE（palette chunk）：它包含有与索引彩色图（（indexed-color image））相关的彩色变换数据，它仅与索引彩色图像有关，而且要放在图像数据块（image data chunk）之前。真彩色的PNG数据流也可以有调色板数据块，目的是便于非真彩色显示程序用它来量化图像数据，从而显示该图像。
  - 图像数据块IDAT（image data chunk）：它存储实际的数据，在数据流中可包含多个连续顺序的图像数据块。
    - 储存图像像数数据
    - 在数据流中可包含多个连续顺序的图像数据块
    - 采用LZ77算法的派生算法进行压缩
    - 可以用zlib解压缩(789C5为标识)
    - 使用hash解码进行解码(30,31为标识符)
  - 图像结束数据IEND（image trailer chunk）：它用来标记PNG文件或者数据流已经结束，并且必须要放在文件的尾部。00 00 00 00 49 45 4E 44 AE 42 60 82，IEND数据块的长度总是00000000，数据标识总是IEND49454E44，因此，CRC码也总是AE
- bmp,dib
  - 42 4D
- tar
  - 75 73 74 61 72 00 30 30
  - 75 73 74 61 72 20 20 00
- 7z
  - 37 3A BC AF 27 1C
- gz,tar.gz
  - 1F 8B
- rar
  - 52 61 72 21 1A 07 00
  - 52 61 72 21 1A 07 01 00
- AVI
  - 52 49 46 46 ?? ?? ?? ?? 
  - 41 56 49 20
- MP3
  - FF FB
- asf,wma,wmv
  - 30 26 B2 75 8E 66 CF 11
  - A6 D9 00 AA 00 62 CE 6C
### LSB
LSB全称leastsignificant bit，最低有效位PNG文件中的图像像数一般是由** RGB三原色（红绿蓝**）组成，每一种颜色占用8位，取值范围为0x00~0xFF，即有256种颜色，一共包含了256的3次方的颜色，即16777216种颜色人类的眼睛可以区分约1000万种不同的颜色这意味着人类的眼睛无法区分余下的颜色大约有6777216种LSB隐写就是修改RGB颜色分量的最低二进制位（LSB），每个颜色会有8bit，LSB隐写就是修改了像数中的最低的1bit，而人类的眼睛不会注意到这前后的变化，每个像数可以携带3比特的信息

工具：Stegsolve，可以提取各个信道的信息