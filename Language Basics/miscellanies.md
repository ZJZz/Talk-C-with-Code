# 语言基础杂记

## 声明和定义

**声明**：告诉编译器函数和变量的名字在其他地方，它们长这个样子。

一旦声明了变量和函数，编译器就可以检查它们是否被正确使用。

**定义**：在这里创建这个函数或变量。

C++/C可以在多个地方声明变量或函数，但只允许有一处声明。

一个声明也可以是一个定义。

## extern

功能：

- 这个函数或变量只是一个声明，定义在别的地方(external linkage, 可以被当前文件以外的访问到)
- 当一个变量声明为`extern`后，它的声明周期和`static`相同

## void *

可以接受任何类型的指针

```cpp
void *vp;
char c;
int i;

// The address of ANY type can be assigned to a void pointer:
vp = &c;
vp = &i;
```

但是在解引用前必须声明类型

```cpp
int i = 99;
void *vp = &i;

// CANNOT dereference a void pointer:
// *vp = 3; // Compile-time error
// MUST cast back to int before dereferencing:
*((int*)vp) = 3; // OK
```


只能在C中赋给其它类型的指针

```cpp
int i = 10;
void* vp = &i; // OK in both C and C++
int* ip = vp; // ONLY acceptable in C
```

没有空引用

## linkage

描述了一个标识符（变量或函数）能或不能在整个程序中被引用

翻译单元：源代码文件 + 所有`#include`的头文件，编译器将要编译成一个obj文件的

### 内部linkage

一块内存空间只在一个翻译单元内部使用，其它翻译单元可以有重名，但相互独立

### 外部linkage

一块内存空间创建后可以被其它翻译单元使用，可以用`extern`关键字声明


而 #include 的作用基本可以理解为 “copy the included file into the current one”。在实际应用中，要注意区分 #include 和 declare。举个例子：

- 如果我在 lib.h 写了 const int STASH_NUM = 8;，这是个 internal linkage
- 我在 main.cpp 里用 extern const int STASH_NUM; 是无法 declare 到这个 const int，使用时会报 “undefined reference”
    - 因为 lib.h 和 main.cpp 是两个不同的 translation units，因为 internal linkage，所以 main.cpp 看不到 lib.h 里的 const int STASH_NUM = 8;
- 如果我在 main.cpp 里写的是 #include 'lib.h'，这时 main.cpp 和 lib.h 是同一个 translation unit。而同一个 translation unit 是可以看到 const int STASH_NUM = 8; 的，所以 main.cpp 可以直接用 STASH_NUM，此时也不需要写 extern const int STASH_NUM;（因为没必要；但是写了也不会报错）


## 变量的作用域

### 函数参数中的

形式参数

### 代码块或函数中

局部变量

### 所有函数之外的

全局变量，有static duration或外部linkage

## static

### file scope

当声明一个变量或函数为`static`时，这个函数和变量就具有了内部linkage

在函数之外声明的名字可以被任意地方的翻译单元访问，

## 变量的存储类型

## auto

自动创建和删除，所有局部变量的存储类型默认是`auto`

## register

建议把变量存储在寄存器而不是内存，所以没有地址

## static

常见用法

- 声明一个变量或者函数的文件作用域，只能在当前文件被访问到，有了内部linkage,一个静态变量有了static duration,并且默认初值为0

- 当在一个函数中声明了static变量，说明这个变量在函数调用期间保持状态

- 当一个成员变量声明为static,那么这个变量的一个拷贝被这个类的所有实例共享

    - 所有静态成员变量必须在文件作用域内定义

- 当一个成员函数被声明为static,说明这个函数被这个类的所有实例共享
    - 一个静态成员函数不能范围实例变量，因为没有this指针
    - 为了访问一个实例的变量，在函数的参数中定义一个实例的指针或引用

## 变量的类型修饰符

### const

告诉编译器，不会改变，编译器会做一些优化

#define的缺点：1，没有类型检查 2，不能取地址 3. 不能是一个自定义类型的常量 4. 

C++中，const变量默认是内部linkage, C中相反。

extern可使const 变量的linkage变为外部linkage

### volatile

告诉编译器，并不知道什么时候会改变，变化的情况超出了编译器的知识

volatile变量总是在变量要求读时就读，因为可能被其它线程或进程改变

