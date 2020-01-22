# 开发|xxx
*现在开始....。*

## 前言
    目前所有的文章思想格式都是:知识+情感。
    知识:对于所有的知识点的描述。力求不含任何的自我感情色彩。
    情感:用我自己的方式，解读知识点。力求通俗易懂，完美透析知识。

## 正文
**....。**

### 什么是模块？
    安装
        pip3 install xxx (下载本包加依赖包)（更改镜像网站下载）
        源码安装
    导入
        import  
        from .. import ..
        as ..
        *
        模块查找路径 sys.path
        . 表示当前目录
    调用
    卸载
        pip3 uninstall xxx
    查看已经安装的包信息
        pip3 freeze
        pip3 list

### 什么是包？
    __ init __.py 导入就执行
    包的导入
    程序入口在项目的第一层文件中

### 远程ssh模块
    paramiko
    登录远程Linux的服务器

### os模块
    path
    abspath
    walk   # 循环所有的文件
    
### sys模块

### time模块
    时间戳
    UTC
    time()
    sleep()
    字符串之间的格式转换
    strftime()
    strptime()
    周一是数字1
    周日是数字0

### datetime模块
    .date
    .datetime
    .timedelta
    
### pytz模块
    时区
    .timezone

### random模块
    randint
    shuffle
    
### string模块
    所有的字符串

### pickle模块
    dumps
    loads
    dump 存文件
    load 加载文件
    先进先出
    Python特有，变bytes格式

### json模块
    全球通用，变字符串格式

### hashlib模块
    加密算法
    hash属于散列
    哈希碰撞
    md5
        update()
        hexdigest()
    撞库：反求md5
    加盐
    SHA-1
    SHA-256
    
### shutil模块
    操作文件，复制，权限，压缩，复制文件树，
    copyfile()
    copymode() copy权限，其他不动
    copy() copy内容与权限
    

### zipfile模块
### tarfile模块

### re模块
    正则表达式
    findall()
    match()  从第一个字符开始符合规则
    search() 匹配遇到的第一个
    group()
    groups()
    groupdict()
    split() 数据分割
    sub() 数据的替换
    匹配规则
        .
        ^
        $
        *
        +
        ?
        ()
        {}
        |
        []
        <>
        ?P<name>[a-z]
    标识符 flag
        


## 结束语
 **恭喜各位，看完了...。**
**总结:。。。。。**
**下一篇将。。。。。**








