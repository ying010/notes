# 背景：

[PageHelper](https://gitee.com/free/Mybatis_PageHelper)是一款好用的开源免费的Mybatis第三方物理分页插件，使用PageHelper可以十分便捷的做到分页并获取到记录总数。但是PageHelper怎么做到的，查出所有数据在内存中操作，还是直接修改了sql语句，总条数怎么获取的这是值得深入探索的。

在查看PageHelper代码过程中发现，他基于Mybatis的拦截器，对原生sql进行了改造，首先根据自定义的查询总条数语句查出总条数，然后在原生sql基础上拼接了limit，将查询结果从list转换为了Page记录信息。

# 一、Mybatis拦截器

MyBatis提供的拦截器接口可以方便用户自由扩展编写各种插件，PageHelper就是通过实现MyBatis中的Interceptor接口。具体MyBatis拦截器的原理参见上一篇。

# 二、PageHelper的使用

可以选择以下两个方式引入PageHelper，更详细的配置信息请参见[官方文档](https://pagehelper.github.io/docs/howtouse/)

## 2.1. 修改配置的方式引入PageHelper

引入PageHelper核心包并通过修改配置文件的方式使其生效。

### 2.1.1 引入maven

在 pom.xml 中添加如下依赖：

```xml
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper</artifactId>
    <version>最新版本</version>
</dependency>
```

### 2.1.2 修改配置文件

使用以下两种方式的其中一种即可

#### 2.1.21 修改MyBatis的配置文件

```
<plugins>
    <!-- com.github.pagehelper为PageHelper类所在包名 -->
    <plugin interceptor="com.github.pagehelper.PageInterceptor">
        <!-- 使用下面的方式配置参数，详细参数介绍见官方文档 -->
        <property name="param1" value="value1"/>
	</plugin>
</plugins>
```

#### 2.1.22 修改Spring的配置文件

```xml
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
  <!-- 注意其他配置 -->
  <property name="plugins">
    <array>
      <bean class="com.github.pagehelper.PageInterceptor">
        <property name="properties">
          <!--使用下面的方式配置参数，一行配置一个 -->
          <value>
            params=value1
          </value>
        </property>
      </bean>
    </array>
  </property>
</bean>
```

## 2.2. PageHelper与SpringBoot整合

PageHelper已与SpringBoot整合，并提供了pagehelper-spring-boot-starter启动，使用这个方式引入pagehelper时，只需要引入该启动即可，SpringBoot会以自动配置的方式使PageHelper生效

### 2.2.1 maven

由于pagehelper-spring-boot-starter依赖了mybatis-spring-boot-starte，如果害怕冲突的同学可以将mybatis启动去除

```xml
<dependency>
  <groupId>com.github.pagehelper</groupId>
  <artifactId>pagehelper-spring-boot-starter</artifactId>
  <version>1.3.0</version>
  <exclusions>
    <exclusion>
      <groupId>org.mybatis.spring.boot</groupId>
      <artifactId>mybatis-spring-boot-starter</artifactId>
    </exclusion>
  </exclusions>
</dependency>
```

## 2.3. 代码中使用PageHelper

```java
PageHelper.startPage(1, 10);
List<Map> mapList = mapper.selectSomeList();
PageInfo pageInfo = new PageInfo(mapList);
```

PageInfo中封装了总记录数、当前页、结果集等信息

# 三、源码分析

