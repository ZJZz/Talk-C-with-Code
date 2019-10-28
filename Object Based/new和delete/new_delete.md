# new / delete

## new

```cpp
Complex* pc = new Complex(1,2);
```

new分解为以下语句
```cpp
Complex *pc;
void *mem = operator new(sizeof(Complex)); // 调用malloc, 分配内存
pc = static_cast<Complex *>(mem); // 转型
pc->Complex::Complex(1,2); // 调用构造函数  
```

所以`new`先分配内存，再调用构造函数

## delete

```cpp
delete ps;
```

delete分解为以下语句

```cpp
String::~String(ps); // 调用析构函数
operator delete(ps); // 调用free，释放内存
```

所以`delete`先调用析构函数，再释放内存

## new []

## delete []