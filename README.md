# maven 学习
Maven是基于项目对象模型（POM），可以通过一小段描述信息，来管理项目的<font color="red">构建</font>，<font color="red">报告</font>，<font color="red">文档</font>的项目管理工具。

## 下载和安装
1. 下载：[Maven官网](http://maven.apache.org/download.cgi)
2. 解压后配置**M2_HOME**

## 修改镜像与本地仓库
如果你第一次使用maven你可以再conf目录下找到setting.xml文件。  
修改以下标签
```xml
<mirror>
    <id>alimaven</id>
    <name>aliyun maven</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
    <mirrorOf>central</mirrorOf>
</mirror>

<localRepository>D:\data\maven</localRepository>
```
## 使用archetype生成项目骨架
```shell
mvn archetype:generate
```

ProjectName  
  -src  
  -|---main  
  -|---|---java        —— 存放项目的.java文件  
  -|---|---resources   —— 存放项目资源文件，如spring,   hibernate配置文件  
  -|---test  
  -|------java        ——存放所有测试.java文件，如JUnit测试类  
  -|------resources   —— 测试资源文件  
  -resources   —— 测试资源文件  
  -target             —— 目标文件输出位置例如.class、.jar、.war文件  
  -pom.xml           ——maven项目核心配置文件  



## 基本命令介绍
1. mvn compile 生成字节码文件
2. mvn clean 删除target目录
3. mvn test 生成三个文件夹：surefire、surefire-reports（测试报告）、test-classes（测试的字节码文件）
4. mvn package 生成jar、war
5. mvn install 将打好的jar包安装到本地仓库

## mvn 组合命令
1. mvn clean compile
2. mvn clean test
3. mvn clean package
4. mvn clean install

## 坐标
1. groupId：定义当前Maven组织名称
2. artifactId：定义实际项目名称
3. version：定义当前项目的当前版本

你可以在[https://mvnrepository.com/](https://mvnrepository.com/)或者[http://search.maven.org/](http://search.maven.org/)搜索到项目坐标

## 生命周期
Maven生命周期就是为了对所有的构建过程进行抽象和统一。  
包括项目清理、初始化、编译、打包、测试、部署等几乎所有构建步骤。  
生命周期可以理解为构建工程的步骤。  

**在Maven中有三套相互独立的生命周期，请注意这里说的是“三套”，而且“相互独立”，这三套生命周期分别是：**   
1. Clean： 在进行真正的构建之前进行一些清理工作。 
2. Default： 构建的核心部分，编译，测试，打包，部署等等。 
3. Site： 生成项目报告，站点，发布站点。 

## maven插件
1. 默认插件  

| plugin | function | life cycle phase |
| ------ | ------ | ------ |
| maven-clean-plugin | 清理target文件 | clean |
| maven-resources-plugin | 处理资源文件 | resources,testResources |
| maven-compiler-plugin | 编译Java代码 | compile、testCompile |
| maven-surefire-plugin | 执行单元测试文件 | test |
| maven-jar-plugin | 创建 jar | package |
| maven-install-plugin | 拷贝jar到本地的maven仓库 | install |
| maven-deploy-plugin | 发布 jar | deploy |
| maven-site-plugin | 生成文档 | site |

2. 常用插件
- Tomcat插件
- ...

## 基本元素
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- 项目根目录 -->
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <!-- 指定当前pom版本 -->
    <modelVersion>4.0.0</modelVersion>  
    <!-- 反写的公司网址 -->
    <groupId>com.deppon.uap</groupId>
    <!-- 项目+模块名 -->
    <artifactId>uap-parent</artifactId>
    <!-- 版本
      0.0.1 大版本.分支版本.小版本
      snapshort快照
      alpha内测版
      beta公测版
      relaese稳定版
      GA正式发布版
     -->
    <version>1.0.0</version>
    <!-- 打包方式 -->
    <packaging>pom</packaging>
    <!-- 项目描述名 -->
    <name></name>
    <!-- 项目地址 -->
    <url></url>
    <!-- 项目描述 -->
    <description></description>
    <!-- 项目开发者 -->
    <developers></developers>
    <!-- 许可证 -->
    <licenses></licenses>
    <!-- 组织 -->
    <organization></organization>
    <!-- 聚合模块，一起打包 -->
    <modules>
        <module>uap-framework</module>
        ...
    </modules>
    <!-- 属性变量 -->
    <properties>
        <!-- Dependency Versions -->
        <slf4j.version>1.7.24</slf4j.version>
    </properties>
    <!-- 依赖 -->
    <dependencies>
        <!-- slf4j api -->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <!-- 依赖范围 -->
            <scope></scope>
            <!-- 是否继承依赖 -->
            <option></option>
            <!-- 排除依赖 -->
            <exclutions>
              <exclution></exclution>
            </exclutions>
        </dependency>
        ...
    </dependencies>


    <!-- 依赖管理定义在父模块，供给子项目调用 -->
    <dependencyManagement>
        <dependencies>
            <!-- slf4j api -->
            <dependency>
                <groupId>org.slf4j</groupId>
                <artifactId>slf4j-api</artifactId>
                <version>${slf4j.version}</version>
            </dependency>
            ...
        </dependencies>
    </dependencyManagement>


    <distributionManagement>
        <repository>
            <id>releases</id>
            <url>http://192.168.17.183:8081/nexus/content/repositories/releases/</url>
            <layout>default</layout>
        </repository>
        <snapshotRepository>
            <id>snapshots</id>
            <url>http://192.168.17.183:8081/nexus/content/repositories/snapshots/</url>
            <layout>default</layout>
        </snapshotRepository>
    </distributionManagement>
    <!-- 父级依赖 -->
    <parent></parent>
    <build>
      <!-- 插件列表 -->
      <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-resources-plugin</artifactId>
        </plugin>
      </plugins>
        <!-- 插件管理 -->
        <pluginManagement>
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <version>${maven-compiler-plugin.version}</version>
                    <configuration>
                        <source>${java.version}</source>
                        <target>${java.version}</target>
                        <meminitial>512m</meminitial>
                        <maxmem>1024m</maxmem>
                        <fork>true</fork>
                        <encoding>${project.encoding}</encoding>
                    </configuration>
                    <executions>
                        <execution>
                            <id>default-testCompile</id>
                            <phase>test-compile</phase>
                            <goals>
                                <goal>testCompile</goal>
                            </goals>
                            <configuration>
                                <skip>false</skip>
                            </configuration>
                        </execution>
                    </executions>
                </plugin>
            </plugins>
        </pluginManagement>
        
    </build>
</project>

```

## 依赖范围
scope:  

**1. compile:** 默认使用该依赖范围,编译、测试、运行三种classpath都有效  
**2. test:** 只对于测试classpath有效，在编译或者运行项目时无效,eg: Jnuit    
**3. provided:** 编译和测试classpath有效，运行时无效 eg: servlet-api在运行时，容器已经提供该依赖 , 无需重新引入。  
**4. runtime:** 测试和运行classpath有效，编译主时无效,eg: JDBC驱动实现类 ，编译时只需要JDK提供的JDBC接口  
**5. system:** 编译和测试classpath有效，运行时无效，system依赖必须通过systemPath元素显示地指定依赖文件的路径。  
**6. import:** 该依赖范围不会对三种classpath产生实际的影响。   


## 依赖传递
假设A依赖于B,B依赖于C，我们说A对于B是第一直接依赖，B对于C是第二直接依赖，A对于C是传递性依赖。**第一直接依赖和第二直接依赖的范围决定了传递性依赖的范围，** 如下图所示，最左边一行表示第一直接依赖范围，最上面一行表示第二直接依赖范围，中间的交叉单元格则表示传递依赖范围。


|| compile | test | provided | runtime |  
| ------ | ------ | ------ |------|-----|
| compile | compile | --- |---|runtime|
| test | test | --- |---|test|
| provided | provided | --- |provided|provided|
| runtime | runtime | --- |---|runtime|


1. 短路优先:  
A->B->C->X(0.0.1)  
A->D->X(0.0.2)  
2. 先声明优先  


## 依赖冲突
1. 排除依赖
2. 可选依赖
3. 依赖传递

## 聚合与继承
1. modules 一起构建
2. parent 继承父项目







