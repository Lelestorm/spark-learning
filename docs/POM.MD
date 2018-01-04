
## [官方文档](https://maven.apache.org/pom.html) 

 Project Object Model，项目对象模型，通过xml格式描述程序之间的依赖和程序管理相关信息，一般在阅读项目时需要先大致看下root模块的pom文件，便于理解程序的结构
 * 声明规范
 * GAV标识
 * 基本信息
 > * name：项目的名称
 > * description：描述
 > * url：项目主页
 > * inceptionYear：创建年份
 > * licenses：licenses信息
 > * developers：项目开发者列表
 > * contributors：其他贡献者列表
 > * organization：项目所属组织信息
 * 包类型：packaging （pom , jar , maven-plugin , ejb , war , ear , rar , par），默认jar
 * 模块： modules（子模块） / parent（父级模块）
 * 依赖列表：dependencies（[详情参考依赖机制](https://maven.apache.org/pom.html#Dependencies)）
 * 属性和自定义变量：properties <!--键值对，Properties可以在整个POM中使用，也可以作为触发条件（见settings.xml配置文件里profiles→properties元素的说明）。格式是<name>value</name>。-->
 * 编译设置：build
 * 环境配置
 
 
 ```xml
 <!-- 声明规范 -->
 <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <!-- 描述maven版本信息，现在唯一支持maven2、maven3的版本 -->
  <modelVersion>4.0.0</modelVersion>
   
  <!-- 要引用的父模块, 只有子模块用到 -->
  <!--
  <parent>
     <artifactId>com.jky.xht</artifactId>
     <groupId>com.jky.xht</groupId>
     <version>0.0.1-SNAPSHOT</version>
     //父项目的pom.xml文件的相对路径,默认值是../pom.xml。Maven首先在构建当前项目的地方寻找父项目的pom，其次在文件系统的这个位置（relativePath位置），然后在本地仓库，最后在远程仓库寻找父项目的pom
     <relativePath>../pom.xml</relativePath>
  </parent>
  -->
	
  <!-- groupId在一个组织或项目中通常是特有的。例如：(大概、也许)Maven所有artifacts的groupId都使用org.apache.maven。groupId并不一定必须使用点符号，例如，JUnit项目。注意使用点符号的groupId不必与项目的包结构相同，但它是一个很好的做法。 -->
  <groupId>com.jky.xht</groupId>
  <!--artifactId一般是该项目的名字。它和groupID一起标识一个唯一的项目。换句话说，你不能有两个不同的项目拥有同样的artifactID和groupID；在某个特定的groupID下，artifactID也必须是唯一的。-->
  <artifactId>com.jky.xht</artifactId>
  <!--这是命名的最后一段。groupId：artifactId表示单个项目，但它们无法描绘具体的版本。如：我想要junit:junit项目今天第四版。version定义当前项目的版本，如：1.0（-SNAPSHOT），SNAPSHOT表示快照，说明该项目还处于开发阶段，是不稳定版本；建议version格式为:主版本.次版本.增量版本-限定版本号-->
  <version>0.0.1-SNAPSHOT</version>
  <!-- 项目名称 -->
  <name>XHT</name>
  
  <!--包类型 ： 项目产生的构件类型，例如jar、war、ear、pom等等。插件可以创建他们自己的构件类型，所以前面列的不是全部构件类型。默认值jar。-->
  <packaging>jar</packaging>
	
  <!-- 开发人员列表 -->
  <developers>
   <developer>
    <id>dtl</id>
    <name>iuhart</name>
    <email>iuhart@163.com</email>
   </developer>
  </developers>
	
  <!-- 模块列表 -->
  <modules>
    <!-- 基础模块，包含公共函数，提供给其他模块使用 -->
    <module>base</module>
    <!-- 做为其他模块的父pom，会引用base模块 -->
    <module>public</module>
  </modules>
	
  <!-- 属性和自定义变量 -->
  <properties>
    <!--文件拷贝时的编码-->
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
    <!--编译时的编码-->
    <maven.complier.encoding>UTF-8</maven.complier.encoding>
    <!-- pom所在目录 -->
    <project.home>${basedir}</project.home>
    <!-- 几个依赖的scope -->
    <dep.scope>provided</dep.scope>
  </properties>

  <!-- 依赖管理 详情参考依赖机制-->
  <dependencies>
	<dependency>
	    <groupId>org.scala-lang</groupId>
	    <artifactId>scala-library</artifactId>
	    <!--依赖的版本号。可以配置成确定的版本号,也可以配置成版本号的范围。(, )不包含 [, ]包含 例如：(3.8,4.0) 表示3.8 - 4.0的版本，但是不包含4.0-->
	    <version>2.11.8</version>
	</dependency>
	
	<dependency>
	    <groupId>org.apache.spark</groupId>
	    <artifactId>spark-core_2.11</artifactId>
	    <version>2.0.2</version>
	</dependency>
	
  	<dependency>
	    <groupId>mysql</groupId>
	    <artifactId>mysql-connector-java</artifactId>
	    <version>5.1.42</version>
	</dependency>
  </dependencies>

  <!-- 编译配置 -->
  <build>
        <resources>
            <!-- 使资源文件可以引用pom文件中的自定义变量 -->
            <resource>
                <directory>src/main/resources</directory>
                <filtering>true</filtering>
            </resource>
        </resources>

        <!-- 插件列表 -->
        <plugins>
            <!-- scala编译插件 -->
            <plugin>
                <groupId>org.scala-tools</groupId>
                <artifactId>maven-scala-plugin</artifactId>
                <version>2.15.2</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>compile</goal>
                            <!-- 如果要使用测试代码，启用下面的goal -->
                            <goal>testCompile</goal>
                        </goals>
                        <configuration>
                            <!-- 消除Multiple versions of scala libraries detected!报错 -->
                            <checkMultipleScalaVersions>false</checkMultipleScalaVersions>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```
