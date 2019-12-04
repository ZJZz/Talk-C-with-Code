# 常量成员函数

```cpp
double real() const { return re; } 
double imag() const { return im; } // 这两个函数都没有改变数据内容
```

如果不加`const`会有什么问题?

```cpp
const complex c1(2,1);

cout << c1.real(); // 调用出问题，因为const对象只能调用const成员函数
cout << c1.imag();
```
