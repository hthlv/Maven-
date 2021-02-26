## 什么是Maven

### Maven

目前无论使用IDEA还是Edips谆其他IDE,使用里面ANT工具.ANT工具帮助我们进行编译，打包运行等工作。
Apache基于ANT讲行了升级，研发出了全新的自动化构建工具Maven。
Maven是Apache的一款开源的项目管理工具。

以后无论是普通javase项目还是javaee项目，我们都创建的是Maven项目。

Maven使用项目对象模型（POM-Project Object Model,项目对象模型）的概念，可以通过一小段描述信息来管理项目的构建，报告和文档的软件项目管理工具。在Maven中每个项目都相当于是一个对象，对象（项目）和对象（项目）之间是有关系的。关系包含了：依赖、继承、聚合，实现Maven项目可以更加方便的实现用ar包、拆分项目等效果.

## Maven的下载

### Idea默认集成了Maven

![image-20210225140853156](E:\hu\Programing\JAVA\Maven\images\image-20210225140853156.png)

### 下载地址

http://maven.apache.org/

![image-20210225141145472](E:\hu\Programing\JAVA\Maven\images\image-20210225141145472.png)

![image-20210225141201119](E:\hu\Programing\JAVA\Maven\images\image-20210225141201119.png)

![image-20210225141252365](E:\hu\Programing\JAVA\Maven\images\image-20210225141252365.png)

* bin：存放的是执行文件，命令

idea可以直接集成Maven

![image-20210225141353809](E:\hu\Programing\JAVA\Maven\images\image-20210225141353809.png)

* conf目录：下面有一个非常重要的配置文件-->settings.xml-->Maven的核心配置文件/全局配置文件

  

### 手动弄出.m2文件

![image-20210225145826655](E:\hu\Programing\Java\Maven\images\image-20210225145826655.png)

**如果没有.m2目录，手动配置执行命令**

![image-20210225145910431](E:\hu\Programing\Java\Maven\images\image-20210225145910431.png)

![image-20210225145922820](E:\hu\Programing\Java\Maven\images\image-20210225145922820.png)

![image-20210225145952419](E:\hu\Programing\Java\Maven\images\image-20210225145952419.png)

![image-20210225150049780](E:\hu\Programing\Java\Maven\images\image-20210225150049780.png)

将这个settings.xml文件复制到.m2文件下

![image-20210225152312913](E:\hu\Programing\Java\Maven\images\image-20210225152312913.png)

## Maven仓库

Maven仓库是基于简单文件系统存储的，集中化管理Java API资源（构件）的一个服务。
仓库中的但可一个码件都有其唯一的坐标,根据这个坐标可以定义其在仓库中的唯一存储路径。得益于Maven的坐标机制，任何Maven项目使用任 何一个构件的方式完全相同的。
Maven可以在某个位置统一存储所有的Maven项目共享的构件，这个统一的位置就是仓库，项目构建完毕后生成的啊件也可以安装或部署到仓库 中，供其它项目使用.
对与Maven来说，仓库分为两类：本地仓库和远程仓库。

### 远程仓库

不在本机中的一切仓库，都是远程仓库：分为中央仓库和本地私服仓库

`默认的远程仓库使用的是Apache提供的中央仓库：`https://mvnrepository.com/

![image-20210225151423209](E:\hu\Programing\Java\Maven\images\image-20210225151423209.png)

![image-20210225151451304](E:\hu\Programing\Java\Maven\images\image-20210225151451304.png)

### 本地仓库

`本地仓库指本地的一份拷贝，用来缓存远程下载，包含你尚未发布的临时构件`

### 在settings.xml中配置本地仓库

打开.m2\repository下的settings.xml文件

![image-20210225152206430](E:\hu\Programing\Java\Maven\images\image-20210225152206430.png)

![image-20210225152407377](E:\hu\Programing\Java\Maven\images\image-20210225152407377.png)

### 在settings.xml中配置镜像仓库

如果仓库A可以提供仓库B存储的所有内容，那么就可以认为A是B的一个镜像。例如：在国内直接连接中央仓库下载一来，由于一些特殊原因下载速度非常慢。这时，我们可以使用阿里云提供的镜像http://maven.aliyun.com/nexus/content/groups/public/来替换中央仓库http://repoLEaven.org/maven2/。修改maven的setting.xml文件，具体内容如下：

```xml
		<mirror>
			<!--指定境像ID （可自己改名）   -->
			<id> nexus-aliyun </id>
			<!-- 匹配中央仓库（阿里云的仓库名称，不可以自己起名，必须这么写）-->
			<mirrorOf> central </mirrorOf>
			<!-- 指定镜像名称（可自己改名）-->
			<name>Nexus aliyun</name>
			<!-- 指定镜像路径（镜像地址）-->
				<url>http://maven.aliyun.com/nexus/content/groups/public</url>
		</mirror>
```

![image-20210225153148726](E:\hu\Programing\Java\Maven\images\image-20210225153148726.png)

![image-20210225153549381](E:\hu\Programing\Java\Maven\images\image-20210225153549381.png)

## 仓库优先级别

优先级别：

![image-20210225153838056](E:\hu\Programing\Java\Maven\images\image-20210225153838056.png)

## jdk配置

当idea中有多个jdk的时候，需要指定编译和运行的jdk

在settings.xml中配置

```xml
	<profile>
		<!-- settings.xml中的id不能随便起的 -->
		<!-- 告诉maven我们用jdk1.8 -->
		<id>jdk-1.8</id>
		<!--开启JDK的使用 -->
		<activation>
			<activeByDefault>true</activeByDefault>
			<jdk>1.8</jdk>
			</activation >
		<properties>
			<!-- 配置编译器信息 -->
			<maven.compiler.source>1.8</maven.compiler.source>
			<maven.compiler.target> 1.8</maven.compiler.target>
			<maven.compiler.compilerVersion > 1.8 </maven.compiler.compilerVersion >
		</properties>
	</profile >
```

## Maven工程类型

### POM工程

POM工程师逻辑工程，用在父级工程或聚合工程中。用来做jar包的版本控制

### JAR工程

将会打包成jar，用作jar包使用。即常见的本地工程

### WAR工程

将会打包成war，发布在服务器上的工程

## 在IDEA中创建Maven工程

![image-20210225155013511](E:\hu\Programing\Java\Maven\images\image-20210225155013511.png)

![image-20210225155458358](E:\hu\Programing\Java\Maven\images\image-20210225155458358.png)

标准目录结构

![image-20210225155712750](E:\hu\Programing\Java\Maven\images\image-20210225155712750.png)

* src/main.java

  这个目录存储Java源代码

* src/main/resources

  存储主要的资源文件。比如xml配置文件和properties文件

* src/test/java

  存储测试用的类

* src/test/resources

  可以自己创建你、储存测试用的资源文件

* src

  包含了项目所有源代码和资源文件，以及其他项目相关的文件。

* target

  编译后内容放置的文件夹

  ![image-20210225160858661](E:\hu\Programing\Java\Maven\images\image-20210225160858661.png)

* pom.xml

  是Maven的基础配置文件。配置项目和项目之间的关系，包括配置依赖关系等等

## POM模式Maven的3种关系

### 依赖

#### 依赖关系

如果A工程开发或运行过程中需要B工程提供支持，则代表A工程依赖B工程。

在这种情况下，需要在A项目的pom.xml文件中增加下属配置定义依赖关系。



![image-20210225161416890](E:\hu\Programing\Java\Maven\images\image-20210225161416890.png)

通俗理解：导入jar包

#### 如何注入依赖

![image-20210225161743879](E:\hu\Programing\Java\Maven\images\image-20210225161743879.png)

可以注入多个依赖

#### 依赖的好处

* 省去了程序员手动添加jar包的操作

* 可以帮我们解决jar冲突问题

#### 依赖的传递性

传递性：A依赖B，B依赖C，所以A也依赖C

案例：

项目1：MavenDemo项目依赖了httpclient的内容

![image-20210225162544349](E:\hu\Programing\Java\Maven\images\image-20210225162544349.png)

注意：将项目1打包为jar包-->重新打包

再创建项目2：让项目2依赖项目1

![image-20210225163011307](E:\hu\Programing\Java\Maven\images\image-20210225163011307.png)

#### 依赖的两个原则

##### 最短路径优先原则

"最短路径优先"意味着项目依赖关系树中路径最短的版本会被使用。
例如，假设A、B、C之间的依赖关系是A->B->C->D(2.0)和A->E->(D1.0),那么D(1.0)会被使用，因为A通过E到D的路径更短。

##### 最先声明原则

依赖路径长度是一样的的时候，第一原则不能解决所有问题，比如这样的依赖关系：A->B->Y(1.0), A->C->Y(2.0), Y(1.0)和Y(2.0)的依赖路径长度是一样的，都为2。那么到底谁会被解析使用呢？在maven2.0.8及之前的版本中，这是不确定的，但是maven2.0.9开始，为了尽可能避免构建的不确定性，maven定义了依赖调解的第二原则：第一声明者优先。在依赖路径长度相等的前提下，在POM中依赖声明的顺序决定了谁会被解析使用。顺序最靠前的那个依赖优胜。

`相同路径长度，选先声明的`

#### 排除依赖

`exclusions:用来排除依赖性传递，可以配置多个exclusion标签，每个标签里面对应的有groupID,artifactID,version三项基本元素。注意：不用写版号`

![image-20210225164313034](E:\hu\Programing\Java\Maven\images\image-20210225164313034.png)

#### 依赖范围

`依赖范围就决定了你依赖的坐标，在什么情况下有效，什么情况下无效`

* compile

  这是默认范围。表示该依赖在编译和运行都有效

* provided

  已提供依赖范围。使用此依赖范围的Maven依赖。

* runtime

  只在运行时生效。典型例子就是JDBC驱动实现

* sytem

  使用本机路径的JAR

* test

  只在编译测试代码和运行代码时的时候需要

* import

  import范围只适用于pom文件中<dependencyManagement>部分。表明指定的POM必须使用<dependencyManagement>部分的依赖。

  注意：import只能用在dependencyManagement的scope里

  定义一个父工程1

![image-20210225165843823](E:\hu\Programing\Java\Maven\images\image-20210225165843823.png)

定义一个子工程

注意：工程1要打包成jar包

![image-20210225170255888](E:\hu\Programing\Java\Maven\images\image-20210225170255888.png)

*如果父工程加入了scope=import 相当于强制的指定了版本号*

### 继承

#### 继承关系

如果A工程继承B工程，则代表A工程默认依赖B工程依赖的所有资源，且可以应用B工程中定义的所有资源信息。
被继承的工程（B工程）只能是POM工程。
注意：在父项目中放在<dependencyManagement>中的内容时不被子项目继承，不可以直会使用
放在<dependencyManagement>中的内容主要目的是进行版本管理。里面的内容在于项目中依赖时坐标只需要填写
<group id>和<artifact id>即可。（注意：如果子项目不希望使用父项目的版本，可以明确配置version）。

### 聚合

#### 聚合关系

总项目：一般为POM项目

![image-20210225172357115](E:\hu\Programing\Java\Maven\images\image-20210225172357115.png)

![image-20210225172406463](E:\hu\Programing\Java\Maven\images\image-20210225172406463.png)

## 常见插件

* settings.xml是全局配置
* 在项目里pom.xml可以使用编译器插件进行再次配置

### 编译器插件

```xml
<bulid>
	<plugin>               		 	
        <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.7.0</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                    <encoding>UTF-8</encoding>
                </configuration>
 	</plugin>
</bulid>
```

### 资源拷贝插件

配置文件一般都放在src/main/resources

然后打包配置文件就会在target的classes放着

![image-20210225173653290](E:\hu\Programing\Java\Maven\images\image-20210225173653290.png)

只有放在resources目录下的配置文件才会被打包放入classes目录里面。

将下面代码配置到<build>中去在src/main/java里的配置文件也会被打包到classes里面

```xml
<resources>
  	<resource>
    	<directory>src/main/java</directory>
    	<includes>
      		<include>**/*.xml</include>
    	</includes>
  </resource>
  <resource>
    	<directory>src/main/resources</directory>
    	<includes>
      		<include>**/*.xml</include>
      		<include>**/*.properties</include>
    	</includes>
  </resource>
</resources>
```

### tomcat插件

