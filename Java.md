[toc]
# 第三章 Java的基本程序数据结构

## 3.1一个简单的Java应用程序

```
public class TestSample {
    public static void main(String[] args) {
        System.out.println("We will not use 'Hello,World!");
    }
}

Java区分大小写
关键字public称为访问修饰符（access modifier）,这些修饰符用于控制程序的其他部分对这段代码的访问级别
关键字class表明Java程序中的全部内容都包含在类中。这里，只需要将类作为一个加载程序逻辑的容器，程序逻辑定义了应用程序的行为。

```

## 3.2注释
```
// 单行注释
/*
*
*/	多行
```
## 3.3数据类型
Java是一种强类型语言。每一个变量必须声明一种类型。
8种基本类型（primitive type),4种整形，2种浮点类型，1种用于表示Unicode编码的字符单元的字符类型char和1种用于表示真值得boolean类型。
### 整型
Java整型
|类型|存储需求|取值范围|
|---|---|---|
|int|4字节|-2 147 483 648 ~ 2 147 483 647（正好超过20亿）|
|short|2字节|-32 768 ~ 32 767|
|long|8字节|-9 223 372 036 854 775 808 ~ 9 223 372 036 854 775 807|
|byte|1字节|-128 ~ -127|
### 浮点类型
|类型|存储需求|取值范围|
|---|---|---|
|float|4字节|大约±3.402 823 47E+38F(有效位数为6 ~ 7位)|
|double|8字节|大约±1.797 693 134 862 315 70E+308（有效位数为15位）|
	double表示的数值精度是float类型的两倍（有人称之为双精度数值）
### char类型
特殊字符的转义序列
|转义序列|名称|Unicode值|
|:---:|:---:|:---:|
|\b|退格|\u0008|
|\t|制表|\u0009|
|\n|换行|\u000a|
|\r|回车|\u000d|
|\"|双引号|\u0022|
|\'|单引号|\u0027|
|\\|反斜杠|\u005c|
### Unicode 和 char类型
	对于任意给定的代码值，在不同的编码方案下有可能对应不同的字母；二是采用大字符集的语言其编码长度有可能不同。
	设计Unicode编码的目的就是要解决这些问题。
	在Java中，char 类型描述了UTF-16编码中的一个代码单元。
	我们强烈建议不要在程序中使用char类型，除非确实需要处理UTF-16代码单元。最好将字符串作为抽象数据类型处理。
### boolean类型
	boolean(布尔)类型有两个值:false和true,用来判定逻辑条件.整型值和布尔值之间不能进行相互转换.
### 变量
	在Java中,每个变量都有一个类型(type).在声明变量时,变量的类型位于变量名之前.
```
double salary;	int vacationDays;
由于声明是一条完整的Java语句,所以必须以分号结束.变量中所有的字符都是有意义的,并且大小写敏感.变量名的长度基本上没有限制.
不能用Java保留字作为变量名,可以在一行中声明多个变量:
int i,j; //both are integers
不过,不提倡使用这种风格.逐一声明每一个变量可以提高程序的可读性
```
### 变量初始化
```
生命一个变量之后,必须用赋值语句对变量进行显式初始化,千万不要使用未初始化的变量.
例如,Java编译器认为下面的语句序列是错误的:
int vacationDays;
System.out.println(vacationDays); //Error--cariable not intiallized
对已经声明过的变量进行赋值,需要将变量名放在等号(=)左侧,相应取值的Java表达式放在等号的右侧.
int vacationDays;
vacationDays = 12;

也可以将变量的声明和初始化放在同一行中.例如:
int vacationDays =12;

最后,再Java中可以将声明放在代码中的任何地方.例如,下列代码的书写形式在Java中是完全合法的:
double salary = 65000.0;
System.out.println(salary);
int vacationDays = 12; //OK to declare a variable here

在Java中,变量的声明尽可能地靠近变量第一次使用的地方,这是一种良好的程序编写风格
```
### 常量
```
在Java中,利用关键字final指示常量.例如:

public class Constants {
    public static void main(String[] args) {
        final double CM_PER_INCH =2.54;
        double paperWidth = 8.5;
        double paperHeight =11;
        System.out.println("Paper size in centimeters:"
        +paperWidth * CM_PER_INCH + "by" +paperHeight*CM_PER_INCH);
    }
}

关键字final表示这个变量只能被赋值一次.习惯上,常量名使用全大写.

在Java中,经常希望某个常量可以在一个类中的多个方法中使用,通常将这些常量称为类常量.可以使用关键字static final 设置一个类常量.下面是使用类常量的示例:
public class Constants2 {
    public static final double CM_PER_INCH=2.54;
    public static void main(String[] args) {
        double paperWidth =8.5;
        double paperHeight=11;
        System.out.println("Paper size in centimeters:"
        + paperWidth * CM_PER_INCH+"by" + paperHeight* CM_PER_INCH);
          
    }
}

需要注意,类常量的定义位于main方法的外部.因此,在同一个类的其他方法中也可以使用这个厂两.而且,如果一个常量被声明为public.那么其他类的方法也可以使用这个常量.在这个市里中,Constants2.CM_PER-INCH就是这样一个常量.
```
### 运算符
```java
在Java中,使用算数运算符+,-,*,/表示加减乘除运算.当参与/运算的两个操作数都是整数时,表示整数除法;否则,表示浮点除法.整数的求余操作(有时称为取模)用%表示.例如,15/2等于7,15%2等于1,15.0/2等于7.5.
需要注意,整数被0除将会产生一个异常,而浮点数被0除将会得到无穷大或NaN结果
```