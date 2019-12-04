# 操作符重载

## 作为成员函数

有`this`指针

用处：比如可以实现+=

```cpp
c2 += c1

const operator+=(this, const complex& r)
```

## 作为非成员函数

无`this`指针

```cpp

int(7);

complex c1(2,1);
complex c2;
complex();
complex(4,5);

cout << complex(2);

inline complex operator+(const complex& x, const complex& y) {}

...
```

因为它们返回的值必定是个local object,函数里被创建出来，所以必须以值的方式返回