# static描述符

[CSAPP - 链接](https://wdxtub.com/csapp/thin-csapp-4/2016/04/16/)

## 修饰对象

static local object，调用时才创建，生命在作用域结束之后仍然存在，直到程序结束，即调用析构函数

global object在整个程序结束后才结束

## 修饰函数


---

静态成员变量和静态成员函数都脱离了对象

## 修饰成员变量

在class外做定义，??才申请内存

## 修饰成员函数

只用一份

没有`this` pointer,只能处理静态数据

可以通过对象调用，也可以通过类名调用

