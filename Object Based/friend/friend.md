# 友元

```cpp
class
{

private:
    friend complex& __decopl(...) // 友元函数
}
```

相同class的各个object互为友元

```cpp
class Complex
{

public:
    complex(double r = 0, double i = 0):re(r), im(i) {}
    int func(const complex& param)
    { return param.re + param.im; }

private:
    double re,im;

}

{
    complex c1(2,1);
    complex c2;
    c2.func(c1);
}
```