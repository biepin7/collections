# about 程序结构

## 1.1 命名 / Names

1. 一个名字必须以一个字母（Unicode字母）或下划线开头，后面可以跟任意数量的字母、数字或下划线

2. 大写字母和小写字母是不同的

3. 函数内部定义，那么它的就只在函数内部有效。如果是在函数外部定义，那么将在当前包的所有文件中都可以访问 。 If an entity is declared within a function, it is **local** to that function. If declared outside of a function, however, it is visible in **all files of the  package** to which it belongs. 

4. 如果一个名字是大写字母开头的，那么它将是**导出的**，也就是说可以被外部的包访问 The cas  of the first letter of a name determines its visibility across package bound aries. If the name begins with an upper-case letter, it is **exported**, which means that it is visible and accessible** **outside of**
    its own package** and may be referred to by other parts of the program

关键字 Keywords：

![](https://raw.githubusercontent.com/biepin7/CloudForImg/master/20220212124433.png)

内建常量 Constants : true false iota nil

内建类型 : int int8 int16 int32 int64
				   uint uint8 uint16 uint32 uint64 uintptr
				   float32 float64 complex128 complex64
				   bool byte rune string error

内建函数: make len cap new append copy close delete
				   complex real imag
				   panic recover

## 1.2 声明 / Declarations

There arefour major kinds of declarat ions: var, const, type, and func.

Each file begins with a **package declaration** that says what package the file is par t of . 

## 1.3 变量的声明

Package-level variables are initialized before main begins , 
and local variables are initialized as their declarations are encountered during function execution.
包级别声明的变量会在main入口函数执行前完成初始化
局部变量将在声明语句被执行到的时候完成初始化


#### 基础声明 var
```
var name type = expression
```

1. type 和 expression 可以省略其中一个
2. 省略 type ，会根据 expression 自动推断
3. 省略 expression  ， value is the zero value for the type
> bool ： false  ; strings : "" ; interfaces and reference : nil; struct and arrary : 对应元素的零值（the zero value）
4. 确保了每个声明的变量都有一个定义的值（不会存在声明和定义的割裂）

#### 同时声明一组变量
```
var i, j, k int 
var b, f, s = true, 2.3, "four" 
var f, err = os.Open(name)
```

#### 简短变量声明 short variable declaration

- 用于大部分的局部变量的声明和初始化
- 对已经声明过的变量就只有赋值行为，但是至少要有一个新变量
- 只有对已经在同级词法域声明过的变量才和赋值操作语句等价，如果变量是在外部词法域声明的，那么简短变量声明语句将会在当前词法域重新声明一个新的变量

```
 name := expression
```

```
i := 100
i,j := 0,1
```

#### 指针

#### new 函数

The expression `new(T)` creates an unnamed variable of type T, initializes it to the zero value of T, and returns its address, which is a value of type *T.

#### Lifetime of Variables

对于在包一级声明的变量来说，它们的生命周期和整个程序的运行周期是一致的

局部变量的声明周期则是动态的：从每次创建一个新变量的声明语句开始，直到该变量不再被引用为止，然后变量的存储空间可能被回收。

函数的参数变量和返回值变量都是局部变量。它们在函数每次被调用的时候创建。

自动圾收集器: #todo

## 1.4 赋值

#### 元组赋值

```
a[i], a[j] = a[j], a[i]
```

在赋值之前，赋值语句右边的所有表达式将会先进行求值，然后再统一更新左边对应变量的值。



#### Assignability 可赋值性

讲隐式赋值

#### 1.5 类型声明 Type Declarations

```
type name underlying-type
```

注意声明后 即使底层类型相同也不再兼容

需要时，需要类型转换（）



# about 基础数据类型

基础类型、复合类型、引用类型和接口类型

## Integers

## string



# about 复合数据类型 Composite Types

## 数组 Arrays

```
var a [3]int 

var r [3]int = [3]int{1, 2}

q := [...]int{1, 2, 3}

r := [...]int{99: -1} // 99个0 1个1

for i,v := range a{
	fmt.Printf("%d %d\n", i, v)
}
```

## Slice

