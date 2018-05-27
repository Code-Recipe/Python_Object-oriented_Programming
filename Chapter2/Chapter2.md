<notice>教程读者请不要直接阅读本文件，因为诸多功能在此无法正常使用，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/3)学习完整教程。如果您喜欢我们的教程，请在右上角给我们一个“Star”，谢谢您的支持！</notice>

类进阶
======

你已经成功入门面向对象编程啦👍 那么让我们继续往下看看吧~

位置参数
------
我们在调用函数时，经常会需要一些参数来完成指定的功能。
```python
def addition(a,b):
  print(a+b)
```
上面代码中的a,b就是我们所说的``位置参数``。位置参数在方法中运用很广，相当于一个input。

默认参数
------
接下来介绍的是**默认传入参数**这一个概念。

在上一章，我们介绍了``__init__``方法，可以在每次实例化一个新的对象时强制自动执行该方法，利用这个特点，我们可以规定一个类必须拥有的一些属性和一开始就执行的操作。
比如我们新建一个``Student``类，来储存学生的个人信息。
```python
class Student(object):
  def __init__(self, name, age):
    self.name = name
    self.age = age
```
在上面的方法中，如果我们想要实例化任何一个学生都必须传入学生的姓名和性别参数，否则会报错。比如
```python
a = Student("Allen", 16) #实例化一个Student对象，储存在a中
b = Student() #会报错
```

如果声明了__init__方法在实例化时却没有传入足够的参数，python编译器会报错：``TypeError: __init__() missing 2 required positional arguments: 'name' and 'age'``

但是有时候有的信息没收集全，这样的话就没有办法继续创建这个对象了。Python为我们提供了一个非常使用的功能：``Default Arguments``。默认参数可以让我们在创建方法时，给定参数一些初始值。
如果我们在创建新的物体时，有些参数没有给全，python会根据默认参数给这些参数赋值。

```python
class Student(object):
  def __init__(self, name= '', age=0):
    self.name = name
    self.age = age
```
我们在这个类的初始化方法中给name了一个空字符的默认值，age一个0的默认值。如果我们在实例化时没有给足需要的参数，程序不会报错。
```python
a = Student()
b = Student('Cindy')
```
**注意**：默认参数在定义时必须写在普通参数后面

但是假如我们遇到了一个对象，不知道其名字只知道其年龄，应该怎样声明这个对象呢？
```python
c = Student(,16)
```
上面代码的输出结果是``Syntax Error``,也就是说这样实例化是会报错的。

如何让python辨认出这个``16``实际上是``age``而不是``name``呢？我们可以用到关键字参数来帮助我们实现这个功能
```python
c = Student(age = 16)
```
这样的话，python就知道了这个16是传给age的。

可变参数
------
在python中，我们还可以定义**可变参数**。意为传入参数的个数是没有限制的，根据实际输入情况，python自己将这些传入的参数组成一个**元组(tuple)**。我们在变量名前加一个``*``来表示这是一个可变参数。
我们可以直接把任意个数字传入函数，在函数里，python会自行生成一个元组。元组相当于一个不能改变的列表，用圆括号括起来。
<lab lang="python" parameters="filename=average.py">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/3)查看。</notice>
def average(*score):
  for i in score:
    sum += i
  return sum
average(1,2,3,4,5,6,7,8,9)
tuple1=(1,2,3,4,5,6)
#average(*tuple1)
</lab>
但如果我们本来传进来的是一个元组或列表，我们可以在前面加一个*号把这个元组变为可变变量传入函数。

关键字参数
------
可变参数可以将输入的任意个参数转变为元组，而关键字参数则可以将输入的任意个参数转化为一个dict。在变量前加两个*号即表示它是关键字参数。
```python
def Student(name, age, **dic)
  print('name: ',name,' age: ',age,' others: ',dic)
```
如果我们以``Student('Allen',16)``来调用这个函数，结果会是``name: Allen age: 16 others:[]``,即在``others: ``后显示一个空词典。

小练习
-----
1. Consider the following code segment.

```java
public class Tester {
    public void someMethod(int a, int b){
     int temp = a;
     a = b;
     b = temp;
  }
}

public class TesterMain{
    public static void main(String[] args){
     int x = 6, y = 8;
     Tester tester = new Tester();
     tester.someMethod(x, y);
  }
}
```
Just before the end of execution of this program, what are the values of x, y, and
temp, respectively?


(A) 6, 8, 6


(B) 8, 6, 6


(C) 6, 8, ?, where ? means undefined


(D) 8, 6, ?, where ? means undefined


(E) 8, 6, 8

<cr type="hidden"><notice>隐藏内容功能在此无法正常显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/3)查看。</notice>C</cr>

   2.Consider the following code segment.

```java
public class Person
{
  private String myName; 
  private int myYearOfBirth;
  public Person(String name, int yearOfBirth)
  {
    myName = name;
    myYearOfBirth = yearOfBirth;
  }

  public String getName()
  { return myName; }

  public void setName(String name)
  { myName = name; }
//There may be instance variables, constructors, and methods that are not shown.
}
```

Assume that the following declaration has been made.

```java
Person student = new Person("Thomas", 1995);
```

Which of the following statements is the most appropriate for changing the name of student from "Thomas" to "Tom" ?

(A) student = new Person("Tom", 1995);

(B) student.myName = "Tom";

(C) student.getName("Tom");

(D) student.setName("Tom");

(E) Person.setName("Tom");

<cr type="hidden"><notice>隐藏内容功能在此无法正常显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/3)查看。</notice>D</cr>

3.Consider the following class declaration.

```java
public class Student
{
  private String myName; 
  private int myAge;

  public Student())
  { /* implementation not shown */ }

  public Student(String name, int age)
  { /* implementation not shown */ }

  // No other constructors
}
```

Which of the following declarations will compile without error?

I.Student a = new Student();

II.Student b = new Student("Juan", 15);

III.Student c = new Student("Juan", "15");

(A) I only

(B) II only

(C) I and II only

(D) I and III only

(E) I, II, and III

<cr type="hidden"><notice>隐藏内容功能在此无法正常显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/3)查看。</notice>C</cr>



### 实验室


<lab lang="java" parameters="filename=Hello.java">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/3)查看。</notice>
public class Hello {
   public static void main(String[] args) {
     // 在这里添加你的代码
   }
}
</lab>
