## bug1
严重: Exception starting filter struts2
java.lang.RuntimeException: java.lang.RuntimeException: java.lang.reflect.InvocationTargetException - Class: com.opensymphony.xwork2.inject.ContainerBuilder$4
File: ContainerBuilder.java
Method: create
Line: 131 - com/opensymphony/xwork2/inject/ContainerBuilder.java:131:-1
	at org.apache.struts2.dispatcher.Dispatcher.init(Dispatcher.java:499)
	at org.apache.struts2.dispatcher.InitOperations.initDispatcher(InitOperations.java:75)
	at org.apache.struts2.dispatcher.filter.StrutsPrepareAndExecuteFilter.init(StrutsPrepareAndExecuteFilter.java:63)
	at org.apache.catalina.core.ApplicationFilterConfig.initFilter(ApplicationFilterConfig.java:279)
	at org.apache.catalina.core.ApplicationFilterConfig.getFilter(ApplicationFilterConfig.java:260)
	at org.apache.catalina.core.ApplicationFilterConfig.<init>(ApplicationFilterConfig.java:105)
	at org.apache.catalina.core.StandardContext.filterStart(StandardContext.java:4908)
	at org.apache.catalina.core.StandardContext.startInternal(StandardContext.java:5602)
	at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:147)
	at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1572)
	at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1562)
	at java.util.concurrent.FutureTask.run(Unknown Source)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source)
	at java.lang.Thread.run(Unknown Source)
Caused by: java.lang.RuntimeException: java.lang.RuntimeException: java.lang.RuntimeException: java.lang.reflect.InvocationTargetException
	at com.opensymphony.xwork2.inject.ContainerBuilder$4.create(ContainerBuilder.java:131)
	at com.opensymphony.xwork2.inject.Scope$2$1.create(Scope.java:52)
	at com.opensymphony.xwork2.inject.ContainerImpl.getInstance(ContainerImpl.java:491)
	at com.opensymphony.xwork2.inject.ContainerImpl.getInstance(ContainerImpl.java:501)
	at com.opensymphony.xwork2.inject.ContainerImpl$9.call(ContainerImpl.java:532)
	at com.opensymphony.xwork2.inject.ContainerImpl.callInContext(ContainerImpl.java:560)
	at com.opensymphony.xwork2.inject.ContainerImpl.getInstance(ContainerImpl.java:530)
	at com.opensymphony.xwork2.config.impl.DefaultConfiguration.reloadContainer(DefaultConfiguration.java:180)
	at com.opensymphony.xwork2.config.ConfigurationManager.getConfiguration(ConfigurationManager.java:67)
	at org.apache.struts2.dispatcher.Dispatcher.getContainer(Dispatcher.java:906)
	at org.apache.struts2.dispatcher.Dispatcher.init_PreloadConfiguration(Dispatcher.java:445)
	at org.apache.struts2.dispatcher.Dispatcher.init(Dispatcher.java:486)
	... 14 more
Caused by: java.lang.RuntimeException: java.lang.RuntimeException: java.lang.reflect.InvocationTargetException
	at com.opensymphony.xwork2.inject.ContainerImpl.inject(ContainerImpl.java:479)
	at com.opensymphony.xwork2.inject.ContainerImpl$7.call(ContainerImpl.java:516)
	at com.opensymphony.xwork2.inject.ContainerImpl.callInContext(ContainerImpl.java:569)
	at com.opensymphony.xwork2.inject.ContainerImpl.inject(ContainerImpl.java:514)
	at com.opensymphony.xwork2.config.impl.LocatableFactory.create(LocatableFactory.java:32)
	at com.opensymphony.xwork2.inject.ContainerBuilder$4.create(ContainerBuilder.java:129)
	... 25 more
Caused by: java.lang.RuntimeException: java.lang.reflect.InvocationTargetException
	at com.opensymphony.xwork2.inject.ContainerImpl$ConstructorInjector.construct(ContainerImpl.java:427)
	at com.opensymphony.xwork2.inject.ContainerImpl.inject(ContainerImpl.java:477)
	... 30 more
Caused by: java.lang.reflect.InvocationTargetException
	at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance(Unknown Source)
	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(Unknown Source)
	at java.lang.reflect.Constructor.newInstance(Unknown Source)
	at com.opensymphony.xwork2.inject.ContainerImpl$ConstructorInjector.construct(ContainerImpl.java:410)
	... 31 more
Caused by: java.lang.NoSuchMethodError: com.opensymphony.xwork2.spring.SpringObjectFactory.<init>(Lcom/opensymphony/xwork2/inject/Container;)V
	at org.apache.struts2.spring.StrutsSpringObjectFactory.<init>(StrutsSpringObjectFactory.java:74)
	... 36 more
	
头文件
<!DOCTYPE struts PUBLIC
	"-//Apache Software Foundation//DTD Struts Configuration 2.5//EN"
	"http://struts.apache.org/dtds/struts-2.5.dtd">导致
改成
<!DOCTYPE struts PUBLIC
	"-//Apache Software Foundation//DTD Struts Configuration 2.3//EN"
	"http://struts.apache.org/dtds/struts-2.3.dtd">