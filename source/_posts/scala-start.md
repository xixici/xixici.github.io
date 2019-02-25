---
title: scala自我书写
date: 2019-02-15 21:48:30
tags: scala
categories: 学习笔记
---

# Scala基础

## Scala变量

首先,Scala有两种变量
- 变量: 其值可以改变, 关键词 `var`
- 常量: 其值不能改变, 关键词 `val`
<!--more-->
```
object HelloWorld {
  def main(args: Array[String]): Unit ={
    //4种声明变量的方式
    //可变变量var 不可变变量val
    //声明变量类型
    //val or var 变量名 : 变量类型 = 变量初始值
    var myVar : String = "myVar";
    val myVal : Int = 1;
    //不声明变量类型 类型推断
    var myVar1 = 20;
    val myVal1 = "sdfsd";
    //多个赋值
    val myVal22, myVal33 = 100;
    val(myVal2: Int, myVal3: String) = Pair(40,"myVal3");
    println(myVar); println(myVal);println(myVar1);println(myVal1);
    println(myVal2);println(myVal3);
  }
}
```

## Scala访问修饰符
类似Java, Scala修饰符有:private , public, protected, 默认未声明时为public, 同时Scala较Java更为严格

### 私有(private)成员
用private关键字修饰，带有此标记的成员仅在包含了成员定义的类或对象内部可见，同样的规则还适用内部类。(Java允许外部类访问内部类的私有成员)
### 保护(Protected)成员
只允许保护成员在定义了该成员的的类的子类中被访问。(Java同一packge都可以访问)
### 公共(Public)成员
任何地方均可以访问

## Scala运算符
### 算术运算符
同Java, 5类 
```
+ //加 +
- //减 -
* //乘 *
/ //除 /
% //取余 %
```
### 关系运算符
同Java, 6类
```
== //等于
!= //不等于
>  //大于
<  //小于
>= //大于等于
<= //小于等于
```
### 逻辑运算符
同Java, 3类
```
&& //逻辑与
|| //逻辑或
!  //逻辑非
```
### 位运算符
位运算针对二进制进行操作,有7类
```
&  //按位与
|  //按位或
^  //按位异或
~  //按位取反
<<  //按位左移运算符
>>  //按位右移运算符
>>>  //无符号右移
```
### 赋值运算符
```
=	//简单赋值
+=	//相加后赋值
-=	//相减后赋值
*= 	//相乘后赋值
/=	//相除后赋值
%=	//求余后赋值
<<=  //按位左移后再赋值
>>=  //按位右移后再赋值
&=	//按位与后赋值
^=	//按位异或后赋值
|=	//按位或后赋值
```

## Scala控制语句
### If
```
if(布尔表达式)
{
   // 如果布尔表达式为 true 则执行该语句块
}
```
### If...Else
```
if(布尔表达式){
   // 如果布尔表达式为 true 则执行该语句块
}else{
   // 如果布尔表达式为 false 则执行该语句块
}
```
### if...else if...else 
```
if(布尔表达式 1){
   // 如果布尔表达式 1 为 true 则执行该语句块
}else if(布尔表达式 2){
   // 如果布尔表达式 2 为 true 则执行该语句块
}else if(布尔表达式 3){
   // 如果布尔表达式 3 为 true 则执行该语句块
}else {
   // 如果以上条件都为 false 执行该语句块
}
```
### While
运行一系列语句，如果条件为true，会重复运行，直到条件变为false。
```
while(condition)
{
   statement(s);
}
```
### do while
条件表达式出现在循环的尾部，所以循环中的 statement(s) 会在条件被测试之前至少执行一次。
```
do {
   statement(s);
} while( condition );
```

### for

```
for( var x <- Range ){
   statement(s);
}
```

range是个范围,左箭头←这个家伙是生成器（generator）,可以理解成后面的范围中生成单值.

for也能用来进行多范围遍历,例如
```
for( a <- 1 to 3; b <- 1 to 3){
	println( "Value of a: " + a );
    println( "Value of b: " + b );
}
```
这样将遍历出所有情况,即所有可能性.

#### until 与 to
to为包含上限的闭区间，如：1 to 3,Range为1,2,3;
until不包含上限，如：1 until 3, Range为1,2

for也能用来遍历集合
```
for( var x <- List ){
   statement(s);
}
```
for的过滤,在for语句中加if条件
```
var a = 0;
val numList = List(1,2,3,4,5,6,7,8,9,10);

for( a <- numList 
	if a != 3; if a < 8 ){
		println( "Value of a: " + a );
}
```
for的存储与返回
```
var a = 0;
val numList = List(1,2,3,4,5,6,7,8,9,10);

// for loop execution with a yield
var retVal = for{ a <- numList if a != 3; if a < 8 }yield a //yield给a

// Now print returned values using another loop.
for( a <- retVal){
 println( "Value of a: " + a );
}
```

## Scala数组
### 定长数组

### 变长数组
## Scala函数


### 按名称调用函数
### 命名参数的函数
### 可变参数的函数
### 递归函数
### 默认参数值函数
### 高阶函数
### 嵌套函数
### 匿名函数
### 部分应用函数
### 柯里化函数


spark2-submit --driver-memory 5G --executor-memory 5G --conf spark.kryoserializer.buffer.max=2047m --jars SparkOnHBase-assembly-0.1-SNAPSHOT-deps.jar --master yarn --class "SparkOnHBase" sparkonhbase_2.11-0.1-SNAPSHOT.jar 

yarn application -list 查询所有的任务；
然后使用yarn application -kill <appId> 
	yarn application -kill application_1512629122215_0235


