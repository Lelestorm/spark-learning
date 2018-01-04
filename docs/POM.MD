 Project Object Model，项目对象模型，通过xml格式描述程序之间的依赖和程序管理相关信息，一般在阅读项目时需要先大致看下root模块的pom文件，便于理解程序的结构
 '''xml
 <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <!-- 描述maven版本信息，现在唯一支持maven2、maven3的版本 -->
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.jky.xht</groupId>
  <artifactId>com.jky.xht</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <name>XHT</name>
  
  
  <dependencies>
	<dependency>
	    <groupId>org.scala-lang</groupId>
	    <artifactId>scala-library</artifactId>
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
</project>
 '''
