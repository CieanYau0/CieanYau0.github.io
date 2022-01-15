# 环境搭建

> 很显然，每当我们更换设备、重置系统等等场景的时候，避免不要需要一步步再重新搭建自己的开发环境，所以在学习文档前，我将在这儿记录我关于Java的开发环境搭建的所有内容



!> 本章节内容仅供学习参考，并非最佳方案，按自己喜好调整即可

## Java安装

安装Java的时候，并不是每个人都仅仅只有一个Java，在某些特定的时候是需要Java11，但你只安装了一个Java8，为了避免这个情况的发生，我将会下载Java8、Java11、Java16、Java17

> 多个Java版本如何共存？

+ 在网上的普遍教程中，Java的环境变量都是只能设置其一，但我们可以将Java8设置为环境变量，并**把不同版本的Java放在你所知道的文件目录内**，这样在你需要某个Java的时候，只需要将其文件目录切换至所需要版本Java的目录下即可

> 注意事项

+ 安装Java8时记得去掉不需要安装的包，并配置自己的存放位置 **[Java8下载地址](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html)**

![](https://cdn.lixingyong.com/2022/01/03/1.png)

> 安装Java11、Java16、Java17或其他版本的时候下载zip文件再解压至目标文件夹即可，我将会用图片的方式说明我的做法

+ **[Java11下载地址](https://www.oracle.com/java/technologies/javase/jdk11-archive-downloads.html)** 、 **[Java16下载地址](https://www.oracle.com/java/technologies/javase/jdk16-archive-downloads.html)** 、 **[Java17下载地址](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html)** 
+ 效果如下:

![](https://cdn.lixingyong.com/2022/01/03/2.png)

+ 配置完后，命令行测试

![](https://cdn.lixingyong.com/2022/01/03/a2.png)



## IDE的选择与配置

当别人问我IDE的选择方面，我会毋庸置疑地喊出:"IDEA YYDS"，但是除了这个绝世神器，我们还有很多选择，如: neovim、vscode、sublime、atom 等等.....

!> 插一嘴 > ... < 我就用过neovim 、 vscode 写过Java代码，但是毕竟轻量化的IDE的繁琐配置总能占据你大把的时间，那么我还是推荐使用IDEA，包括本人现在也是使用IDEA，当然你若时间有余可以去尝试一下其他的IDE



> 根据上面的了解呢，我并不会带你一步步安装IDEA，我会将重要的部分截图

+ **[IntelliJ IDEA下载](https://www.jetbrains.com/zh-cn/idea/)**

+ 配置自己所想存放的位置

![](https://cdn.lixingyong.com/2022/01/03/3.png)

+ IDEA界面设置

![](https://cdn.lixingyong.com/2022/01/03/4.png)

+ 自动导包(import)

![](https://cdn.lixingyong.com/2022/01/03/5.png)

+ 代码补全

![](https://cdn.lixingyong.com/2022/01/03/6.png)

+ 代码区字体设置

![](https://cdn.lixingyong.com/2022/01/03/7.png)



## Maven安装配置

Maven作为一个版本控制工具，对于后面的开发帮助很大，假如你现在是一名刚学Java不久的萌新，那么你跟着我的步伐将Maven安装并配置好后，存放着，在日后的学习中会有所接触

!> 假如你懂编程的话，你可能会问:"为什么不使用比Maven快2-3倍的Gradle呢？"

+ 我不否认Gradle优秀的事实，并且我也有在使用，但并不是很深入的了解过，在这讲解Maven的安装配置，仅仅是我用惯了Maven，当然，我在日后或许会在本章贴出Gradle的安装配置

> Maven和Java一样是可以下载多个版本共存的，但是在实际使用中使用其一就行了，要是不放心，可以在知乎、CSDN、BiliBili上搜索现在最流行的版本，然后在去官网下载对应的版本即可

+ **[Maven下载地址]([Maven – Download Apache Maven](https://maven.apache.org/download.cgi))**
+ 下载此位置的Maven

!> src代表带着源码的maven，而bin就仅仅是Maven自身，我们并不需要源码文件，所以我们选择这个，当然，如果你有需求，你也可以下载src版本的进行学习

![](https://cdn.lixingyong.com/2022/01/03/8.png)

+ 在Maven的目录下创建一个 **Repository** 文件夹

![](https://cdn.lixingyong.com/2022/01/03/10.png)

+ 找到Maven的目录下 conf 下的 settings.xml

![](https://cdn.lixingyong.com/2022/01/03/9.png)

+ 在<**localRepository**>标签内添加自己的本地位置路径

```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.2.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.2.0 https://maven.apache.org/xsd/settings-1.2.0.xsd">
  <!-- localRepository
   | The path to the local repository maven will use to store artifacts.
   |
   | Default: ${user.home}/.m2/repository
  <localRepository>/path/to/local/repo</localRepository>
  -->
  <!-- 此处替换为你所创建的Repository文件夹位置 -->
  <localRepository>D:\Tools\Maven\Repository</localRepository>

</settings>

```

+ 在<**profiles**>标签内添加一个<**profile**>标签，修改maven默认的JDK版本

```xml
<profile>     
    <id>JDK-1.8</id>       
    <activation>       
        <activeByDefault>true</activeByDefault>       
        <jdk>1.8</jdk>       
    </activation>       
    <properties>       
        <maven.compiler.source>1.8</maven.compiler.source>       
        <maven.compiler.target>1.8</maven.compiler.target>       
        <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>       
    </properties>       
</profile>
```

+ 在<**mirrors**>标签内添加国内镜像源

```xml
<!-- 阿里云仓库 -->
<mirror>
    <id>alimaven</id>
    <mirrorOf>central</mirrorOf>
    <name>aliyun maven</name>
    <url>http://maven.aliyun.com/nexus/content/repositories/central/</url>
</mirror>

<!-- 中央仓库1 -->
<mirror>
    <id>repo1</id>
    <mirrorOf>central</mirrorOf>
    <name>Human Readable Name for this Mirror.</name>
    <url>http://repo1.maven.org/maven2/</url>
</mirror>

<!-- 中央仓库2 -->
<mirror>
    <id>repo2</id>
    <mirrorOf>central</mirrorOf>
    <name>Human Readable Name for this Mirror.</name>
    <url>http://repo2.maven.org/maven2/</url>
</mirror>
```

+ 配置 **M2_HOME** 的环境变量

![](https://cdn.lixingyong.com/2022/01/03/11.png)

+ 配置 path 环境变量

![](https://cdn.lixingyong.com/2022/01/03/12.png)

+ IDEA配置 **Build、Execution、Deployment** -> **Build Tools** -> **Maven**

![](https://cdn.lixingyong.com/2022/01/03/ab.png)

+ 配置完后，命令行测试

![](https://cdn.lixingyong.com/2022/01/03/c1.png)



## Gradle安装配置

!> Gradle真的太好用了! 和Maven并无二致，但是它的性能比Maven高出几倍，我并不会因为这个而不使用Maven，因为在很多项目中也还在使用Maven做构建工具，所以建议Maven和Gradle两个都学起来

和Maven一样，假如你现在还是初学者的话，建议下载Gradle和Maven，安装好后，留着以后备用

> Gradle也是有很多版本的，所以我们仅需安装一个就行了，在项目中若版本不对，IDE会自动下载对应的版本，或者你也可以同时下载多个版本

+ 在安装Gradle之前，请先确保你安装好了Java

![](https://cdn.lixingyong.com/2022/01/03/a2.png)

+ **[Gradle下载地址](https://gradle.org/install/)**
+ **Binary-only**是只下载二进制源码，**Complete, with docs and sources**是下载源码和文档，如果有阅读文档的需求可以下载第二个，没有需要的下载**Binary-only**即可

![](https://cdn.lixingyong.com/2022/01/03/a3.png)

+ 配置GRADLE_HOME环境变量

![](https://cdn.lixingyong.com/2022/01/03/a4.png)

+ 配置GRADLE_USER_HOME环境变量 **(用于指示仓库位置)**

![](https://cdn.lixingyong.com/2022/01/03/a5.png)

+ 配置 **path** 环境变量

![](https://cdn.lixingyong.com/2022/01/03/a6.png)

+ 在Gradle安装目录下的 init.d 文件夹下，新建一个 init.gradle 文件

![](https://cdn.lixingyong.com/2022/01/03/a7.png)\

+ 在 **init.gradle** 内编写以下内容

```groovy
allprojects {
    repositories {
        maven { url 'file:///C:/Java/maven_repository'}
        mavenLocal()
        maven { name "Alibaba" ; url "https://maven.aliyun.com/repository/public" }
        maven { name "Bstek" ; url "http://nexus.bsdn.org/content/groups/public/" }
        mavenCentral()
    }

    buildscript { 
        repositories { 
            maven { name "Alibaba" ; url 'https://maven.aliyun.com/repository/public' }
            maven { name "Bstek" ; url 'http://nexus.bsdn.org/content/groups/public/' }
            maven { name "M2" ; url 'https://plugins.gradle.org/m2/' }
        }
    }
}
```

+ Gradle完毕后，IDE会自动检测

![](https://cdn.lixingyong.com/2022/01/03/a8.png)

+ 配置完后，命令行测试

![](https://cdn.lixingyong.com/2022/01/03/c2.png)



## MySQL安装配置

> 在Java开发中，我们在开发项目或者测试时或多或少会接触点数据存储的场景，那么这时候就需要我们在自己的开发环境安装一个数据库，数据库也有很多可以选择，那么我们选择MySQL作为我们的数据库

+ [MySQL下载](https://dev.mysql.com/downloads/mysql/)
+ 下载MySQL的zip包

!> 不推荐下载使用msi或exe的方式安装，因为非常的麻烦

![](https://cdn.lixingyong.com/2022/01/03/a9.png)

+ 配置MYSQL_HOME环境变量

![](https://cdn.lixingyong.com/2022/01/03/C3.png)

+ 配置 **path** 环境变量

![](https://cdn.lixingyong.com/2022/01/03/c4.png)

+ 创建 **my.ini**

```xml
[client]
# 设置mysql客户端默认字符集
default-character-set=utf8
[mysqld]
#设置3306端口
port = 3306
# 设置mysql的安装目录 这块换成自己解压的路径
basedir=D:\\Tools\\MySQL
# 允许最大连接数
max_connections=200
# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
```

+ **初始化MySQL**

!> 若在这出现了问题，请移步[此链接](https://milank.cn/archives/vcrun)查看

![](https://cdn.lixingyong.com/2022/01/03/c6.png)

+ 初始化后将自动创建data文件夹

![](https://cdn.lixingyong.com/2022/01/03/c7.png)

+ 在 **my.ini** 添加以下内容

```xml
[client]
# 设置mysql客户端默认字符集
default-character-set=utf8
[mysqld]
#设置3306端口
port = 3306
# 设置mysql的安装目录 这块换成自己解压的路径
basedir=D:\\Tools\\MySQL
# 新增加内容
# 数据存放的位置
datadir=D:\\Tools\\MySQL\\data
# 允许最大连接数
max_connections=200
# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
```

+ 安装MySQL的启动脚本

> 若出现Service successfully installed，证明安装成功；如出现Install of the Service Denied，则说明没有以管理员权限来运行cmd

![](https://cdn.lixingyong.com/2022/01/03/c8.png)

+ 启动MySQL

![](https://cdn.lixingyong.com/2022/01/03/c9.png)

## Tomcat安装配置

> Tomcat是在学习Web和写项目的时候必不可少的，那么它的用处就在于他会对项目进行软部署，使得你的项目可以在你的电脑上运行起来

!> 假如你现在还是初学者的话，建议安装配置，留着备用

+ 在安装前，请确保你安装了Java

![](https://cdn.lixingyong.com/2022/01/03/a2.png)

+ **[Tomcat下载地址](https://tomcat.apache.org/)** 、下载Tomcat的zip包
+ 配置 CATALINA_HOME 环境变量

![](https://cdn.lixingyong.com/2022/01/03/d1.png)

+ 配置 **path** 环境变量

![](https://cdn.lixingyong.com/2022/01/03/d2.png)

!> Tomcat的相关问题请移步[此链接]()

## Git安装配置

> 以上的东西初学者或许没听过，但是对于一个想要学习编程的人来说，GitHub是每个人必知的代码分享网站，你需要将代码发送至GitHub就需要用到Git这个工具

+ **[Git下载地址](https://git-scm.com/)**
+ 安装详 **只有两部分需要修改**

![](https://cdn.lixingyong.com/2022/01/03/d3.png)

![](https://cdn.lixingyong.com/2022/01/03/d4.png)

+ 设置Git的全局信息

```bash
git config --global user.email "你的邮箱"

git config --global user.name "你的名称"
```

## Redis安装配置

> Redis的作用就像我们电脑的内存条一样，我们可以将数据放入Redis内，会比放在存储硬盘的速度快很多

+ **[Redis下载地址](https://github.com/MicrosoftArchive/redis/releases)**
+ 配置 **Redis** 下载位置

![](https://cdn.lixingyong.com/2022/01/03/e1.png)

+ 配置默认端口、配置防火墙

![](https://cdn.lixingyong.com/2022/01/03/e2.png)

+ 配置内存最大使用限制

![](https://cdn.lixingyong.com/2022/01/03/e3.png)

+ 在命令行测试是否成功

![](https://cdn.lixingyong.com/2022/01/03/e4.png)



## 总结

虽然这部分环境搭建就这么多，但在实际开发中所需要的东西不仅仅只是这些

> 加油！
