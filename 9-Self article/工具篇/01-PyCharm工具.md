# 工具|PyCharm
*主要介绍关于PyCharm的使用小技巧，方便自己使用这款软件。*

## 前戏准备
1.下载pycharm: [官方网站(鼠标单击)](https://www.jetbrains.com/)
2.安装(自己百度一下，教程很多)

### 正式开始
#### PyCharm 模块
1.在Pycharm下为你的Python项目配置Python解释器
方法: **File>settings>Project:当前项目名>Project Interpreter>add Local**

2.使用Pycharm安装Python第三方模块
方法1: **File>settings>Project:当前项目名>Project Interpreter>点击右侧绿色小加号>进行搜索需要的第三方模块>点击左下角(Install Package)**
方法2: **pip3 install 第三方模块名**

3.在Pycharm下创建Python文件、Python模块、Python文件夹
**Python文件:File>New>Python File**
**Python模块:File>New>Python Package**
**Python文件夹:File>New>Python Directory**

#### PyCharm 设置
1.**不使用tab、tab=4空格**：File>settings>Editor>Code Style>Python(是否勾选Use tab character)

2.**字体、字体颜色**：File>settings>Editor>Colors Scheme>Python(可以进行自定义显示的颜色)

3.**关闭自动更新**：File>settings>Appearance & Behavior>System Settings>Updates(自己进行自动更新的设置)

4.**脚本头设置**：File>settings>Editor>File and Code Templates>Python Script (书写自己每一次新建py文件都会出现的脚本头)

5.**显示行号**：File>settings>Editor>General>Appearance>Show line numbers 
注意:可以直接在显示行号的位置鼠标右键，进行显示与隐藏的勾选

6.右侧竖线是**PEP8的代码规范**，提示一行不要超过120个字符

7.**导出、导入自定义的配置**： File>Export Settings、Import Settings
注意:需要自己重新启动之后才会生效。

8.**设置菜单字体和大小**: File>settings>Appearance&Behavior>Appearance

9.**设置Console&Terminal字体大小**: File>settings> Editor>Font>Console Font

10.**设置文件编码：**File>settings> Editor>File Encodings> Global Encoding/Project Encoding / Properties Files  都设置为UTF-8

11.**修改背景颜色**：Settings>Editor>Color Scheme>General>右边Text下面
选中Default text>修改Background颜色即可

#### PyCharm 快捷键
0. 常用快捷键的查询和配置：Keymap
1. Ctrl + D：复制当前行
2. Ctrl + E：删除当前行
3. Shift + Enter：快速换行(不用鼠标在最后一行就可以实现换行)
4. Ctrl + /：快速注释（选中多行后可以批量注释）
5. Tab：缩进当前行（选中多行后可以批量缩进）
6. Shift + Tab：取消缩进（选中多行后可以批量取消缩进）
7. Ctrl + F：查找
8. Ctrl + H：替换
9. Ctrl + 减号：折叠当前代码块
10. Ctrl + Shift + 减号：折叠当前文件
11.  Live Templates（善用live templates提高开发效率）==>Settings>Editor>Live Templates

#### PyCharm 安装插件 
Pycharm安装插件，例如Markdown support、数据库支持插件等。安装.ignore、BashSupport、IdeaVim、CodeGlance等

**步骤:** File>settings>Plugins>Browse repositories（下方三个按钮中间那个）>搜索‘markdown support’>install
**注意:**此时就可以新建带有md后缀的文件


#### PyCharm Git配置
1.本地安装好Git
 2.File>settings>Version Control>Git
3.配置了Git等版本控制系统之后，可以很方便的diff查看文件的不用
4.配置github：File>Settings>Version Control>GitHub>右侧填写Host、Login 及Password 即可。

#### PyCharm 常用操作
**例如**:复制文件路径、在文件管理器中打开、快速定位、查看模块结构视图、tab批量换space、TODO的使用、Debug的使用。
1. **复制文件路径**(对于整个项目而言的相对路径)：左侧文件列表右键选中的文件>Copy Path
2. **在文件管理器中打开**：右键选中的文件>往下找到Show In Explorer
3. **快速定位**：Ctrl + 某些内建模块之后，点击在源文件中展开
4. **查看结构**：IDE左侧边栏Structure 查看当前项目的结构
5. **tab批量换space**：Edit>Convert Indents > To Spaces /Tabs
6. **TODO的使用**：# TODO 要记录的事情/# todo
7. **Debug设置断点**，直接点击行号与代码之间的空白处即可设置断点。debug一般只需在关键点设置一个，然后debug调试时步进执行。没必要点很多个断点
8. **双页面显示:** Tab页上右键>Move Right（Down），把当前Tab页移到窗口右边（下边），方便对比
9. **查看修改历史**: 文件中右键>Local History > show history 能够查看文件修改前后的对比
10. **IDE右下角**能看到一些有用的信息，光标当前在第几行的第几个字符、当前回车换行、当前编码类型、当前Git分支
11. **查看数据库信息**:IDE右侧边栏>Database（点开后）>左上角绿色“+”号>下拉Data Source选择你要连接的数据库类型>点击之后页面最下方会有提示安装驱动（Download missing driver files）
12.** 执行某个文件中的某一行（某些行）**：选中要执行的代码部分>右键Execute Selection in Console

#### PEP8规范
1. 单独一行的注释：#+1空格+注释内容
2. 代码后跟着的注释：2空格+#+1空格+注释内容
3. pyCharm会自动进行不规范显示波浪线
4. 在设置中去掉:1.settings>Editor>Inspections>Python
5. 函数前面空一行，类前面空两行
6. 某些单词一直有下划线提示，可以右键>Spelling>Typo:Save 'xxx' to dictionary

#### UTF-8 编码
更改编码格式，SSH Terminal： Default encoding:UTF-8
步骤: Settings>Tools>SSH Terminal>最后一行Default encoding:选择UTF-8

#### 远程调试
边改边同步到远程服务器，本地直接执行远程服务器上的代码。
1. Build,Execution,Deployment>Deployment>点击绿色“+”添加一个Deployment配置。配置好SFTP之后可以右键上传更新后的代码文件。
2. Project Interpreter>Add Remote>选择Deployment configuration>下拉框选择上面的配置>下面选择python解释器路径
3. 关掉对话框，配置Path mappings。
4. 官网文档：https://www.jetbrains.com/help/pycharm/2017.1/configuring-remote-interpreters-via-deployment-configuration.html?search=remote

## 结束语
**PyCharm只是工具，熟练地掌握很有必要，但是离不开“熟能生巧”。所以还是多打开pycharm多书写代码，自然就会用的多了，自然就熟悉了。**









