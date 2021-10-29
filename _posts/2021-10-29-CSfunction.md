---
layout: post
title: C#-函数
date: 2021-10-29 12:00 +0800
tags: [learning, c#]
author: LMCube
toc:  true
---

> 由于C语言和C#有部分地方相似，故以前的部分知识不做详细回顾

## 函数

格式如下

```c#
static void name() //or Main(string[] args)
{
	//Code
}
```

函数在命名后仅有在被调用时才会开始执行内部相关代码。

eg.

```c#
        static void Write()
        {
            string mystring = "String defined in Write()";
            
            WriteLine("Now in Write()");
            WriteLine($"mystring = {mystring}");
        }
```

在Main()函数中必须使用`Write()`后才能执行Write()内部的代码

如下

```c#
        static void Main(string[] args)
        {
            Write();
            //Write()
            ReadKey();
        }
```



## 局部&全局变量

**局部变量**

指在指定函数声明的变量，such as

```c#
        static void Main(string[] args)
        {
            string mystring = "String defined in Main()";
            //上述为局部变量
            WriteLine($"mystring = {mystring}");
            ReadKey();
        }
```

局部变量仅能在该函数内调用，无法跨函数使用



**全局变量**

声明全局变量的方法如下

```c#
    class Program
    {
        static string mystring;
        //static是声明全局变量的关键词
        //声明全局变量 Program.mystring，可在任意函数调用
        static void Main(string[] args)
        {
            Program.mystring = "Global String";
            //给全局变量Program.mystring赋值
            WriteLine($"Global string = {Program.mystring}");
            ReadKey();
        }
    }


```

在class里使用**static**前缀可声明全局变量，所有隶属于该程序的函数均可调用该变量。

其中 全局变量的名称 不会与 局部变量的名称 冲突。

调用方法为`Program.XXXXX`，意为调用Program内的XXXX变量



**其他类似的情况**

在同一函数中，以下情况的变量均有使用范围。

**1.声明位置出错**

```c#
int i;
for(i = 0 ; i <10 ; i++)
{
    text = "Line" + Convert.Tostring(i);
    WriteLine($"{text}");
}
WriteLine($"Result : {text}")
```

该代码中的text变量仅在for循环内被声明，无法在循环外调用该变量。

**2.仅在特定情况下初始化函数**

```c#
int i;
string text;
for(i = 0 ; i <10 ; i++)
{
    text = "Line" + Convert.Tostring(i);
    WriteLine($"{text}");
}
WriteLine($"Result : {text}")
```

该情况也不可运行，text仅在for循环内被初始化，但跳出循环块后数据会丢失，循环外的WriteLine函数无法读取。

若要读取只能重新初始化。

**3.正确初始化的方法**

```c#
int i;
string text = "";						//给text赋值后text才会被分配内存空间
for(i = 0 ; i <10 ; i++)
{
    text = "Line" + Convert.Tostring(i);
    WriteLine($"{text}");
}
WriteLine($"Result : {text}")
```

text在声明后立刻被初始化并赋予空白数据，此后在循环内的数据将被保留，所有函数均可访问。

