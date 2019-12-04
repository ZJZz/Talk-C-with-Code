# 虚函数搭配继承

## 虚函数

有默认定义，希望子类override

## 纯虚函数

无默认定义，子类一定要override

## 非虚函数

不希望子类override

## 继承和符合搭配时的构造，析构

### derieved拥有Component时

构造：Base, Component, Derieved
析构：Derieved, Component, Base

### Base拥有Component

构造: Component, Base, Derieved
析构: Derieved, Base, Component

## vptr vtbl

vptr指向vtbl

vtbl里存放函数指针，指向虚函数存在的位置

```cpp
class A
{
public:
    virtual void vfunc1();
    virtual void vfunc2();
    void func1();
    void func2();
private:
    int m_data1, m_data2;
};

class B: public A
{
public:
    virtual void vfunc1();
    void func2();
private:
    int m_data3;
};

class C: public B
{
public:
    virtual void vfunc1();
    void func2();
private:
    int m_data1, m_data4;
};
```


## 动态绑定

触发条件: ①对象指针 ②向上转型 `茶叶 *t= new 红茶();` ③ 调用虚函数


```c
pa->vfunc1();

// 底层过程

(p->vptr) // 找到vptr
(p->vptr)[n] // 找到虚表中的函数指针
(*(p->vptr)[n]) // 当成函数 

(*(p->vptr)[n])(p) // 函数调用，参数就是p
```


## 静态绑定(函数重载)

调用者为对象时，不会进行动态绑定

## 虚函数的常见用法

多态: 容器中放基类的指针，调用时不同类型调用不同的方法

模板方法(设计模式),如下

A部门的任务

```cpp
class CDocument
- OnFileOpen()
- Serialize()
```


B部门的任务

```cpp
class CMyDoc
- Serialize()
```

现在A部门并不知道`Serialize()`该如何实现，所以把`Serialize()`设为虚函数

```cpp
CDocument::OnFileOpen() // 成员函数都有一个隐藏的this指针
{
    // 2
    ...

    // 3
    Serialize(); // 实际是 this->Serialize();而this指向子类CMyDoc,所以会去子类中

    // 5
    ...
}

virtual Serialize();
```

B部门实现

```cpp
class CMyDoc: public CDocument
{
    // 4
    virtual Serialize() { ... }
};
```

主函数调用,运行走向用数字做出了注释

```cpp
main()
{
    CMyDoc myDoc;
    
    // 1
    myDoc.OnFileOpen(); // 此时myDoc为this指针，子类对象调用父类函数

    // 6
}
```

