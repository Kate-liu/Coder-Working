# 工具|搭建python环境
**实现python2版本与python3版本的环境搭建。**

## 正文

**1.Python下载**
    官网:
    **www.python.org**
下载:
    ( 64位3.5.2Windows x86-64 executable installer或32位3.7.1 Windows x86 executable installer)
    (64位2.7.12 Windows x86-64 MSI installer或32位2.7.12 Windows x86 MSI installer)

**2.Python安装**
    推荐安装路径为C:\Python27和C:\Python37，因为如果路径有空格的话（C:\Program Files\Python35）pip可能会有问题.
    比如：将C:\Python37\python.exe修改为python3.exe，C:\Python35\Scripts\pip.exe改为pip3.exe，如果已经有pip3.exe，就把pip.exe删除。
    以后需要使用Python3的环境就在终端输入python3就行（输入python就是python2.7的环境），同理pip3就是使用python3的pip

**3.报错解决**
终端输入:  **pip3  -V**
报错如下：
    Fatal error in launcher: Unable to create process using 
解决:
    需要升级一下对应的pip3(终端输入>python3 -m pip install -U pip)

关于pip的介绍,以前旧版本的Python可能还要单独装pip，现在Python都是自带pip，无需单独安装pip。

**4.环境变量的设置**
   ** 计算机（我的电脑\此电脑）>右键>属性>高级系统设置>环境变量>系统变量**










