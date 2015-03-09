

>"别名"意味着多个句柄指向同一个对象，改变对象A将影响对象B。

###`背景知识`
#####1、Java的两大数据类型:
* 基本数据类型：
	<table>
    <tr>
        <th>基本数据类型</th>
        <th>  </th>
        <th>  </th>
        <th>  </th>
        <th>  </th>
    </tr>

    <tr>
        <td> 整数型 </td>
        <td> byte(1) </td>
        <td> short(2) </td>
        <td> int(4)  </td>
        <td> long(8) </td>
    </tr>
    
    <tr>
        <td>浮点型 </td>
        <td>float(4) </td>
        <td>double(8) </td>
        <td>    </td>
        <td>    </td>
    </tr>
    
    <tr>
        <td> 布尔型 </td>
        <td> boolean</td>
        <td> (1bit) </td>
         <td>    </td>
        <td>    </td>
    </tr>
    
    <tr>
        <td> 字符型 </td>
        <td> char(2)</td>
        <td>    </td>
        <td>    </td>
        <td>    </td>
    </tr>
</table>
	
* 引用数据类型：
 引用数据类型变量由类的构造函数创建，可以通过他们来访问引用的对象。

 java是静态语言，变量类型不可以被改变。引用类型的默认值都是null。
 
#####2、java数据类型在内存中的存储:
 - 基本数据类型的存储：
 
   基本类型不存在“引用”的概念，数据本身存储在内存中的stack中，变量直接访问内存数据；
 - 引用数据类型的存储：
 
   引用类型将对象存储在**heap**中，将“引用”存储在**stack**中。变量直接访问内存中的“引用”；
	
- 基本数据类型占据的空间是固定的，所以将他们存储在较小的内存区域 - 栈中，便于迅速查找变量的值；

- 引用数据类型的引用值大小会改变，放在栈中会降低变量查询的速度。因此，将对象存储在堆中的地址放在变量的栈空间中。由于地址的大小是固定的，所以对变量性能无负面影响;

###`产生方式：`
#####1、对象之间直接进行赋值：

```java
class Task{
 int number;	 
}
public class Assignment { 
 public static void main(String []args){
  
  Task test_1 = new Task();
  Task test_2 = new Task();
  
  test_1.number= 11;
  test_2.number= 22;
  
  System.out.println("test_1.number= " + test_1.number);
  System.out.println("test_2.number= " + test_2.number);   
  
  test_1 = test_2; //对象之间赋值
 
  System.out.println("test_1.number= " + test_1.number);
  System.out.println("test_2.number= " + test_2.number);
  
  test_1.number= 33;
  
  System.out.println("test_1.number= " + test_1.number);
  System.out.println("test_2.number= " + test_2.number);
 }
}
```
结果如下：

```java
test_1.number= 11
test_2.number= 22
test_1.number= 22
test_2.number= 22
test_1.number= 33
test_2.number= 33
```


#####2、方法调用时，将对象作为参数传递：

```java
 public class PassObject { 
  int i;  
  PassObject (int j) { i = j; } 
  static void f(PassObject o){
    o.i = 20;
  }
  public static void main(String[] args) {    
    PassObject A = new PassObject(10);
    System.out.println("Before f() ,A : " + A.i);
    f(A);
    System.out.println("After f() ,A : " + A.i);
  } 
} 
```
结果如下：

```java
Before f() ,A : 10
After f() ,A : 20
```

###`解决方式：`
别名问题的原因在于引用类型赋值时传递的是“引用”而不是数值，所以解决关键在于操作基本数据类型而避免引用类型。

例如:
```java
 test_1.number = test_2.number ; //对象之间赋值
```
