---
title: log4j configuration
date: 2016-04-27 21:20:09
tags: 
    - log4j
    - hadoop
---

开始学习Hadoop的时候看代码是很枯燥的,就算看懂了对整个系统的流程可能还是不是很了解,这时候从日志文件着手就能快速地了解一个系统是大致流程,Hadoop使用的是log4j这个日志系统,默认的情况下Hadoop不会给每个类记录日志,需要手动的配置.

如果需要配置某一个类的日志输出需要如下的填写方式:

**log4j.logger.类名=日志级别, 自定义名称 log4j.appender.自定义名称**

例如:
+ 配置org.apache.hadoop.yarn.server.nodemanager.containermanager.ContainerManagerImpl类
+ 日志级别为Info
+ 日志名称为ContainerManagerImpl日志使用按天滚动添加
+ 日志文件的日期格式为xxx-dd.log
+ 日志存放位置为${hadoop.log.dir}/ContainerManagerImpl.log

{% codeblock log4j.property lang:xml %}
log4j.logger.org.apache.hadoop.yarn.server.nodemanager.containermanager.ContainerManagerImpl=INFO, ContainerManagerImpl
log4j.appender.ContainerManagerImpl=org.apache.log4j.DailyRollingFileAppender
log4j.appender.ContainerManagerImpl.datePattern='-'dd'.log'
log4j.appender.ContainerManagerImpl.File=${hadoop.log.dir}/ContainerManagerImpl.log
log4j.appender.ContainerManagerImpl.layout=org.apache.log4j.PatternLayout
log4j.appender.ContainerManagerImpl.layout.ConversionPattern=%-6r %d{ISO8601} %-5p %40.40c %x - %m%n
{% endcodeblock %}
