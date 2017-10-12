## 序列化
序列化是一种对象持久化手段，普遍应用在网络传输，rmi等场景中。对象序列化是将对象转化为便于传输的格式，常见的格式有字节数组，json字符串，xml字符串等。
## 反序列化
接收序列化的格式，以相同的方式反序列化，得到传输的对象。
## 如何实现序列化
1、使用到JDK中关键类 ObjectOutputStream 和ObjectInputStream

ObjectOutputStream 类中：通过使用writeObject(Object object) 方法，将对象以二进制格式进行写入。

ObjectInputStream 类中：通过使用readObject（）方法，从输入流中读取二进制流，转换成对象。

2.1、目标对象需要先实现 Seriable接口

```
public class Student implements Serializable {
    private static final long serialVersionUID = 3404072173323892464L;
    private String name;
    private transient String id;
    private String age;

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", id='" + id + '\'' +
                ", age='" + age + '\'' +
                '}';
    }

    public String getAge() {
        return age;
    }

    public void setAge(String age) {
        this.age = age;
    }

    public Student(String name, String id) {
        System.out.println("args Constructor");
        this.name = name;
        this.id = id;
    }

    public Student() {
        System.out.println("none-arg Constructor");
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

}
```



