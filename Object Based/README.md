# 设计一个类时需要注意的地方

## 类内(没有指针类型的成员变量)

1. 构造函数要使用**初始化列表**
2. 参数尽可能以**引用**来传递，`const`需要看情况
3. 函数名后是否要加`const`,常量成员函数
4. 返回值要考虑return by value(返回值是local object，即栈变量)或者return by reference
5. 数据尽可能放在`private`区里,函数放`public`区
6. 操作符重载的方式，成员函数 ? 非成员函数 ? 链式使用时使用非成员函数

## 类外

1. 什么情况可以pass by reference
2. 什么情况可以return by reference

---

## 类内(有指针类型的成员变量)

