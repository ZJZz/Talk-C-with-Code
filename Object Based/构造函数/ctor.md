# 构造函数

## 初始化列表

运行在初始化阶段，与赋值阶段不同，可以对一些如const类型的变量进行初始化。

[侯捷-Initializer list 上](https://www.bilibili.com/video/av51863195/?p=5)
[侯捷-Initializer list 下](https://www.bilibili.com/video/av51863195/?p=6)

```cpp
complex(double r = 0, double i = 0): re(r), im(i)
{}

complex(double r = 0, double i = 0): re(r), im(i) 
complex(): re(0), im(0) {} // 不可以，因为有初值  ???
```


## 默认构造函数

## 拷贝构造函数

有指针类型的成员变量需要写拷贝构造函数，否则不写的话，在进行拷贝时，两个指针指向同一块地址，在删除时会删除两次。

```cpp
public:
    String(const char* str = 0);
    String(const String& str); // 拷贝构造
    String& operator=(const String& str); // 拷贝赋值

private:
    char* m_data; // 让字符串动态变化的考虑
```

## 拷贝赋值

关键的三个步骤

1. 把原来的清空 (**易忘**)
2. 分配一个同样大的空间，和要赋值的内容
3. 拷贝

```cpp
s2 = s1; // s1作用在s2上

String& String::operator=(const String& str)
{
    if(this == &str) return *this; // 检测自我赋值，注意

    delete[] m_data; // 1
    m_data = new char[strlen(str.m_data) + 1];
    strcpy(m_data, str.m_data);

    return *this;
}
```

## 类型转换构造函数 

`explicit`

non-explicit-one-argument ctor

[侯捷-Explicit for ctors taking more than one arguments](https://www.bilibili.com/video/av51863195/?p=7)


在只接收一个**实参**时的构造函数，默认会隐式创建临时对象，进行类型转换

```cpp
Fraction(int num, int den = 1) ...
Fraction operator+(const Fraction& f) { ... }

Fraction f(3,5);
Fraction d2 = f + 4; // 会调用non-explict ctor,将4转换为Faction(4,1);
```

```cpp
Fraction(int num, int den = 1) {...} // 4转换为faction

operator double() const { ... } // fraction转为double
Fraction operator+(const Fraction& f) { ... }

Fraction f(3,5);
Fraction d2 = f + 4; // Error ambiguous
```

解决上错误可以添加`explicit`,是的只有fraction转换为double可以




## 单例模式

把构造函数放到`private`

```cpp
class A 
{
public:
    static A& getInstance();
    setup() { ... };
private:
    A();
    A(const A& rhs);
    ...
}

A& A::getInstance()
{
    static A a;
    return a;
}
```