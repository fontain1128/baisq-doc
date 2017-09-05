## Schema规范
1.所有标签和属性都需要schema文件来定义
2.所有与的schema文件都需要有一个id,但在这里叫他namespace
3.namespace的值由什么来指定？
    由targetNameSpace属性来指定,他的值是一个url（很有可能不存在）
4.如何引入一个Schema约束?
    属性：用xmlns属性
    属性值：对应的schema文件的id（namespace值）

5.如果引入的schema不是w3c组织定义，必须指定schema文件的位置
6.schema文件的位置由什么属性指定？
    属性?：schemalocation
    属性值：namespace path
7.如果引入了N个约束,需要给n-1个起别名    

