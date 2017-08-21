# 一、 背景
由于现在开源框架日益丰富，好多开源框架使用的日志组件不尽相同。存在着在一个项目中，不同的版本，不同的框架共存。导致日志输出异常混乱。虽然也不至于对系统造成致命伤害，但是明显可以看出，架构不够精良，追求极致略有不足。其中有一些标准通用接口，标准实现，各种桥接器的存在。

# 二、slf4J与旧日志框架的关系

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

# 三、转移到logback的理由 
slf4j支持参数化的logger.error("帐号ID：{}不存在", userId);告别了if(logger.isDebugEnable()) 时代。 
另外logback的整体性能比log4j也较佳，hibernate等项目已经采用了slf4j:
某些关键操作，比如判定是否记录一条日志语句的操作，其性能得到了显著的提高。这个操作在LOGBack中需要3纳秒，而在Log4J中则需要30纳秒。 LOGBack创建记录器（logger）的速度也更快：13毫秒，而在Log4J中需要23毫秒。更重要的是，它获取已存在的记录器只需94纳秒，而 Log4J需要2234纳秒，时间减少到了1/23。

# 四、参考链接
[http://phl.iteye.com/blog/2021461]

