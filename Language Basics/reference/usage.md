函数传参时，pass-by-reference 并没有 copy 参数

引用是一种漂亮的指针，多用在**参数处理**和**返回类型上**,使用引用时，被调用端的写法相同

``` cpp
void func1(cls* pobj) { pobj->xxx(); }
void func2(cls obj)   { obj->xxx(); } // 写法相同
void func3(cls& obj)  { obj->xxx(); } // 写法相同

cls obj;

func1(&obj);
func2(obj); //
func3(obj); // 调用端接口相同
```

注意：

```cpp
double imag(const double& im) {}
double imag(const double  im) {} 
```

上面两个函数被视为相同的signature,二者不能同时存在


