# 一、log jar
##log4j1:

log4j：log4j1的全部内容
##log4j2:

log4j-api:log4j2定义的API
log4j-core:log4j2上述API的实现
##logback:

logback-core:logback的核心包
logback-classic：logback实现了slf4j的API
##commons-logging:

commons-logging:commons-logging的原生全部内容
log4j-jcl:commons-logging到log4j2的桥梁
jcl-over-slf4j：commons-logging到slf4j的桥梁
##slf4j转向某个实际的日志框架:

场景介绍：如 使用slf4j的API进行编程，底层想使用log4j1来进行实际的日志输出，这就是slf4j-log4j12干的事。

slf4j-jdk14：slf4j到jdk-logging的桥梁
slf4j-log4j12：slf4j到log4j1的桥梁
log4j-slf4j-impl：slf4j到log4j2的桥梁
logback-classic：slf4j到logback的桥梁
slf4j-jcl：slf4j到commons-logging的桥梁
##某个实际的日志框架转向slf4j：

场景介绍：如 使用log4j1的API进行编程，但是想最终通过logback来进行输出，所以就需要先将log4j1的日志输出转交给slf4j来输出，slf4j再交给logback来输出。将log4j1的输出转给slf4j，这就是log4j-over-slf4j做的事

这一部分主要用来进行实际的日志框架之间的切换（下文会详细讲解）

jul-to-slf4j：jdk-logging到slf4j的桥梁
log4j-over-slf4j：log4j1到slf4j的桥梁
jcl-over-slf4j：commons-logging到slf4j的桥梁

# 二、集成总结

##commons-logging与其他日志框架集成

1 commons-logging与jdk-logging集成：
需要的jar包：
commons-logging

2 commons-logging与log4j1集成：
需要的jar包：
commons-logging
log4j

3 commons-logging与log4j2集成：
需要的jar包：
commons-logging
log4j-api
log4j-core
log4j-jcl(集成包)

4 commons-logging与logback集成：
需要的jar包：
logback-core
logback-classic
slf4j-api、jcl-over-slf4j(2个集成包,可以不再需要commons-logging)

5 commons-logging与slf4j集成：
需要的jar包：
jcl-over-slf4j(集成包，不再需要commons-logging)
slf4j-api
## slf4j与其他日志框架集成

1 slf4j与jdk-logging集成：
需要的jar包：
slf4j-api
slf4j-jdk14(集成包)

2 slf4j与log4j1集成：
需要的jar包：
slf4j-api
log4j
slf4j-log4j12(集成包)

3 slf4j与log4j2集成：
需要的jar包：
slf4j-api
log4j-api
log4j-core
log4j-slf4j-impl(集成包)

4 slf4j与logback集成：
需要的jar包：
slf4j-api
logback-core
logback-classic(集成包)

5 slf4j与commons-logging集成：
需要的jar包：
slf4j-api
commons-logging
slf4j-jcl(集成包)

# 三、参考案例
[https://my.oschina.net/pingpangkuangmo/blog/410224#comment-list]

# 四、 背景
由于现在开源框架日益丰富，好多开源框架使用的日志组件不尽相同。存在着在一个项目中，不同的版本，不同的框架共存。导致日志输出异常混乱。虽然也不至于对系统造成致命伤害，但是明显可以看出，架构不够精良，追求极致略有不足。其中有一些标准通用接口，标准实现，各种桥接器的存在。

# 五、slf4J与旧日志框架的关系

1 slf4j等于commons-logging，是各种日志实现的通用入口，会根据classpath中存在下面哪一个Jar来决定具体的日志实现库。 

logback-classic(默认的logback实现) 

slf4j-jcl.jar(apache commons logging) 

slf4j-logj12.jar(log4j 1.2.4) 

slf4j-jdk14(java.util.logging) 
2 将所有使用旧式日志API的第三方类库或旧代码的日志调用转到slfj 

jcl-over-slf4j.jar/jcl104-over-slf4j：apache commons logging 1.1.1/1.0.4，直接替换即可。 

log4j-over-slf4j.jar：log4j，直接替换即可。 

jul-to-slf4j：jdk logging，需要在程序开始时调用
SLF4JBridgeHandler.install()来注册listener参考JulOverSlf4jProcessor，可在applicationContext.xml中定义该bean来实现初始化。注意原有Alog4j.properites将失效，logback网站上提供转换器，支持从log4j.properties 转换到logback.xml 。 

# 六、转移到logback的理由 
slf4j支持参数化的logger.error("帐号ID：{}不存在", userId);告别了if(logger.isDebugEnable()) 时代。 
另外logback的整体性能比log4j也较佳，hibernate等项目已经采用了slf4j:
某些关键操作，比如判定是否记录一条日志语句的操作，其性能得到了显著的提高。这个操作在LOGBack中需要3纳秒，而在Log4J中则需要30纳秒。 LOGBack创建记录器（logger）的速度也更快：13毫秒，而在Log4J中需要23毫秒。更重要的是，它获取已存在的记录器只需94纳秒，而 Log4J需要2234纳秒，时间减少到了1/23。


   