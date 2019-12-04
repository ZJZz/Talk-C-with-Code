传递者无需知道接受者是否以reference形式接收

```cpp

inline complex& __doapl(complex *this, const complex& r) // 返回值complex&为接受者
{
    ...
    return *this; // 传递者
}


inline complex& complex::operator+=(const complex& r)
{
    return __doapl(this, r);
}

```

返回值类型为`complex&`支持这种写法就可以写出`c3 += c2 += c1;`，如果返回值为`void`就不可以。