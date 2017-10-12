## Web Service 是什么

1基于Web的服务,服务端整出一些资源让客户端应用访问\(获取数据\)  
2一个跨语言,跨平台的规范\(抽象\)  
3多个跨平台,跨语言的应用间通信整合的方案\(实际\)

以各个网站显示天气预报功能为例：  
气象中心的管理系统将收集的天气信息并将数据暴露出来\(通过WebService Server\),而各大站点的应用就去调用它们得到天气信息以不同的样式去展示\(WebService Client\),其实网站提供天气预报的服务，只是简单的调用了气象中心暴露的服务\(一段代码\);

## 为什么要用

1跨平台调用  
2跨语言调用  
3远程调用

## 什么时候用

同一家公司新旧项目之间调用  
不同公司的应用之间\(淘宝上\(淘宝应用\)显示物流\(顺丰应用\)信息\)

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

## SEI WebService EndPointInterface\(终端\)

web service的终端接口  
1就是WebService服务端用来处理请求的接口

## CXF\(框架\):Celtix\(后来加入这个框架作为辅助\)+XFire\(以前只有XFire一个框架\)

一个apache的用于开发webService服务端和客户端的框架

## 服务端要一直开启webService服务
客户端生成代码根据wsdl文档

## 监听请求使用eclipse的TCP/IP工具(端口转发器)

1.将服务器端的wsdl文档保存到客户端本地
2.修改文档：将端口号从8989改为8080
3.根据本地的wsdl文档生成客户端代码，并编写客户端的调用代码
4.配置eclipse的TCP/IP，启动监听。
5.执行客户端代码发送WebService请求(SOAP请求(POST)，SOAP响应)

## undefined element declaration 's:schema'
webService 可能是.net开发的,需要本地修改wsdl文档中的 s:schema = ""..
为<s:any minOccurs="2" maxOccurs="2"></s:any>

## wsdl深入浅出
<defination>
    <types>
        <schema> -- 定义约束
            <element>
    </types>
    <message> -- 请求消息，响应消息结构
        <part>
    </message>
    <portType> -- 接口(一个接口就是一个端口类型)
        <operation>
            <input>
            <output>
    </portType>
    <binding> -- 接口实现类
        <operation>
            <input>
            <output>
    </binging>
    <service> -- 提供实现

## 详情参考wsdl文档
外部引用约束
<types>
    //内部也定义了约束
    //用于请求
    <sayHello>
        <arg0>String</arg0>
    </sayHello>
    
    //用于响应
    <sayHelloResponse>
        <return>String</return>
    </sayHelloResponse>
</types>

message:用来定义消息的结构
    part:指定引用types中定义的标签片段

portType :用来定义服务器端的SEI 接口名
    operation(操作对应行为)：用来指定SEI中的处理请求的方法
        input:指定客户端应用传过来的数据，会引用上面定义的message标签
        output:指定服务器端返回给客户端的数据，会引用上面的message标签
        
binding:用来定义SEI的实现类
    type属性：引用上面定义的portType标签
    <soap:binding style="document"> :绑定的数据是一个document(xml)
    <operation>:用来定义实现类的方法
        <soap:operation style= "document">传输的是document(xml)
        input:
            <soap:body use="literal">:传输的是一个xml形式的文本数据
        output:指定服务器端返回给客户端的数据
            <soap : body use="literal"/>:文本数据

service:服务器端的一个webService的容器
    name属性：它用于指定客户端容器类
    port:用来指定一个服务器端处理请求的入口(SEI的实现)
        binding属性：引用上面定义的<binding>
        address:当前webService的请求地址
     
        
        
         
    
