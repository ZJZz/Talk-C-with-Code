# 函数模板

```cpp
template<typename T>
inline const T& min(const T& a, const T& b)
{
    return a < b ? a : b;
}
```

使用过程

```cpp
class stone
{
public:
    stone(int w, int h, int we):_w(w), _h(h), _we(we) {}
    bool operator<(const stone& rhs) const
    {
        return _weight < rhs._weight;
    }
private:
    int _w, _h, _weight;
}

{
    stone r1(2,3), r2(3,3), r3;
    r3 = min(r1, r2);
}
```

在运行到`min()`时，会调用定义好的函数模板，在函数模板内运行到`a<b`时，会调用`stone`类里的操作符重载函数

