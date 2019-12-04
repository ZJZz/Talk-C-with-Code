# 左值和右值

[侯捷-Rvalue references and move semantics](https://www.bilibili.com/video/av51863195/?p=23)

## 左值

可以出现在`=`左侧的值

当一个对象被用作左值的时候，用的是对象的身份(在内存中的位置)

左值持久存在，变量

## 右值

只能出现在`=`右侧的值

右值短暂存在，函数返回值，字面值常量，表达式求值过程中创建的临时对象。

```cpp
int a = 9;
int b = 4;

a = b;
b = a;
a = a + b;

a + b = 42; // 错误，a + b的结果为右值
```

```cpp
int foo() { return 5; }
int x = foo();
int * p = &foo(); // 函数返回值为右值，右值不可以取地址， &foo才是取函数地址
foo() = 7; // 错误
```
