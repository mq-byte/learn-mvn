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
  |-src  
  |---|-main  
  |---|---|-java        —— 存放项目的.java文件  
  |---|---|-resources   —— 存放项目资源文件，如spring,   hibernate配置文件  
  |---|-test 
  |------|-java        ——存放所有测试.java文件，如JUnit测试类  
  |------|-resources   —— 测试资源文件  
  |-target             —— 目标文件输出位置例如.class、.jar、.war文件  
  |-pom.xml           ——maven项目核心配置文件  



## 基本命令介绍
1. mvn compile 生成字节码文件
2. mvn clean target目录删除
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

		
		
	处理资源文件	
	编译Java代码	
	执行单元测试文件	test
maven-jar-plugin	创建 jar	package
maven-install-plugin	拷贝jar到本地的maven仓库 .m2/repository 下面	install
maven-deploy-plugin	发布 jar	deploy
maven-site-plugin	生成文档	site