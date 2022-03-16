# c++ DSA



来自 《数据结构与算法 c++语言描述一书》 不看了现在



## 一 程序设计：综述

### 1.4 C++ 类

#### 1.4.1 基本class语法

```
class IntCell
{
public:
	IntCell() { storedValue = 0; };
	IntCell(int initialValue) { storedValue = initialValue; };
	int read() { return storedValue; }
	void write(int x) { storedValue; }
private:
	int storedValue;
};
```

改进：

#### 1.4.2 构造函数的附加语法和访问函数

```
class InCell
{
public:
	explicit InCell(int initialValue = 0) // 单构造函数为 explicit ，防止后台类型转换，正常情况下，定义的是一个隐式类型转换
		: storedValue{ initialValue } { } // 初始化表列 initialization list
	int read() const
	{
		return storedValue;
	}
	void write(int x) { storedValue = x; }


private:
	int storedValue;
};
```

explicit : 注意 正常情况单参数构造函数定义了一个隐式类型转换，会创建一个临时对象，这个对象使得赋值兼容

```
InCell obj;
obj = 37;

// 会变成：
IntCell temporary = 37;
obj = temporary;
```

const：默认情况下，所有的成员函数都应该是修改函数，为了使得成员换上变为访问函数，应该在`()`后加上 `const` 

#### 1.4.3 接口与实现的分离

在 main 函数中调用：

```
#include<iostream>
#include<IntCell.h>
using namespace std;

int main() {

	IntCell m;

	m.write(5);
	cout << "Cell contents: " << m.read() << endl;

	return 0;
}
```

于 `IntCell.h` 中定义接口：

```
#ifndef IntCell_H
#define IntCell_H

class IntCell
{
public:
	explicit IntCell( int initalValue = 0 );
	int read() const;
	void write(int x);
private:
	int storedValue;
};
#endif
```

于 `IntCell.cpp` 中实现接口：

```
#include<IntCell.h>

IntCell::IntCell(int initialValue) : storedValue{ initialValue } {}

int IntCell::read() const
{
	return storedValue;
}

void IntCell::write(int x) 
{
	storedValue = x;
}
```

#### 预处理： #ifndef 

1. 为了防止一个接口被读两次，预定义一个唯一符号`IntCell_H`，构建时候会检测`#ifndef`,若是已经读取过会跳到`#endif`

#### 1.4.4 vector 和 string

- C++11 中允许了`vector<int> daysInMonth = {31,28,31,30,31,...}`的初始化方法
    - `vector<int> daysInMonth {12}` 
    - `vector<int> daysInMonth (12)` 

### 1.5 c++ 细节

#### 1.5.1 指针 pointer

改写 1.4.3 的调用

```
#include<iostream>
#include<IntCell.h>
using namespace std;

int main() {

	//IntCell m;
	IntCell* m; // 注意没有初始化

	//m.write(5);
	m = new IntCell{ 0 }; // 花括号 
	//cout << "Cell contents: " << m.read() << endl;
	cout << "Cell contents: " << m->read() << endl;

	delete m;

	return 0;
}


```

#### 1.5.2 左值 右值 引用

左值：标识非临时性对象的表达式

右值：标识临时性对象的表达式

一般来说，有变量名，就是左值

##### 左值引用

1. 复杂名称别名
```
auto & whichList = theLists[myhash(x,theLists.size())]

//若没有 & 会导致pushback作用于拷贝

if(find(begin(whichList),end(whichList),x)!=end(whichList)) return false;

whichList.push_back(x);
```
2. 范围 for 循环

```
for(auto & x:arr) ++x;
```

3. 避免复制
```
auto & x = findMax(arr);
//auto 将推导出常态性
```
右值引用：略

#### 1.5.3 参数传递
call-by-value 下，实参复制到形参

#### 1.5.5 std::swap std:move

#### 1.5.6 构造 拷贝构造 移动构造 拷贝赋值 移动赋值

