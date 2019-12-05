# 模板特化

对某些独特的类型，要做特殊的设计

```cpp
template<class Key>
struct hash{};

template<> // 此时Key已经被绑定了，无需再写
struct hash<char> // Key被绑定到了这里
{
    size_t operator()(char x) const { return x; }
};

template<>
struct hash<int>
{
    size_t operator()(int x) const { return x; }
};

template<>
struct hash<long>
{
    size_t operaotr()(long x) const { return x; }
}
```