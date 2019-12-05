# 模板偏特化

## 模板参数个数

只绑定模板参数中的一个

```cpp
template<typename T, typename Alloc=...> // 两个模板参数
class vector
{
    ...
};

// 现在绑定其中一个

template<typename Alloc=...>
class vector<bool, Alloc> // 为bool类型单独设计
{
    ...
};
```

## 模板类型范围

对指针类型进行特化

```cpp
template <typename T> // 1
class C
{
    ...
};

template <typename T> // 2 这里T换成U也可以
class C<T*>
{
    ...
};

{
    C<string> obj1;   // 调用1
    C<string *> obj2; // 调用2
}
```