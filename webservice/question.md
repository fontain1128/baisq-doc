##Web Service 是什么
1基于Web的服务,服务端整出一些资源让客户端应用访问(获取数据)
2一个跨语言,跨平台的规范(抽象)
3多个跨平台,跨语言的应用间通信整合的方案(实际)

以各个网站显示天气预报功能为例：
气象中心的管理系统将收集的天气信息并将数据暴露出来(通过WebService Server),而各大站点的应用就去调用它们得到天气信息以不同的样式去展示(WebService Client),其实网站提供天气预报的服务，只是简单的调用了气象中心暴露的服务(一段代码);

## 为什么要用
1跨平台调用
2跨语言调用
3远程调用

##什么时候用
同一家公司新旧项目之间调用
不同公司的应用之间(淘宝上(淘宝应用)显示物流(顺丰应用)信息)

## webService 原理
http+xml 
请求体和响应体是http+xml形式

## WSDL
WebService定义语言
1对应一种类型的文件.wsdl
2定义了web service 的服务端与客户端应用交互传递请求和响应数据的格式和方式
3一个web service 对应一个唯一的 wsdl文档

## SOAP 
简单对象访问协议
1是一种简单的，基于http和xml的协议,用于在web上交换结构化的数据
2soap消息：请求消息和响应消息
3http+xml片段

##SEI WebService EndPointInterface(终端)
web service的终端接口
1就是WebService服务端用来处理请求的接口

## CXF(框架):Celtix(后来加入这个框架作为辅助)+XFire(以前只有XFire一个框架)
一个apache的用于开发webService服务端和客户端的框架

