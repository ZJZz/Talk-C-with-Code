# 复合

表示has-a的关系

复合关系下的构造与析构调用顺序

```cpp
class Container
{
    Component comp;
}
```

构造由内而外，首先调用Component的默认构造函数，再执行自己的构造函数

析构由外而内

```cpp
Container::~Container() { ... ~Component();};
```