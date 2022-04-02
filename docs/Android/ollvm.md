# OLLVM教程

基于OLLVM-4.0，参考[文章链接](https://www.bilibili.com/read/cv13148903)

如果尝试自己配置环境进行编译，环境建议为ubuntu，gcc版本与g++版本控制在8，cmake版本随意

下载gcc-8与g++-8
```bash
sudo apt-get install gcc-8 g++-8 -y
```
切换版本至8或者9
```bash
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 8
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-8 8
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 9
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 9
```
# 编译（成功率低，环境问题）

# docker容器方法进行编译（成功率高）