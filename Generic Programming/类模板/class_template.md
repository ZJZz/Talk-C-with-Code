# 类模板

允许使用者指定类中成员变量为任意类型,例如下面complex类，它的成员变量`re`和`im`可以为任意类型

```cpp
template<typename T>
class complex
{
public:
    complex(T r = 0, T i = 0):re(r), im(i) {}
    complex& operator+=(const complex&);
    T real() { return re; }
    T img() { return im; }

private:
    T re, im;
};

{
    complex<double> c1(2.5, 1.5);
    complex<int> c2(2,6);
}
```
