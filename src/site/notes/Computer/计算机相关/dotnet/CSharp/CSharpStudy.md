---
{"dg-publish":true,"permalink":"/Computer/计算机相关/dotnet/CSharp/CSharpStudy/","created":"2025-03-15T17:24:00","updated":"2025-04-09T23:20:10.251+08:00"}
---


---

# 微软官方文档

- ## [微软 C# 官方文档][微软 C# 官方文档]

- ## [历代 C# 语言特性，C# 发展历史——微软官方][历代 C# 语言特性，C# 发展历史——微软官方]
	- [从 C# 1.0 到 C# 9.0，历代 C# 语言特性一览](https://zhuanlan.zhihu.com/p/349915066)

- ## [编译器错误消息—微软官方文档](https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/compiler-messages/feature-version-errors)


---
# 基础知识

---

## 类型

### 值类型

- 和 C/C++ 不同，在 **C# 中数字不具有布尔意义。**

| 名称      | 含义              | 范围                                                           | .Net框架类型       | 默认值         |
| ------- | --------------- | ------------------------------------------------------------ | -------------- | ----------- |
| sbyte   | 8位有符号整数         | -128~127                                                     | System.Sbyte   | 0           |
| byte    | 8位无符号整数         | 0~255                                                        | System.byte    | 0           |
| short   | 16位有符号整数        | -32768~32767                                                 | System.Int16   | 0           |
| ushort  | 16位无符号整数        | 0~35535                                                      | System.UInt16  | 0           |
| int     | 32位有符号整数        | -2147 483 648~<br/><br/>2 147 483 647                          | System.Int32   | 0           |
| uint    | 32位无符号整数        | 0~4 294 967 295                                              | System.UInt32  | 0           |
| long    | 64位有符号整数        | -9 223 372 036 854 775 808~<br/><br/>9 223 372 036 854 775 807 | System.Int64   | 0           |
| ulong   | 64位无符号整数        | 0~18 446 744 073 709 551 615                                 | System.UInt64  | 0           |
| float   | 单精度浮点数          | 1.5*10 -45~<br/><br/>3.4*10 38                                 | System.Single  | 0.0f        |
| double  | 双精度浮点数          | 5*10 -324~<br/><br/>1.7*10 308                                 | System.Double  | 0.0d        |
| bool    | 布尔型             | true 或 false                                                 | System.Boolean | false       |
| char    | Unicode字符串      | U+0000~U+ffff                                                | System.Char    | '\0' 即 null |
| decimal | 小数类型的有效数字精度为28位 | +-1.0*10 28~<br/><br/>+-7.9*10 28                              | System.Decimal | 0m          |

---

## 方法

#未完成 

### ref引用

- ref 必须位于类型和名称前面
	- `int ref i = ref j; // 错误`
	- `ref int i = ref j;// 正确`
	- `int ref j;// 错误，必须要有初始值`

```cs
int i = 10; 
ref int j = ref i; //j = 20; //i 也会变为 20 
ChangeValue(ref i);// 必须加 ref ，不然报错 
void ChangeValue(ref int value) 
{ 
	value = 20; 
} 
Console.WriteLine(i);// 20
```

---

## 字符串

### 字符串内插（C#6.0-2015年7月）

```cs
int a = 16; 
string s = "Hello, World!";
string s2 = $"{s}, Goodbye, World!, {a}"; Console.WriteLine(s2); 
string s3 ＝ @"C:\users";// 引号前面加@（称作"逐字字符串"）将转义字符（\）当作普通字符对待
```

### 原始字符串（C#11-2022年11月发布）

- 以至少三个双引号字符序列 (""") 开头和结尾。俩三引号都要单独在一行
- 字符串内容位置以结尾引号左端为起点，不能比结尾引号靠左，可以靠右

```cs
string oStr = """ 
	Hello World 
		This is a multi-line string 
	""";
Console.WriteLine(oStr);
```

- json格式内插
	- 用两个$，两个{}
```cs
string str = "Ace"; 
int age = 16; 
string oStr = $""" 
{ 
	"name":"{{str}}", 
	"age":{{age}} 
} 
"""; 
Console.WriteLine(oStr);
```

### [字符串格式](https://www.cnblogs.com/diwu/articles/Csharp_tostring.html)

- `XXX.ToString("X2");`

---

## 结构体
#未完成 

---

## 枚举

#未完成 

---

## 数组
#未完成 

---

## 集合

### ArrayList
- 缺点：会进行装、拆箱；类型匹配混乱

```cs
using System.Collections; 

ArrayList arrayList = new ArrayList(); 
arrayList.Add(10); 
arrayList.Add("Hello"); 
arrayList.Add(true); 
arrayList.Insert(1, "World"); 
arrayList.Remove(10); 
arrayList.RemoveAt(1); 
arrayList.Clear(); 

foreach (var item in arrayList) 
{ 
	Console.WriteLine(item); 
}

```

### List`<>`
- 删除集合元素后，表面上集合变小了，实际上集合大小没变，只是能获取到的索引范围变小了

```cs
List<string> names = new List<string>() { "John", "Mary", "Peter" }; 
names.Add("Tom"); 
names.Add("Jane"); 
names.Insert(1, "Lily");
names.Remove("Mary"); 
names.AddRange(new string[]{"zhang", "wang", "li", "zhao"}); names.AddRange(names); 

foreach (var name in names) 
{
	Console.WriteLine(name); 
}
// List泛型集合可以转换为数组，同样数组可以转换成泛型集合 
string[] names2 = names.ToArray();
List<string> list = name2.ToList(); 

names.Clear(); 
Console.WriteLine(names.Count);
```

### [元组（C#7.0-2017 年 3 月）](https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/value-tuples)

- 元组最常见的用例之一是作为方法返回类型。 也就是说，你可以将方法结果分组为元组返回类型，而不是定义 out 方法参数，如以下示例所示：

```cs
int[] xs = new int[] { 4, 7, 9 }; 
var limits = FindMinMax(xs); 
Console.WriteLine($"Limits of [{string.Join(" ", xs)}] are {limits.min} and {limits.max}"); 
// Output: 
// Limits of [4 7 9] are 4 and 9 

int[] ys = new int[] { -9, 0, 67, 100 }; 
var (minimum, maximum) = FindMinMax(ys); Console.WriteLine($"Limits of [{string.Join(" ", ys)}] are {minimum} and {maximum}"); 
// Output:
// Limits of [-9 0 67 100] are -9 and 100 

(int min, int max) FindMinMax(int[] input) 
{ 
	if (input is null || input.Length == 0) 
	{ 
		throw new ArgumentException("Cannot find minimum and maximum of a null or empty array."); 
	} 
	
	// Initialize min to MaxValue so every value in the input 
	// is less than this initial value. 
	var min = int.MaxValue; 
	// Initialize max to MinValue so every value in the input 
	// is greater than this initial value. 
	var max = int.MinValue;
	 foreach (var i in input) 
	 { 
		 if (i < min) 
		 { 
			 min = i; 
		 } 
		 if (i > max) 
		 { 
			 max = i; 
		 } 
	 } 
	 return (min, max); 
}
```


---

## 字典

### 字典

```cs
using System.Collections.Generic; 

Dictionary<string, int> studentScores = new Dictionary<string, int>(); 

studentScores.Add("张三", 85); 
studentScores.Add("李四", 90); 
studentScores.Add("王五", 95);
studentScores["赵六"] = 75; 
studentScores.Remove("王五"); 
studentScores.Remove("aa");// 如果要删除的键值对在字典中不存在，也不会报错 

if (studentScores.ContainsKey("张三")) 
{
	Console.WriteLine(studentScores["张三"]);
} 

Dictionary<string, int> scores = new Dictionary<string, int>() 
{ 
	{"张三", 85}, 
	{"王五", 95}, 
	{"赵六", 75}, 
}; 
Dictionary<string, int> scores2 = new() { {"张三", 85}, {"王五", 95}, {"赵六", 75}, }; foreach (var item in studentScores) { Console.WriteLine($"{item.Key}: {item.Value}"); }
```

### 只读字典

```cs
Dictionary<string, float> dict = new Dictionary<string, float>(); 
dict.Add("张三", 85.5f); 
dict.Add("王五", 95.5f); 
dict.Add("赵六", 75.5f); 

var b = dict.AsReadOnly();

foreach (var item in b) 
{ 
	Console.WriteLine(item.Key + " " + item.Value); 
} 

var readOnlyDict = new ReadOnlyDictionary<string, float>(dict); 
//readOnlyDict["张三"] = 90.5f;// 报错，只读 

Console.WriteLine(readOnlyDict["张三"]);

foreach (var item in readOnlyDict) 
{ 
	Console.WriteLine(item.Key + " " + item.Value); 
}
```


---

## 面向对象

### 类

- 自动属性（C#3-2007-11-06）
	- `public string Name {get; set;}`
- 类实例化时，更简单的初始化（C#3-2007-11-06）

```cs
Student stu1 = new Student { Name = "John", Age = 16 }; Student stu2 = new() { Name = "Mary", Age = 17 }; Console.WriteLine(stu1.Name + stu1.Age); Console.WriteLine(stu2.Name + stu2.Age); 

class Student 
{ 
	public string Name { get; set; } 
	public int Age { get; set; } 
}
```

### 类继承

- [继承的本质(刘铁猛)](https://www.bilibili.com/video/BV13b411b7Ht/?p=25&share_source=copy_web&vd_source=407f92cf6751e29e9d623fde5b09db24&t=1120)：继承的本质是派生类在基类已有的成员的基础之上对基类进行横向或者纵向上的扩展
	- 横向：类成员在数量上的扩充
	- 纵向：对某个类成员进行版本的更新（重写）

- 类前加 sealed ，则该类不能被继承
- 基类的私有成员也会被继承，只是派生类不能直接访问
- 子类的访问级别，**不能超过**父类的访问级别
	- 如父类是 internal，子类就不能是public

- 当创建子类时，**先构建父类**的构造方法，再一级级往下构建子类的，最终构建要创建的子类对象
- 若写了有参构造，则编译器不再默认提供无参构造
	- **构造函数和析构函数不被继承**

```cs
class Vehicle 
{ 
	public Vehicle(string vOwner) 
	{ 
		this.Owner = vOwner;
	} 
	
	public string Owner { get; set; } 
	
} 

class Car : Vehicle 
{ 
	// 因为父类只有有参构造，所以子类要 
	public Car(string cOwner) : base(cOwner)//先赋值给 Car 的cOwner ，后 base 的 
	{ 
		//this.Owner = cOwner 
	} 
	// 或者 
	public Car() : base("N/A") 
	{ 
		this.Owner = "Car Owner"; 
	} 
	public void ShowOwner()
	{
		Console.WriteLine(Owner); 
	} 
}
```

#### [类修饰符](https://learn.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/access-modifiers#summary-table)

- **公共 public** ：任何程序集（VS创建新项目时的项目）中的代码都可以访问此类型或成员。 包含类型的可访问性级别控制该类型的公共成员的可访问性级别。

- **专用 private**：只有在**同一 class** 或 struct 中声明的代码才能访问此成员。

- **受保护 protected**：只有同一 class 或派生的 class 中的代码才能访问此类型或成员。**继承链（类体内，声明的对象不能访问）**

- **内部 internal**：只有**同一程序集**中的代码才能访问此类型或成员。

- **受保护的内部 protected internal**：只有同一程序集中的代码或另一个程序集的派生类中的代码才能访问此类型或成员。**同一程序集或继承链**
 
- **专用受保护 private protected**：只有同一程序集和同一类/派生类中的代码才能访问该类型或成员。**同一程序集且继承链**

- **文件 file**：只有同一文件中的代码可以访问类型或成员。

- 类的修饰符默认为 internal
- 类成员的修饰符默认为 private

- 访问级别不对，自己的对象都不能访问

```cs
class Vehicle 
{ 
	public string Owner { get; set; } 
	
	protected void ShowOwner() 
	{ 
		Console.WriteLine(Owner); 
	} 
} 
public static void Main()
{ 
	Vehicle vehicle = new Vehicle("John");
	vehicle.ShowOwner();// 不行，报错：不可访问， 
	//因为它具有一定的保护级别 
}
```

#### 密封类

- 用 sealed 修饰
- 只能继承别的类，不能被别的类继承

```cs
public sealed Class Student:Person {}
```

### 重写

- 父类变量可以引用子类对象，重写可以让父类调用子类的方法——多态

- 下面这种写法只是子类对父类方法的隐藏

```cs
class Vehicle 
{ 
	public void Run() 
	{
		Console.WriteLine("Vehicle is running"); 
	} 
} 
class Car : Vehicle 
{ 
	public void Run() 
	{
		Console.WriteLine("Car is running"); 
	} 
}
```

- 只有父类加 virtual ，子类加 override 才是重写

```cs
class Vehicle 
{ 
	public virtual void Run() 
	{ 
		Console.WriteLine("Vehicle is running"); 
	} 
} 
class Car : Vehicle 
{ 
	public override void Run() 
	{ 
		Console.WriteLine("Car is running"); 
	} 
}
```

- 若按第一种隐藏的写法，下面代码执行结果为：`Vehicle is running`
- 重写的话，结果为：`Car is running`

```cs
Vehicle vehicle = new Car();
vehicle.Run();
```

### 抽象类

- 抽象类为做基类而生，我们应该封装那些不变的、稳定的、固定的和确定的成员，而把那些不确定的、有可能改变的成员声明为抽象成员，并且留给子类去实现——[# 刘铁猛《C#语言入门详解》第27集，18：30]( https://www.bilibili.com/video/BV13b411b7Ht/?p=27&share_source=copy_web&vd_source=407f92cf6751e29e9d623fde5b09db24&t=1104)
- 抽象类不一定有抽象方法，但有抽象方法的类一定是抽象类
- 抽象方法不能是 private 的
- 抽象类不能被实例化


---

## 接口

- 接口是一种约束，[只要是继承自这个接口的类，强制实现接口中的方法](https://www.bilibili.com/video/BV1hx4y1G7C6/?p=40&share_source=copy_web&vd_source=407f92cf6751e29e9d623fde5b09db24&t=339)
	- 所以多态中，用接口类型变量引用继承该接口的类实例对象，必然可以调用接口所含有的方法

- **接口只能有方法、属性、索引器、事件，不能有字段和构造函数**
- 接口不能被实例化，接口与接口之间可以继承，并且可以多继承
- 接口不能继承一个类，而类可以继承接口（接口只能继承接口，而类既可以继承接口，又可以继承类）
- 一个类可以同时继承一个类并实现多个接口，如果一个子类同时继承了父类A，并实现了接口IA，那么语法上A必须写在IA的前面
- C#12中，接口成员可以添加 public internal修饰符了
- C#8.0接口中的方法可以有方法体（默认实现）了

### 显式实现接口

- C# 独有的功能
- 显式实现的接口成员，只能通过指向该接口的引用来访问

```cs
class MyClass:IIfc1
{
	void IIfc1.PrintOut(string s)
	{
		Console.WriteLine("IIfc1");
	}
	public void Method1()
	{
		PrintOut("...");// 编译错误
		this.PrintOut("...");// 编译错误
		// 转换为接口引用
		((IIfc1)this).PrintOut("...");// 成功调用
		
	}
}
```


### 接口隔离原则

-  一个接口应该拥有尽可能少的行为，使其精简单一。对于不同的功能的模块分别使用不同接口，而不是使用同一个通用的接口。

例：
- 把大接口变成小接口的组合，然后参数类型用需要的小接口
	- 只关注我想要的功能，多余的功能不需要，也调用不了
	- 只需要机动车能跑，不需要开火，所以用IVehicle接口
		-  而把ITank从原来的大接口分成IVehicle和IWeapon，因为用IVehicle类型变量接收实例，所以只能够调用IVehicle里的Run方法，而调用不了IWeapon中的Fire
		- 这样就把我不需要的功能隐藏了起来，我看不见，也调用不了


- 我想到了Godot的组合模式

```cs
Driver driver = new Driver(new Car());
driver.Run();
driver = new Driver(new Truck());
driver.Run();
driver = new Driver(new Tank());
driver.Run();

class Driver
{
    private IVehicle _vehicle;

    public Driver(IVehicle vehicle)
    {
        this._vehicle = vehicle;
    }

    public void Run()
    {
        _vehicle.Run();
    }
}

interface IVehicle
{
    void Run();
}
interface IWeapon
{
    void Fire();
}
// 把大接口变成用小接口组合
interface ITank : IVehicle, IWeapon
{

}

class Car : IVehicle
{
    public void Run()
    {
        Console.WriteLine("car is running...");
    }
}
class Truck : IVehicle
{
    public void Run()
    {
        Console.WriteLine("truck is running...");
    }
}
class Tank : ITank
{
    public void Fire()
    {
        Console.WriteLine("tank is firing...");
    }

    public void Run()
    {
        Console.WriteLine("tank is running...");
    }
}
```

#### 把接口隔离的方法隐藏起来

- 如果接口里方法不想轻易让人调用，就显式实现它
- 显式实现接口方法后，只有显式的使用接口类型的变量，去引用实现了这个接口的具体类的实例时，这个接口里的方法才可以被看见

```cs
// 显式实现接口，接口隔离

WarmKiller warmKiller = new WarmKiller();
// 只能看见Love方法，看不见Kill方法

warmKiller.Love();
IKiller killer = warmKiller as IKiller;// 同一个实例的身份转换
// 可以看见Kill方法了，不过看不见Love方法了
killer?.Kill();

interface IGentleman
{
    void Love();
}
interface IKiller
{
    void Kill();
}
class WarmKiller : IGentleman, IKiller
{
    public void Love()
    {
        Console.WriteLine("I will love you forever...");
    }

    void IKiller.Kill()
    {
        Console.WriteLine("我是个杀手，我莫得感情...");
    }
}
```


---

## 用什么方式实现多态

> [!question] **什么时候用虚方法来实现多态？**

- 几个子类中可以抽象提取出一个公共的父类，并且父类必须写上几个子类共有的方法，但是又不知道父类方法具体怎么写，而且需要父类实例化对象

> [!question] **什么时候用抽象类来实现多态？**

- 和上面一样，但是不需要父类实例化

> [!question] **什么时候用接口来实现多态？**

 - 几个子类根本就抽象不出父类，但是他们都有一个共同的行为、能力

---

## 委托

- 委托是一种类，类是数据类型，所以委托也是一种数据类型。
	- 委托是类，所以写在命名空间中
- 可以把委托看成是一个类型安全的、面向对象的C\C++ 函数指针

- 一切皆地址
	- 变量（数据）以某个地址为起点的一段内存中所存储的值
	- 函数（算法）是以某个地址为起点的一段内存中所存储的一组机器语言指令
- 直接调用与间接调用
	- 直接调用：通过函数名来调用函数，CPU通过函数名直接获得函数所在地址并开始执行→返回
	- 间接调用：通过函数指针来调用函数，CPU通过读取函数指针存储的值获得函数所在地址并开始执行→返回
		- **为什么要多此一举间接调用？**
			- 函数指针可以做成员，可以做本地变量
			- 因为可以做成员，有了链表等数据结构
			- 因为函数指针可以做函数形参，你传进来啥函数，就调用啥，增加复用

- 委托的作用
	- 函数传参
	- 回调函数
- 委托的简单使用
	- Action委托
		- 无返回值
	- Func委托
		- 有返回值
 
### 声明委托类型

- 以 delegate 关键字开头
- 没有方法主体

```cs
delegate void MyDel(int x﻿);
```

### 创建委托对象

- 委托是引用类型，因此有引用和对象
- 委托类型的变量声明
	- `MyDel delVar;`

>  **创建委托对象**

> [!warning] 注意
> 若使用 new 运算符创建，**圆括号里必须写一个方法**，不能不写也不能写两个及以上


```cs
delegate void MyDelegate(string message); 

// 方法一：使用带 new 运算符的对象创建表达式 
MyDelegate delVar = new MyDelegate(myInstObj.Mym1);// 创建委托并保存引用 

// 方法二：使用快捷语法
MyDelegate delVar = myInstObj.Mym1;// 创建委托并保存引用
```

- 给委托变量重新赋值，会创建一个新的委托对象并赋值给它，旧的委托对象会被垃圾回收器回收。

### 委托的一般使用

- 实例：把方法当作参数传给另一个方法
	- 正确使用1：**模板方法**，借用指定的外部方法来产生结果
		- 相当于“填空题”
		- 常位于代码中部
		- 委托有返回值
	- 正确使用2：**回调（callback）方法**，调用指定的外部方法
		- 相当于"流水线”
		- 常位于代码末尾
		- 委托无返回值

- 注意：难精通+易使用+功能强大东西，一旦被滥用则后果非常严重
	- 缺点1：这是一种方法级别的紧耦合，现实工作中要慎之又慎
	- 缺点2：使可读性下降、debug的难度增加
	- 缺点3：把委托回调、异步调用和多线程纠缠在一起，会让代码变得难以阅读和维护
	- 缺点4：[委托使用不当有可能造成内存泄漏和程序性能下降](https://www.bilibili.com/video/BV13b411b7Ht/?p=19&share_source=copy_web&vd_source=407f92cf6751e29e9d623fde5b09db24&t=3226)
		- 内存泄漏：程序在申请内存后，无法释放已申请的内存空间
		- 如果委托引用的方法是一个对象的实例方法，拿委托引用了这个方法，即使没有别的引用类型变量来引用此对象了，这个对象也不得不存在于内存中，无法被释放。

> [!warning] 注意
> 应该适时地使用接口取代一些对委托的使用
> - Java完全地使用接口取代了委托的功能，即Java没有与C#中委托相对应的功能实体
### 多播委托

#### 增加方法

- 在使用+=运算符时，实际发生的是创建了一个新的委托，其调用列表是左边的委托加上右边方法的组合，然后将这个新的委托赋值给变量

```cs
Mydel delVar = M1;// 创建委托并初始化 
delVar += M2;//增加方法 
delVar += M3;//增加方法 

/*由于委托是不可变的，所以为委托的调用列表添加三个方法后的结果 其实是变量指向一个全新的委托*/
```

#### 移除方法

- 与委托增加方法一样，其实是创建了一个新的委托。新的委托是旧委托的副本——只是没有了已经被移除方法的引用。
- 如果在调用列表中的方法有多个实例，-=运算符将从列表最后开始搜索，并且移除第一个与方法匹配的实例。
- 试图移除委托中不存在的方法没有效果。
- 试图调用空委托会抛出异常。我们可以通过委托和Null进行比较来判断委托的调用列表是否为空。如果调用列表为空，则委托是null。

```cs
delVar -= SCL.m3// 从委托移除方法
```

### 调用委托

- 可以像调用方法一样简单地调用委托。用于调用委托的参数将会用于调用调用列表中的每一个方法。
	- 也可以 myDelegate.Invoke("你好，世界！");

- 如果一个方法在调用列表中出现了多次，当委托被调用时，每次在列表中遇到这个方法时它都会被调用一次。
- 在调用委托时，它使用相同的参数来调用调用列表中的每一个方法
- 如果调用委托时委托为空，则会报错

```cs
Unhandled exception. System.NullReferenceException: Object reference not set to an instance of an object. at Program.<Main>$(String[] args) in E:\Computer\VS\Console\ConsoleApp1\ConsoleApp1\Program.cs:line 273
```

> [!tip] **为避免调用空委托，可以使用空条件运算符**

- `myDelegate?.Invoke("你好，世界！");`
- `myDelegate?.("你好，世界！");`

```cs
MyDel delVar = inst.Mym1; 
delVar += scl.m3; 
delVar += x.act; 

if(null != delVar)// 确认委托有方法 
{ 
	delVar(53); // 调用委托 
} 
else 
{ 
	Console.WriteLine("委托是空的") 
} 
/* 
在调用委托时，它使用相同的参数来调用调用列表中的每一个方法 inst.mym1(53); scl.m3(53); x.act(53); 
*/
```

#### 调用带返回值的委托

- 如果委托有返回值并且在调用列表中有一个以上的方法
	- 调用列表中最后一个方法返回的值就是委托调用返回的值
	- 调用列表中所有其他方法的返回值都会被忽略

#### 调用带引用参数的委托

- 如果委托有引用参数，参数值会根据调用列表中的一个或多个方法的返回值而改变

### 匿名方法（C#2.0 2005-11-07）

#### 语法

- delegate 类型关键字
- 参数列表，如果语句块没有使用任何参数则可以省略
- 语句块，它包含了匿名方法的代码

```cs
delegate(参数列表){语句块}
```

```cs
// 使用具名方法 
class Program 
{ 
	public static int Add20(int x) 
	{ 
		return x + 20 ; 
	} 
	delegate int OtherDel(int a); 
	static void Main() 
	{ 
		OtherDel del = Add20;
		Console.WriteLine("{0}", del(5)); 
	} 
} 

// 使用匿名方法 
class Program 
{ 
	delegate int OtherDel(int a); 
	static void Main() 
	{ 
		OtherDel del = delegate(int x) 
		{ 
			return x + 20;
		}; 
		Console.WriteLine("{0}", del(5)); 
	} 
}
```

#### 返回类型

- 匿名方法不会显式声明返回值。
- 如果委托有返回类型，则在匿名方法的语句块内返回值。
- 如果委托是void 类型，则匿名方法就不能返回值。
- 例如下面代码，委托返回类型是 int ，匿名方法的实现代码因此也必须返回 int 值

```cs
delegate int Del(int param); 

static void Main() 
{ 
	Del del = delegate(int x) 
	{ 
		return x + 20; // 返回一个整型值 
	}; 
}
```

#### params 参数

- 如果委托声明的参数列表包含了 params 参数，那么匿名方法的参数将忽略 params 关键字。例如在如下代码中：
	- 委托类型声明指定最后一具参数为 params 类型的参数
	- 然而，匿名方法参数列表忽略了 params 关键字

```cs
// 在委托类型声明中使用 params 关键字 
delegate void Somedel(ibt x, params int[] y); 
// 在匹配的匿名方法中省略关键字 
Somedel mDel = delegate(int x, int[] y) 
{ 
	... 
};

```


#### Lambda 表达式（C#3.0 2007-11-06）

- 删除 delegate 关键字
- 在参数列表和匿名方法主体之间放 Lambda 运算符 =>。Lambda 运算符读作“goes to“
- 编译器可以从委托的声明中知道委托参数的类型，因此 Lambda 表达式允许我们省略类型参数

```cs
delegate double Mydel(int par); 

Mydel del = delegate(int x){return x + 1;}; // 匿名方法 
Mydel lam1 =        (int x) => {return x + 1;}; // Lambda 表达式 
Mydel lam2 =            (x) => {return x + 1;}; // Lambda 表达式 
Mydel lam1 =             x => {return x + 1;}; // Lambda 表达式 
Mydel lam1 =             x => x + 1; // Lambda 表达式
```

- Lambda 表达式参数列表中参数必须在参数数量、类型和位置上与委托相匹配
- 如果没有参数，必须使用一组空的圆括号


---

## 事件

### 简介

1.  **事件的误传： [认为事件是一种特殊的委托类型字段]( https://www.bilibili.com/video/BV13b411b7Ht/?p=20&share_source=copy_web&vd_source=407f92cf6751e29e9d623fde5b09db24&t=52)**
	 - 类中有字段了，但还是有属性这个东西，事件和委托差不多也是这个关系[^1]

2. **事件最大的特点就是能够发生**。如果一个作为主语的名词，可以使用“发生”这个词来做它的谓语动词的话，那么它就是一个事件。例如：
	- 苹果，我们不能说一个苹果发生了
	- 公司上市、产品发布，它们是可以发生的， 所以这俩是事件
	
3. **事件是一种类型的成员**
	- 凡是事件，都是隶属于某一个主体的，没有公司，就不会有“上市”这个事件发生；没有产品，就不会有”发布“这个事件发生
4. **事件的功能**
	- 事件是使对象或类具备**通知能力**的成员
	- 事件的功能 = 通知 + 可选的事件参数（即详细信息）

5. **事件的使用**
	- 用于对象或类间的动作协调与信息传递（消息推送）

6. **事件原理**：事件模型中的两个“5”
	- "发生→响应"中的5个部分——闹钟响了你起床、孩子饿了你做饭....这里隐含着"订阅"关系
	- "发生→响应"中的5个动作——
		- （1）我有一个事件→
		- （2）一个人或者一群人关心我的这个事件→
		- （3）我的这个事件发生了→
		- （4）关心这个事件的人会被依次通知到→
		- （5）被通知到的人根据拿到的事件信息（又称"事件数据"、"事件参数"、"通知"）采取行动，称为对事件进行响应（又称"处理事件"）。

7. **约定的术语**
	- 这四个是一个意思 
		- **事件的订阅者**
		- 事件消息的接收者
		- 事件的响应者
		- 被事件所通知的对象
	- 事件的处理者
	- 这四个是一个意思 
		- 事件信息
		- 事件消息
		- 事件数据
		- **事件参数**

> [!tip]- 提示
> - 事件多用于桌面、手机等开发的客户端编程，因为这些程序经常是用户通过事件来"驱动"的
> - 各种编程语言对这个机制的实现方法不尽相同
> - Java语言里没有事件这种成员，也没有委托这种数据类型。Java的"事件"是使用接口来实现的
> - MVC、MVP、MVVM等模式，是事件模式更高级、更有效的"玩法"
> - 日常开发的时候，使用已有事件的机会比较多，自己声明事件的机会比较少，所以先学使用

### 事件的应用

- 事件模型的五个组成部分
	1. 事件的拥有者（event source，对象）
	2. 事件成员（event，成员）
	3. 事件的响应者（event subscriber，对象）
	4. 事件处理器（event handler，方法成员）——本质上是一个回调方法
	5. 事件订阅——把事件处理器与事件关联在一起，本质上是一种以委托类型为基础的"约定"
- 触发事件，是事件的拥有者的一些内部逻辑触发的事件

```cs
// 事件的拥有者
class Program
{
	static void Main(string[] args)
	{
		System.Timers.Timer timer = new System.Timers.Timer();
		timer.Interval = 1000;
		Boy boy = new Boy();
		timer.Elapsed += boy.Action;
		Girl girl = new girl();
		timer.Elapsed += girl.Action;
		timer.Start();
		Console.ReadKey();
	}
}

// 事件的响应者
class Boy
{
	// 事件处理器
    internal void Action(object? sender, ElapsedEventArgs e)
    {
        Console.WriteLine("Jump!");
    }
}
class Girl
{
	// 事件处理器
    internal void Action(object? sender, ElapsedEventArgs e)
    {
        Console.WriteLine("Sing!");
    }
}
```

- ⭐
	- **事件的拥有者和事件的响应者是两个不同的对象**
```mermaid
---

config:

  look: neo

  theme: default

---

flowchart RL

 subgraph s1["事件的拥有者"]

        n1["事件"]

  end

 subgraph s2["事件的响应者"]

        n2["事件处理器"]

  end

    n2 -- 订阅 --> n1
```

```cs title:⭐
class Program
{
	static void Main(string[] args)
	{
		// 事件的拥有者为 Form
		Form form = new Form();
		Controller controller = new Controller(form);
		form.ShowDialog();
	}
}
// 事件的响应者为 Controller
class Controller
{
	private Form _form;
	public Controller(Form form)
	{
		if(form != null)
		{
			_form = form;
			// 订阅
			_form.Click += this.FormClicked;
		}
	}
	// 事件处理器
	private void FormClicked(object sender, EventArgs e)
	{
		_form.text = DataTime.New.ToString();
	}
}
```

- ⭐⭐
	- **事件的拥有者同时也是事件的响应者**

```mermaid
---

config:

  look: neo

  theme: default

---

flowchart

 subgraph s2["事件的拥有者同时也是事件的响应者"]

        n2["事件处理器"]

        n3["事件"]

  end

    n2 -- 订阅 --> n3
```

```cs title:⭐⭐
class Program
{
	static void Main(string[] args)
	{
		// 事件的拥有者为 MyForm
		MyForm myForm = new MyForm();
		myForm.Click += myForm.FormClicked;
		myForm.ShowDialog();
	}
}
class MyForm:Form
{
	// 事件的响应者还是事件拥有者它自己
	// 事件处理器
	void FormClicked(object sender, EventArgs e)
	{
		this.Text = DataTime.Now.ToString();
	}
}

```


- ⭐⭐⭐
	- **事件的拥有者是事件的响应者的一个字段成员。**
	- 例子：
		- 窗口对象有关闭按钮，按钮是窗口的成员，按钮有关闭事件，窗口的关闭方法订阅了按钮的事件
```mermaid
flowchart TB

 subgraph s2["事件的拥有者"]

        n2["事件"]

  end

 subgraph s1["事件的响应者"]

        n1["事件处理器"]

        s2

  end

    n1 -- 订阅 --> n2
```

```cs title:⭐⭐⭐
class Program
{
	static void Main(string[] args)
	{
		// 事件的响应者为 MyForm
		MyForm myForm = new MyForm();
		myForm.ShowDialog();
	}
}
// 窗口有按钮和文本框成员，按钮是事件拥有者，窗口是事件响应者
class MyForm:Form
{
	private TextBox textBox;
	// 事件的拥有者为 Button
	private Button button;
	
	public MyForm()
	{
		this.textBox = new TextBox();
		this.button = new Button();
		this.Controls.Add(this.texbox);
		this.Controls.Add(this.button);
		this.button.Click += this.ButtonCLicked;
		this.button.Text = "SayHello";
		this.button.Top = 100;// 按钮的上边界距窗口距离
	}
	// 事件处理器
	private void ButtonClicked(object sender, EventArgs e)
	{
		this.textBox.Text = "Hello World";
	}
}
```

> **一个事件可以同时挂接多个事件处理器**
> 	Boy、Girl 的例子
> 	
> **一个事件处理器可以被多个事件挂接**
> 	

#未完成 
### 事件的自定义声明

- 事件是基于委托的，有两层意思：
	1. 第一层：**事件需要委托类型来做一个约束**。这个约束既规定了事件能够发送什么样的消息给事件的响应者，也规定了事件的响应者能收到什么样的事件消息，这就决定了事件响应者的事件处理器必须能够跟这个约束匹配上，它们才能订阅这个事件。
	2. 第二层：当事件的响应者，向事件的拥有者提供了能够匹配这个事件的事件处理器之后，需要把这个事件处理器保存或者记录下来，能够记录或者说引用方法的任务，也只有委托类型的实例能做到。

- 事件只能出现在 += 和 -= 的左边，不能出现在其他任何操作符的左边
- 就像属性是普通字段的包装器一样，事件是委托的包装器，是对委托的一种约束限制：限制外界对这个委托字段的访问，只能为它添加或移除事件处理器，**只能在事件拥有者的内部去触发事件**。


- 两个声明可以看下面的例子
#### 完整声明

```cs
delegate void CallWaiterEventHandler(Customer customer);

class Customer
{
	// 声明委托类型字段，用来存储引用事件处理器
	private CallWaiterEventHandler _callWaiter;
	// 顾客叫服务员事件
	public event CallWaiterEventHandler CallWaiterEvent
	{
	    add
	    {
	        _callWaiter += value;
	    }
	    remove
	    {
	        _callWaiter -= value;
	    }
	}
}
```

#### 简略声明

```cs
// 顾客点餐事件
public event EventHandler<OrderEventArgs> Order;
```


#### 例子

- 有这样一流程：

```mermaid
graph LR
	顾客进饭馆-->喊服务员点餐-->服务员展示菜单-->顾客点餐-->服务员上菜-->顾客结账-->服务员展示账单-->顾客付款
```

- 首先抽象出两个角色类，顾客类和服务员类
- 然后是事件：（五个部分，**事件**，==事件拥有者==，==订阅者==，==事件处理器==，==订阅==）
	1. **喊服务员事件**：因为是顾客喊服务员，所以==事件拥有者==是顾客，==订阅者==是服务员，==事件处理器==是服务员展示菜单方法，服务员==订阅==顾客
	2. **点餐事件**：顾客点餐，==事件拥有者==为顾客，==订阅者==为服务员，==事件处理器==是服务员上菜，服务员==订阅==顾客
	3. **结账事件**：顾客结账，==事件拥有者==为顾客，==订阅者==为服务员，==事件处理器==是服务员展示账单，服务员==订阅==顾客
- 这个例子是一星模型，**事件的拥有者和事件的响应者是两个不同的对象**
- [[Computer/计算机相关/dotnet/CSharp/未命名/事件例子\|事件例子]]


### 事件与委托的关系

> **有了委托字段/属性，为什么还需要事件？**

- 为了程序的逻辑更加"有道理”、更加安全，==谨防像上面例子里李四那样"借刀杀人"==

> **事件真的是"以特殊方式声明的委托字段/实例"吗？**

- ==不是！==只是声明的时候"看起来像”（对比委托字段与事件的简化声明，field-like）
- 事件声明的时候使用了委托类型，简化声明造成事件看上去像一个委托的字段（实例），而event关键字则更像是一个修饰符——这就是==错觉的来源之一==
- 订阅事件的时候+=操作符后面可以是一个委托实例，这与委托实例的赋值方法语法相同，这也让事件看起来像是一个委托字段一一这是==错觉的又一来源==
- **重申**：事件的本质是加装在委托字段上的一个"蒙板"（mask），是个起掩蔽作用的包装器。这个用于阻挡非法操作的"蒙板"绝不是委托字段本身

>  **为什么要使用委托类型来声明事件？**

- 站在source的角度来看，是为了表明source能对外传递哪些消息
- 站在subscriber的角度来看，它是一种约定，是为了约束能够使用什么样签名的方法来处理（响应）事件
- 委托类型的实例将用于存储（引用）事件处理器
- 事件基于委托，实际上是由事件处理器决定的，处理器需要啥，事件就需要传递啥（决定了参数列表），同时处理器是一个方法，能存储方法及其参数类型的只有委托[^2]。

- **对比事件与属性**
	- 属性不是字段——很多时候属性是字段的包装器，这个包装器用来保护字段不被滥用
	- 事件不是委托字段一一它是委托字段的包装器，这个包装器用来保护委托字段不被滥用
	- 包装器永远都不可能是被包装的东西

- 所以==事件的本质==是委托字段的一个包装器
	- 这个包装器对委托字段的访问起==限制作用==，相当于一个"蒙板"
	- 封装（encapsulation）的一个重要功能就是隐藏
	- 事件==对外界==隐藏了委托实例的大部分功能，==仅暴露添加/移除事件处理器的功能==
	- 添加/移除事件处理器的时候可以直接使用方法名，这是委托实例所不具备的功能

> [!question]- 疑问
> 委托实例不是也可以直接用方法名来添加和移除方法吗？
> 
> 不对，那好像是简化的快捷语法



### 命名约定

#### 用于声明事件的委托类型的命名约定

- 用于声明Foo事件的委托，一般命名为FooEventHandler（除非是一个非常通用的事件约束）
	- Foo 就是 XXX
- FooEventHandler委托的参数一般有两个（由Win32 APl演化而来，历史悠久）
	- 第一个是object类型，名字为sender，实际上就是事件的拥有者、事件的source。
	- 第二个是EventArgs类的派生类，类名一般为FooEventArgs，参数名为e。也就是前面讲过的事件参数
	- 虽然没有官方的说法，但我们可以把委托的参数列表看做是事件发生后发送给事件响应者的“事件消息”
- 触发Foo事件的方法一般命名为OnFoo，即"因何引发"、“事出有因"
	- 访问级别为protected，不能为public，不然又成了可以"借刀杀人"了
	- **触发事件这个工作必须由事件拥有者自己来做**

#### 事件的命名约定

- 带有时态的动词或者动词短语
- 事件拥有者"正在做”什么事情，用进行时；事件拥有者"做完了"什么事情，用完成时



---

## 转换

### 显式转换

- `Convert.ToInt32()`
	- [四舍六入五成双]( https://baike.baidu.com/item/%E5%9B%9B%E8%88%8D%E5%85%AD%E5%85%A5%E4%BA%94%E6%88%90%E5%8F%8C/9062547)
{ #4Round6Carry}

		- （1）被修约的数字小于5时，该数字舍去；
		- （2）被修约的数字大于5时，则进位；
		- （3）被修约的数字等于5时，要看5前面的数字，若是奇数则进位，若是偶数则将5舍掉，即修约后末尾数字都成为偶数；若5的后面还有不为“0”的任何数，则此时无论5的前面是奇数还是偶数，均应进位。

### 装箱、拆箱

- 装箱：将值类型转换为引用类型
- 拆箱：将引用类型转换为值类型
- 看两种类型是否发生了装箱或者拆箱，要看，这两种类型是否存在继承关系。
	- 有继承关系可能发生装箱，无继承关系一定不会发生装箱
	- 如：`string str = "123"; int i = (int)str;` 没有发生拆箱，因为 int 和 string 没有继承关系
- 装、拆箱会影响性能

---
## IO文件

### Path类-路径操作

- 静态类，不能创建对象

```cs
string str = @"C:\3000soft\RedSPider\Data\Message\老赵.wav"; // 获得文件名 
Console.WriteLine(Path.GetFileName(str));// 老赵.wav
// 获得文件名但是不包含扩展名 
Console.WriteLine(Path.GetFileNameWithoutExtension(str));// 老赵
// 获得文件的扩展名 
Console.WriteLine(Path.GetExtension(str));// .wav 
// 获得文件所在的文件夹的名称 
Console.WriteLine(Path.GetDirectoryName(str));// C:\3000soft\RedSPider\Data\Message 
// 获得文件所在的全路径 
Console.WriteLine(Path.GetFullPath(str));// C:\3000soft\RedSPider\Data\Message\老赵.wav 
// 连接路径
Console.WriteLine(Path.Combine(@"c:\a\", "b.txt"));// c:\a\b. txt
```

### File类-文件操作

- 静态类，不能创建对象
- 适用于操作小文件

```cs
// 创建文件 
// 再次运行创建，只会修改第一次创建的把它的内容清空，可以看下文件属性的创建时间、修改时间 
string str = @"C:\Users\Zhang\Desktop\test"; File.Create(str+@"\test.txt");
// 删除文件，不放入回收站直接删除 
File.Delete(str + @"\test.txt"); 
// 复制文件 
File.Copy(str + @"\test.txt", str + @"\test2.txt");
```

#### 读取文件

- 方法二、三只能读取文本文件，方法一可以读取多媒体文件

```cs
// 方法一：ReadAllBytes 
string str = @"C:\Users\Zhang\Desktop\钱塘湖春行.txt"; byte[] bytes = File.ReadAllBytes(str); 
string content = Encoding.UTF8.GetString(bytes); Console.WriteLine(content); 

// 方法二：ReadAllLines 
string strAddress = @"C:\Users\Zhang\Desktop\钱塘湖春行.txt"; 
// ReadAllLines方法会返回指定路径文件的所有行内容，并以字符串数组的形式返回。 
string[] contents = File.ReadAllLines(strAddress); foreach (string content in contents) 
{ 
	Console.WriteLine(content); 
} 

// 方法三：ReadAllText 
string contents = File.ReadAllText(strAddress); Console.WriteLine(contents);

```

#### 写入文件

```cs
// 方法一：WriteAllBytes 
string strAddress = @"C:\Users\Zhang\Desktop\阿大.txt"; 
string str = "今天天气好晴朗，处处好风光。";
string str2 = "你好，世界！"; 
// 将字符串转换成字节数组 
byte[] bytes = Encoding.UTF8.GetBytes(str2); 
// 将字节数组写入文件，如果没有这个文件，则创建这个文件，有的话则覆盖原文件 
File.WriteAllBytes(strAddress, bytes); 

// 方法二：WriteAllLines 
string strAddress = @"C:\Users\Zhang\Desktop\阿大.txt"; 
string[] str = { "今天天气好晴朗，处处好风光。", "你好，世界！" , "张三李四王五赵六。"}; 
File.WriteAllLines(strAddress, str); 

// 方法三：WriteAllText 
string str = "今天天气好晴朗，处处好风光。" + "你好，世界！" + "张三李四王五赵六。"; 
File.WriteAllText(strAddress, str);
```

##### 往文件追加内容，而不是覆盖

```cs
string str = "打开一个文件，向其中追加指定的字符串，然后关闭该文件。如果文件不存在，此方法创建一个文件，将指定的字符串写入文件，然后关闭该文件。"; 
// 打开一个文件，向其中追加指定的字符串，然后关闭该文件。如果文件不存在，此方法创建一个文件，将指定的字符串写入文件，然后关闭该文件。 
File.AppendAllText(strAddress, str);
```

### FileStream

- 操作字节
- 适用于操作大文件
- 非静态类，可创建对象

#### 读取文件

```cs
string strAddress = @"C:\Users\Zhang\Desktop\阿大.txt"; 
FileStream fs = new FileStream(strAddress, 
FileMode.Open, FileAccess.Read); 
byte[] buffer = new byte[1024*1024*5];// 每次读取5M 
int r = fs.Read(buffer, 0, buffer.Length);// 返回本次实际读取到的有效字节数 
string content = Encoding.UTF8.GetString(buffer); 
// 关闭文件流 
fs.Close(); 
// 释放流所占用的资源 
fs.Dispose(); 
Console.WriteLine(content);

```
#### 写入文件

```cs
string strAddress = @"C:\Users\Zhang\Desktop\阿大.txt";
using (FileStream fw = new FileStream(strAddress, 
FileMode.Open, FileAccess.Write))
{ 
	string str = """ 
			钱塘湖春行 
			唐代：白居易 
	孤山寺北贾亭西，水面初平云脚低。 
	几处早莺争暖树，谁家新燕啄春泥。 
	乱花渐欲迷人眼，浅草才能没马蹄。 
	最爱湖东行不足，绿杨阴里白沙堤。 
	"""; 
	byte[] buffer = Encoding.UTF8.GetBytes(str); 
	fw.Write(buffer, 0, buffer.Length);
}

```

### StreamReader、StreamWriter

```cs
string strAddress = @"C:\Users\Zhang\Desktop\阿大.txt"; 
using(StreamReader sr = new StreamReader(strAddress, Encoding.UTF8)) 
{ 
	while(!sr.EndOfStream) 
	{ 
		Console.WriteLine(sr.ReadLine());
	} 
} 

using (StreamWriter sw = new StreamWriter(strAddress, true, Encoding.UTF8)) 
{
	sw.WriteLine("看我有木有把你覆盖掉"); 
}
```


---

## 加密

- ###  MD5

```cs
string str = "123"; 
string md5 = GetMD5(str);
// result: 202cb962ac59075b964b07152d234b70 
// strNew: 202CB962AC59075B964B07152D234B70 
Console.WriteLine(md5); 

static string GetMD5(string str) 
{ 
	// 创建 MD5 对象 
	MD5 md5 = MD5.Create(); 
	// 开始加密 
	// 需要将字符串转换成字节数组 
	byte[] buffer = Encoding.UTF8.GetBytes(str); 
	// 返回一个加密好的字节数组 
	byte[] newBuffer = md5.ComputeHash(buffer); 
	// 将加密好的字节数组转换成字符串 
	string result = BitConverter.ToString(newBuffer).Replace("-", "").ToLower(); 
	
	// 将字节数组中的每一个元素ToString 
	string strNew = ""; 
	for (int i = 0; i < newBuffer.Length; i++) 
	{ 
	strNew += newBuffer[i].ToString("X2");
	// 如果用小写x2，就是小写的字母 
	} 
	return strNew; 
}
```


---

## ?、??、?. 运算符

### (?)可空类型修饰符（C#2.0-2005-11-07）

- 引用类型可以使用空引用表示一个不存在的值，而值类型通常不能表示为空。
	- 例如：`string str=null;` 是正确的，`int i=null;` 编译器就会报错。
- 为了使值类型也可为空，就可以使用可空类型，即用可空类型修饰符"？"来表示，表现形式为"T？"
	- 例如：`int?` 表示可空的整形，`DateTime?` 表示可为空的时间。
	- `T?` 其实是`System.Nullable`(泛型结构）的缩写形式，也就意味着当你用到`T？`时编译器编译时会把`T？`编译成`System.Nullable`的形式。
	- 例如：`int?`,编译后便是`System.Nullable`的形式。

### (??) 空合并运算符（C#8.0-2019-04-18）

- 用于定义可空类型和引用类型的默认值。**如果此运算符的左操作数不为null，则此运算符将返回左操作数，否则返回右操作数。**
	- 例如：`a??b` 当a不为null时返回a本身，a为null时则返回b，。
- 空合并运算符为右结合运算符，即操作时从右向左进行组合的。如，“`a??b??c`”的形式按“`a??(b??c)`”计算。

```cs
string a = null;
a = "Hello" ?? "World"; 
Console.WriteLine(a);// Hello 

a = null ?? "world"; 
Console.WriteLine(a);// world
```

### (??=)空合并赋值运算符 （C#8.0-2019-04-18）

- 空合并赋值运算符 (??=) 是 ?? 运算符的赋值版本，它允许你为可能为 null 的变量提供一个默认值。**如果变量为 null，则将其赋值为右边的值；否则保持不变。**
- ??= 运算符的左操作数必须是变量、属性或索引器元素。
- `a = a + b ;` =>` a += b;`
	- `a = a ?? b;` => `a ??= b;`

```cs
string nickname = null;// 昵称 
//nickname = nickname ?? "CoolCoder"; 
nickname ??= "CoolCoder"; 
Console.WriteLine(nickname); // 输出: CoolCoder 

string username = "DeveloperDave"; 
//username = username ?? "Newbie"; 
username ??= "Newbie"; 
Console.WriteLine(username); // 输出: DeveloperDave（未改变，因为原本不为null）
```

### (?.)空条件运算符 （C#8.0-2019-04-18）

- 空条件运算符 (?.) 使你能够在访问对象成员之前安全地检查该对象是否为 null。如果对象为 null，则表达式立即返回 null 而不是继续执行成员访问，从而避免了 NullReferenceException。

```cs
Person person = null;
string jobTitle = person?.JobTitle; Console.WriteLine(jobTitle); // 输出: null（而不是引发异常） 

person = new Person { JobTitle = "Software Engineer" }; jobTitle = person?.JobTitle; 
Console.WriteLine(jobTitle); // 输出: Software Engineer
```


---

## 杂项

### 命名约定

- [微软 C# 标识符命名规则和约定](https://learn.microsoft.com/zh-cn/dotnet/csharp/fundamentals/coding-style/identifier-names)

| 风格名称        | 描述                       | 推荐使用                                                        | 示例                             |
| ----------- | ------------------------ | ----------------------------------------------------------- | ------------------------------ |
| Pascal大小写   | 标识符中每个单词的首字母大写           | 用于：命名空间、类、结构、接口、委托、属性、事件、和公共字段、公共方法                         | CardDeck、Dealershand           |
| Camel大小写    | 标识符中第一个单词首字母小写，其他单词首字母大写 | 用于局部变量的名称和方法声明的形参名称                                         | totalCycleCount、randomSeedParm |
| 下划线加Camel小写 | 以下划线开头的Camel大小写          | private、internal；static 的 private或interenal 用`s_`；线程静态用`t_` | _cycleCount、_selectedIndex     |


### 怎么写注释

- 对方法和类使用“///”三斜线注释。
- 代码行文注释采用“//”和“`/**/`”进行，应该尽量说明问题。

```cs
/// <summary> 
/// 在这里简单描述类、方法主要是干什么的。<br/> 
/// 像 <see langword="bool"/> 这样写，可以给关键字啥的添加颜色<br/> 
/// <see cref="MyIntProperty" />， 添加超链接<br/> 
/// </summary> 
/// <remarks> 
/// <para> 
/// 这里可以详细写原理、算法、设计思想等。 
/// </para> 
/// </remarks> 
/// <example> 
/// <code> 
/// 在这里写示例代码 
/// MyClass myClass = new MyClass();
/// myClass.MyMethod(); 
/// </code> 
/// </example> 
/// <param name="a">在这里写参数a的描述</param> 
/// <param name="b">在这里写参数b的描述</param> 
/// <returns>在这里写返回值描述</returns>

```

### 获取变量类型

- BLC 声明了一个叫做Type的抽象类，它被设计用来包含类型的特性。使用这个类的对象能让我们获取程序使用的类型的信息

| 成员            | 成员类型 | 描述                                |
| ------------- | ---- | --------------------------------- |
| Name          | 属性   | 返回类型的名字                           |
| Namespace     | 属性   | 返回包含类型声明的命名空间                     |
| Assembly      | 属性   | 返回声明类型的程序集。如果类型是泛型的，返回定义这个类型的程序集。 |
| GetFields     | 方法   | 返回类型的字段列表，默认返回public类型            |
| GetProperties | 方法   | 返回类型的属性列表，默认返回public类型            |
| GetMethods    | 方法   | 返回类型的方法列表，默认返回public类型            |

- object 是所有类的根类，object 类包含了一个叫做 GetType 的方法，返回对实例的 Type 对象的引用
- 使用 GetType 方法和  typeof 运算符



```cs
Type t = typeof(Zhangsan);
Type t2 =  Zhangsan.GetType();

Type tb = t.BaseType; 
Zhangsan zs = new Zhangsan(); 

Console.WriteLine(t);// Zhangsan 
Console.WriteLine(tb);// Person 
Console.WriteLine(zs.GetType().Name)// Zhangsan 

// 没有写继承哪个类默认继承自 Object 类 
class Person 
{ 
	public string Name { get; set; } 
	public int Age { get; set; } 
} 

class Zhangsan : Person 
{ 
	public string Address { get; set; } 
}
```

### 测试程序运行时间

```cs
using System.Diagnostics; 

Stopwatch sw = new Stopwatch();
sw.Start(); 

foreach (var item in arrayList) 
{ 
	Console.WriteLine(item);
} 
sw.Stop();
Console.WriteLine($"Time elapsed: {sw.Elapsed}");
```

### 控制台

- 控制台高度以行（线）为单位，而不是像素。
- `Console.SetWindowSize(40, 20);`
- 可以通过下面两行代码查看控制台最大高度、宽度
	- `Console.WriteLine(Console.LargestWindowHeight);`
	- `Console.WriteLine(Console.LargestWindowWidth);`

### 不会重复的Guid

```cs
Guid guid = Guid.NewGuid(); 
Console.WriteLine(guid);
```

### 遍历数组

```cs
int[] arr = { 1, 2, 3, 4, 5 }; 
//foreach (var item in arr) 
//{ 
	// Console.Write(item + " ");
//} 

// 对指定数组的每个元素执行指定操作。 
Console.WriteLine("开始："); 
Array.ForEach<int>(arr, x => Console.Write(x + " ")); 

Array.ForEach<int>(arr, x => x *= 2); 
Console.WriteLine("\nArray.ForEach +=2后："); 

Array.ForEach<int>(arr, x => Console.Write(x + " ")); 

arr = arr.Select(x => x * 2).ToArray(); 
Console.WriteLine("\nselect *=5后："); 

Array.ForEach<int>(arr, x => Console.Write(x + " ")); 
/* 
开始： 
1 2 3 4 5 
Array.ForEach *=2后：
1 2 3 4 5 
select *=5后： 
2 4 6 8 10 
*/
```

### CSharp反编译

- [刘铁猛《C#语言入门详解》全集——反反编译部分](https://www.bilibili.com/video/BV13b411b7Ht/?p=14&share_source=copy_web&vd_source=407f92cf6751e29e9d623fde5b09db24&t=833)
- [刘铁猛《C#语言入门详解》全集 - 事件下—反编译2 ](https://www.bilibili.com/video/BV13b411b7Ht/?p=22&share_source=copy_web&vd_source=407f92cf6751e29e9d623fde5b09db24&t=1857)

- 开始搜索 -> Developer Command Prompt for VS2022 -> 输入 `ildasm`  回车
	- 项目生成解决方案->在 bin/net8.0/Debug 文件夹下找到“项目名.exe”，把它拖进ildasm里
	- il：中间语言；Dasm：反编译
	- ildasm 工具帮助我们查看Csharp语言编译好的低级语言代码

- 别的反编译软件
	- [ILSpy](https://github.com/icsharpcode/ILSpy)
	- JetBrains Rider 更多工具窗口-> IL->低级别C#


### [[Computer/计算机相关/dotnet/CSharp/未命名/类图\|类图]]


---

# 进阶知识


## 泛型
#未完成 
- Csharp 提供了5种泛型：类、结构、接口、委托和方法。
- `<T>` 是占位符，可以不写 T ，而是其他任意标识符
- 
### 泛型类

- 声明泛型类

```cs
class SomeClass <T1, T2>
{
	T1 SomeVar = new T1();
	T2 OtherVar = new T2();
}
```

- 创建泛型对象

```cs
SomeClass<short, int> mySc1 = new SomeClass<short, int>;
```

---

## Linq
#未完成 

---

## 多线程、异步编程

视频教程：
- **[C#基础教程 多线程编程入门 Thread/Task/async/await 简单秒懂!]( https://www.bilibili.com/video/BV16G4y1c72R/?share_source=copy_web&vd_source=407f92cf6751e29e9d623fde5b09db24)**

### 简介

- 同步与异步
	- 同步：你做完了我在你的基础上接着做（一条流水线）
	- 异步：咱们两个同时做（相当于汉语中的同步进行）（多条流水线）
- 同步调用与异步调用的对比
	- 每一个运行的程序是一个进程（process）
	- 每个进程可以有一个或多个线程（thread）
	- 同步调用是在同一线程内
	- 异步调用的底层机理是多线程
	- 串行 == 同步 == 单线程；并行 == 异步 == 多线程
- 隐式多线程 VS 显式多线程
	- 直接同步调用：使用方法名
	- 间接同步调用：使用单播/多播委托的invoke方法
	- 隐式异步调用：使用委托的BeginInvoke
	- 显式异步调用：使用Thread或Task


### 委托异步调用

```cs
Student stu1 = new Student { Name = "张三", PenColor = ConsoleColor.Green };
Student stu2 = new Student { Name = "李四", PenColor = ConsoleColor.Yellow };
Student stu3 = new Student { Name = "王五", PenColor = ConsoleColor.Blue };

Action action = stu1.DoHomework;
action += stu2.DoHomework;
action += stu3.DoHomework;

class Student
{
    public string Name { get; set; }
    public ConsoleColor PenColor { get; set; }

    public void DoHomework()
    {
        for (int i = 0; i < 5; i++)
        {
            Console.ForegroundColor = PenColor;
            Console.WriteLine($"{Name} doing homework {i + 1} hours");
            Thread.Sleep(1000);// 暂停1秒
        }
    }
}
```

#### 隐式异步调用

```cs
// .net core平台不支持，要换成.net framework
action.BeginInvoke(null, null);// 隐式异步调用
```

#### 显式异步调用

```cs
// Thread 显式异步调用
Thread thread1 = new Thread(new ThreadStart(stu1.DoHomework));
Thread thread2 = new Thread(new ThreadStart(stu2.DoHomework));
Thread thread3 = new Thread(new ThreadStart(stu3.DoHomework));

thread1.Start();
thread2.Start();
thread3.Start();

/*
 结果：
张三 doing homework 1 hours
李四 doing homework 1 hours
王五 doing homework 1 hours
李四 doing homework 2 hours
王五 doing homework 2 hours
张三 doing homework 2 hours
张三 doing homework 3 hours
李四 doing homework 3 hours
王五 doing homework 3 hours
王五 doing homework 4 hours
张三 doing homework 4 hours
李四 doing homework 4 hours
王五 doing homework 5 hours
李四 doing homework 5 hours
张三 doing homework 5 hours
 
 */

// Task 显式异步调用
Task task1 = new Task(new Action(stu1.DoHomework));
Task task2 = new Task(new Action(stu2.DoHomework));
Task task3 = new Task(new Action(stu3.DoHomework));

task1.Start();
task2.Start();
task3.Start();
Task.WaitAll(task1, task2, task3);

---

Task task1 = Task.Run(() => stu1.DoHomework());
Task task2 = Task.Run(() => stu2.DoHomework());
Task task3 = Task.Run(() => stu3.DoHomework());

Task.WaitAll(task1, task2, task3);
```

### 异步

#### 异步方法

- 用 async 关键字修饰的方法
	- 异步方法的返回值一般是 `Task<T>`，T 是真正的返回值类型，`Task<int>`，惯例：异步方法名字以 Async 结尾
	- 即使方法没有返回值，也最好把返回值声明为非泛型的 Task
	- 调用泛型方法时，一般在方法前加上 await 关键字，这样拿到的返回值就是泛型指定的 T 类型
	- 异步方法的“传染”性：一个方法中如果有 await 调用，则这个方法也必须修饰为 async

```cs
static async Task Main(string[] args)
{
    string fileName = @"C:\Users\Zhang\Desktop\阿大.txt";
    string str = """
    赋得古原草送别

    白居易白居易〔唐代〕

    离离原上草，一岁一枯荣。
    野火烧不尽，春风吹又生。
    远芳侵古道，晴翠接荒城。
    又送王孙去，萋萋满别情。
    """;
    byte[] bytes = Encoding.UTF8.GetBytes(str);
    await File.WriteAllBytesAsync(fileName, bytes);

	string s = await File.ReadAllTextAsync(fileName);
	Console.WriteLine(s);
}
```






---

## 反射和特性
#未完成 

### 反射

>- 反射不是 C# 语言的功能，而是 dotnet 框架的功能
>- 只要有 dotnet 框架的地方,使用什么编程语言都可以使用反射的功能
>
>- 要使用反射，必须使用 System.Reflection 命名空间


### 依赖注入

- 依赖反转是一种思想概念，依赖注入是在这个概念的基础上，结合接口、反射机制所形成的一种应用


---
## solid设计原则

>  **S-single responsibility principle（SRP）—单一职责原则**

- 一个类或一个模块只做一件事，让一个类或者一个模块专注于单一的功能，减少功能之间的耦合程度，这样做在需要修改某个功能时，就不会影响到其他的功能

>  **O—open closed principle（OCP）——开闭原则**

- 对扩展开放，对修改关闭。一个类独立之后就不应该去修改它，而是以扩展的方式适应新需求。

> **L—liskov substitution principle（LSP）—里氏替换原则**

- 所有基类出现的地方都可以用派生类替换，而不会让程序产生错误，派生类可以扩展基类的功能，但不能改变基类原有的功能。

>  **I—interface segregation principle（ISP）—接口隔离原则**

- 一个接口应该拥有尽可能少的行为，使其精简单一。对于不同的功能的模块分别使用不同接口，而不是使用同一个通用的接口。

>  **D—depend inversion principle（DIP）—依赖倒置原则**

- 高级模块不应该依赖低级模块，而是依赖抽象接口，通过抽象接口使用对应的低级模块。

### 依赖反转

- 高层的模块不应该依赖于低层的模块，二者都应该依赖于抽象类，抽象类不应该依赖于细节，而是细节依赖于抽象类
	- 抽象类：抽象类和接口 细节：就是实现抽象类或接口的具体类。

- 比如（[[Computer/计算机相关/dotnet/CSharp/未命名/类图\|类图]]）:
```mermaid
classDiagram
class Driver{
	-car:Car
	+Drive()
}

class Trucker{
-truck:Truck
+Drive()
}

class Racer{
-raceCar:RaceCar
+Drive()
}

class Car{
+Run()
}

class Truck{
+Run()
}

class RaceCar{
+Run()
}

Driver .. >Car
Trucker .. > Truck
Racer .. > RaceCar
```

```mermaid
classDiagram
class IVehicle{
	<<Interface>>
	+Run()
}

class Driver{
	-vehicle:IVehicle
	+Drive()
}

class Car{
	+Run()
}

class Truck{
	+Run()
}

IVehicle <.. Driver
IVehicle <|.. Car
IVehicle <|.. Truck
```


```mermaid
classDiagram

class IDriver{
	<<Interface>>
	-vehicle:IVehicle
	+Drive()
}
class IVehicle{
	<<Interface>>
	+Run()
}
class Driver{
	-vehicle:IVehicle
	+Drive()
}
class AiDriver{
	-vehicle:IVehicle
	+Drive()
}
class Car{
	+Run()
}
class Truck{
	+Run()
}

IDriver <|.. Driver
IDriver <|.. AiDriver
IDriver <.. IVehicle
IVehicle <|.. Car
IVehicle <|.. Truck
```

















---
始建于：2025-3-15-17：24

 

[历代 C# 语言特性，C# 发展历史——微软官方]:https://learn.microsoft.com/zh-cn/dotnet/csharp/whats-new/csharp-version-history

[微软 C# 官方文档]:https://learn.microsoft.com/zh-cn/dotnet/csharp/tour-of-csharp/


---
[^1]: 引用于：[刘铁猛《C#语言入门详解》全集  1分25秒处弹幕](https://www.bilibili.com/video/BV13b411b7Ht/?p=20&share_source=copy_web&vd_source=407f92cf6751e29e9d623fde5b09db24&t=83) 

[^2]: 引用于：[刘铁猛《C#语言入门详解》全集  1:02:06 处弹幕](https://www.bilibili.com/video/BV13b411b7Ht/?p=22&share_source=copy_web&vd_source=407f92cf6751e29e9d623fde5b09db24&t=3726)
