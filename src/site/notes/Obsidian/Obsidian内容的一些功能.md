---
{"dg-publish":true,"permalink":"/Obsidian/Obsidian内容的一些功能/","tags":["gardenEntry"],"updated":"2025-03-31T21:05:17.535+08:00"}
---

# 插入东西

---
## 嵌入内容

链接  [[计算机相关/dotnet/CSharp/CSharpStudy\|CSharpStudy]]


<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/obsidian//" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">




反链接 [[Obsidian/Obsidian内容的一些功能\|Obsidian内容的一些功能]]
这是你的新*仓库*。

写点笔记，[[Obsidian/Obsidian内容的一些功能\|Obsidian内容的一些功能]]，或者试一试[导入器](https://help.obsidian.md/Plugins/Importer)插件!

当你准备好了，就将该笔记文件删除，使这个仓库为你所用。


</div></div>


### 嵌入标题


<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="//dotnet/c-sharp/c-sharp-study/#" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">



# 基础知识

## 类型

### 值类型

| 名称      | 含义              | 范围                                                           | .Net框架类型       | 默认值         |
| ------- | --------------- | ------------------------------------------------------------ | -------------- | ----------- |
| sbyte   | 8位有符号整数         | -128~127                                                     | System.Sbyte   | 0           |
| byte    | 8位无符号整数         | 0~255                                                        | System.byte    | 0           |
| short   | 16位有符号整数        | -32768~32767                                                 | System.Int16   | 0           |
| ushort  | 16位无符号整数        | 0~35535                                                      | System.UInt16  | 0           |
| int     | 32位有符号整数        | -2147 483 648~<br><br>2 147 483 647                          | System.Int32   | 0           |
| uint    | 32位无符号整数        | 0~4 294 967 295                                              | System.UInt32  | 0           |
| long    | 64位有符号整数        | -9 223 372 036 854 775 808~<br><br>9 223 372 036 854 775 807 | System.Int64   | 0           |
| ulong   | 64位无符号整数        | 0~18 446 744 073 709 551 615                                 | System.UInt64  | 0           |
| float   | 单精度浮点数          | 1.5*10 -45~<br><br>3.4*10 38                                 | System.Single  | 0.0f        |
| double  | 双精度浮点数          | 5*10 -324~<br><br>1.7*10 308                                 | System.Double  | 0.0d        |
| bool    | 布尔型             | true 或 false                                                 | System.Boolean | false       |
| char    | Unicode字符串      | U+0000~U+ffff                                                | System.Char    | '\0' 即 null |
| decimal | 小数类型的有效数字精度为28位 | +-1.0*10 28~<br><br>+-7.9*10 28                              | System.Decimal | 0m          |

## 转换

### 显式转换

- Convert.ToInt32()
	- [四舍六入五成双](https://baike.baidu.com/item/%E5%9B%9B%E8%88%8D%E5%85%AD%E5%85%A5%E4%BA%94%E6%88%90%E5%8F%8C/9062547) 		- （1）被修约的数字小于5时，该数字舍去；
		- （2）被修约的数字大于5时，则进位；
		- （3）被修约的数字等于5时，要看5前面的数字，若是奇数则进位，若是偶数则将5舍掉，即修约后末尾数字都成为偶数；若5的后面还有不为“0”的任何数，则此时无论5的前面是奇数还是偶数，均应进位。

## ref引用

- ref 必须位于类型和名称前面
	- int ref i = ref j; // 错误
	- ref int i = ref j;// 正确
	- int ref j;// 错误，必须要有初始值

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

- XXX.ToString("X2");

### [元组（C#7.0-2017 年 3 月）](https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/value-tuples)

元组最常见的用例之一是作为方法返回类型。 也就是说，你可以将方法结果分组为元组返回类型，而不是定义 out 方法参数，如以下示例所示：

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

## ?、??、?. 运算符

### (?)可空类型修饰符（C#2.0-2005-11-07）

- 引用类型可以使用空引用表示一个不存在的值，而值类型通常不能表示为空。
	- 例如：string str=null; 是正确的，int i=null; 编译器就会报错。
- 为了使值类型也可为空，就可以使用可空类型，即用可空类型修饰符"？"来表示，表现形式为"T？"
	- 例如：int? 表示可空的整形，DateTime? 表示可为空的时间。
	- T? 其实是System.Nullable(泛型结构）的缩写形式，也就意味着当你用到T？时编译器编译 时会把T？编译成System.Nullable的形式。
	- 例如：int?,编译后便是System.Nullable的形式。

### (??) 空合并运算符（C#8.0-2019-04-18）

- 用于定义可空类型和引用类型的默认值。**如果此运算符的左操作数不为null，则此运算符将返回左操作数，否则返回右操作数。**
	- 例如：a??b 当a不为null时返回a本身，a为null时则返回b，。
- 空合并运算符为右结合运算符，即操作时从右向左进行组合的。如，“a??b??c”的形式按“a??(b??c)”计算。

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
- a = a + b ; => a += b;
	- a = a ?? b; => a ??= b;

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

## 装箱、拆箱

- 装箱：将值类型转换为引用类型
- 拆箱：将引用类型转换为值类型
- 看两种类型是否发生了装箱或者拆箱，要看，这两种类型是否存在继承关系。
	- 有继承关系可能发生装箱，无继承关系一定不会发生装箱
	- 如：string str = "123"; int i = (int)str; 没有发生拆箱，因为 int 和 string 没有继承关系
- 装、拆箱会影响性能

## 集合

- ### ArrayList
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
- ### List<>
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

## 面向对象

### 类

- 自动属性（C#3-2007-11-06）
	- public string Name {get; set;}
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
	- **构造器不被继承**

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

- 抽象类为做基类而生，我们应该封装那些不变的、稳定的、固定的和确定的成员，而把那些不确定的、有可能改变的成员声明为抽象成员，并且留给子类去实现——[27集，18：30](【刘铁猛《C#语言入门详解》全集】 【精准空降到 18:24】 https://www.bilibili.com/video/BV13b411b7Ht/?p=27&share_source=copy_web&vd_source=407f92cf6751e29e9d623fde5b09db24&t=1104)
- 抽象类不一定有抽象方法，但有抽象方法的类一定是抽象类
- 抽象方法不能是 private 的
- 抽象类不能被实例化

#### 依赖反转

- 高层的模块不应该依赖于低层的模块，二者都应该依赖于抽象类，抽象类不应该依赖于细节，而是细节依赖于抽象类
	- 抽象类：抽象类和接口 细节：就是实现抽象类或接口的具体类。

## 接口

- 接口是一种约束，[只要是继承自这个接口的类，强制实现接口中的方法](https://www.bilibili.com/video/BV1hx4y1G7C6/?p=40&share_source=copy_web&vd_source=407f92cf6751e29e9d623fde5b09db24&t=339)
	- 所以多态中，用接口类型变量引用继承该接口的类实例对象，必然可以调用接口所含有的方法

- **接口只能有方法、属性、索引器、事件，不能有字段和构造函数**
- 接口不能被实例化，接口与接口之间可以继承，并且可以多继承
- 接口不能继承一个类，而类可以继承接口（接口只能继承接口，而类既可以继承接口，又可以继承类）
- 一个类可以同时继承一个类并实现多个接口，如果一个子类同时继承了父类A，并实现了接口IA，那么语法上A必须写在IA的前面
- C#12中，接口成员可以添加 public internal修饰符了
- C#8.0接口中的方法可以有方法体（默认实现）了

## 用什么方式实现多态

> 什么时候用虚方法来实现多态？

   几个子类中可以抽象提取出一个公共的父类，并且父类必须写上几个子类共有的方法，但是又不知道父类方法具体怎么写，而且需要父类实例化对象

> 什么时候用抽象类来实现多态？

   和上面一样，但是不需要父类实例化

>什么时候用接口来实现多态？

 几个子类根本就抽象不出父类，但是他们都有一个共同的行为、能力

## 委托

- 委托是一种类，类是数据类型，所以委托也是一种数据类型。
	- 委托是类，所以写在class外边

- 可以把类看成是一个类型安全的、面向对象的C\C++ 函数指针
- 委托的作用
	- 函数传参
	- 回调函数

 
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

> **为避免调用空委托，可以使用空条件运算符**

- myDelegate?.Invoke("你好，世界！");
- myDelegate?.("你好，世界！");

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

## 事件





## 匿名方法（C#2.0 2005-11-07）

### 语法

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

### 返回类型

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

### params 参数

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

## Lambda 表达式（C#3.0 2007-11-06）

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

## solid设计原则

>  S-single responsibility principle（SRP）—单一职责原则

- 一个类或一个模块只做一件事，让一个类或者一个模块专注于单一的功能，减少功能之间的耦合程度，这样做在需要修改某个功能时，就不会影响到其他的功能

>  O—open closed principle（OCP）——开闭原则

- 对扩展开放，对修改关闭。一个类独立之后就不应该去修改它，而是以扩展的方式适应新需求。

> L—liskov substitution principle（LSP）—里氏替换原则

- 所有基类出现的地方都可以用派生类替换，而不会让程序产生错误，派生类可以扩展基类的功能，但不能改变基类原有的功能。

>  I—interface segregation principle（ISP）—接口隔离原则

- 一个接口应该拥有尽可能少的行为，使其精简单一。对于不同的功能的模块分别使用不同接口，而不是使用同一个通用的接口。

>  D—depend inversion principle（DIP）—依赖倒置原则

- 高级模块不应该依赖低级模块，而是依赖抽象接口，通过抽象接口使用对应的低级模块。

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

 - ####  读取文件
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

- #### 写入文件

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


## 杂项

### 怎么写注释

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

- Object 是所有类的根类

```cs
Type t = typeof(Zhangsan); 
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
- Console.SetWindowSize(40, 20);
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

Array.ForEach<int>(arr, x => Console.Write(x + " ")); /* 
开始： 
1 2 3 4 5 
Array.ForEach *=2后：
1 2 3 4 5 
select *=5后： 
2 4 6 8 10 
*/
```


</div></div>


### 嵌入内容块


<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="//dotnet/c-sharp/c-sharp-study/#258d2f" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">



	- [四舍六入五成双](https://baike.baidu.com/item/%E5%9B%9B%E8%88%8D%E5%85%AD%E5%85%A5%E4%BA%94%E6%88%90%E5%8F%8C/9062547) 

</div></div>


## 插入附件

![[跟韩愈柳宗元轻松学写议论文～.mp4]]


## 插入代码块

```csharp
MyDelegate myDelegate = new MyDelegate(PrintMessage);
myDelegate -= PrintMessage;
```

`{cs icon title:print}Console.WriteLine("你好，世界！")`
## 插入表格

| 1   | 2   |     |
| --- | --- | --- |
|     |     |     |
|     |     |     |
|     |     |     |
##   插入标注

> [!tip] 提示
> Contents

> [!NOTE] 备注
> Contents

> [!info] 信息
> Contents

> [!warning] 警告
> Contents

> [!danger] 危险
> Contents

> [!question] 问题
> Contents

> [!example] 举例
> Contents

> [!todo] Title
> Contents

> [!NOTE]+ 折叠标注
> Information

> [!TIP] 嵌套标注
> Text inside the tip callout
> > [!EXAMPLE] Inner callout
> > Multiple nesting layers
> > > [!TODO] Inner inner callout


## 插入脚注

此行文本有一条脚注[^1]

[^1]: 这是一条脚注


---
# [Mermaid 使用教程](https://zhuanlan.zhihu.com/p/625897489)

# 功能

### 突出显示文本

==床前明月光，疑是地上霜。==

### 复选框

快速插入复选框： ctrl + L
- [ ] adada
- [x] asdada
