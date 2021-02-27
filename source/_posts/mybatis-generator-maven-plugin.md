---
title: mybatis-generator-maven-plugin配置
date: 2021-02-26 17:59:18
tags:
---
### pom.xml配置

配置maven
```xml
<!-- mybatis generator -->
<plugin>
    <groupId>org.mybatis.generator</groupId>
    <artifactId>mybatis-generator-maven-plugin</artifactId>
    <version>1.4.0</version>
    <configuration>
        <!--mybatis generator插件配置文件位置，默认值${basedir}/src/main/resources/generatorConfig.xml-->
        <configurationFile>${basedir}/src/main/resources/generator/generatorConfig.xml</configurationFile>
        <overwrite>true</overwrite>
        <verbose>true</verbose>
    </configuration>
    <dependencies>
        <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.49</version>
        </dependency>
    </dependencies>
</plugin>
```

### generatorConfig.xml配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">

<generatorConfiguration>
    <!--参数配置-->
    <properties resource="generator/generator.properties"/>
    <!--驱动jar-->
<!--    <classPathEntry location="${classPathEntry}"/>-->

    <context id="OracleTables" targetRuntime="MyBatis3">

        <!-- 解决每次都会生成的重复的xml 代码文件 -->
        <!--覆盖生成XML文件-->
        <plugin type="org.mybatis.generator.plugins.UnmergeableXmlMappersPlugin" />
        <!-- 生成的实体类添加toString()方法 -->
        <plugin type="org.mybatis.generator.plugins.ToStringPlugin" />

        <!-- 不生成注释 -->
        <commentGenerator>
            <property name="suppressAllComments" value="true"/>
        </commentGenerator>

        <jdbcConnection driverClass="${driverClass}" connectionURL="${connectionURL}" userId="${userId}" password="${password}">
        </jdbcConnection>

        <javaTypeResolver>
            <property name="forceBigDecimals" value="false"/>
        </javaTypeResolver>

        <javaModelGenerator targetPackage="${modelTargetPackage}" targetProject="src/main/java">
            <property name="enableSubPackages" value="true"/>
            <property name="trimStrings" value="true"/>
        </javaModelGenerator>

        <sqlMapGenerator targetPackage="{sqlMapTargetPackage}" targetProject="src/main/resources">
            <property name="enableSubPackages" value="true"/>
        </sqlMapGenerator>

        <javaClientGenerator type="XMLMAPPER" targetPackage="${javaClientTargetPackage}" targetProject="src/main/java">
            <property name="enableSubPackages" value="true"/>
        </javaClientGenerator>

        <table enableCountByExample="false" enableUpdateByExample="false"
               enableDeleteByExample="false" enableSelectByExample="false"
               selectByExampleQueryId="false" tableName="${tableName}" domainObjectName="${domainObjectName}">
        </table>

    </context>
</generatorConfiguration>
```

### generator.properties配置

```properties
connectionURL=jdbc:mysql://localhost:3306/test_db?characterEncoding=utf-8&useSSL=false
userId=root
password=19930205
driverClass=com.mysql.jdbc.Driver
# 实体类
modelTargetPackage=com.example.springbootdemo.domin
# mapping文件
sqlMapTargetPackage=mybatis/sqlmap
# mapper类
javaClientTargetPackage=com.example.springbootdemo.mapper
# 哪个用户的表
tableName=t_user
domainObjectName=User
```