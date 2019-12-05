# 成员模板

类中的成员函数是模板，增加了更多的灵活性

下面是构造函数为函数模板的例子

```cpp
template<class T1, class T2>
struct pair
{
    typedef T1 first_type;
    typedef T2 second_type;

    T1 first;
    T2 second;

    pair():first( T1() ), second( T2() ) {}
    pair(const T1& a, const T2& b):first(a), second(b) {}

    // 把p的first,second放进来，当做本身的first, second
    template<class U1, class U2>
    pair(const pair<U1, u2>& p):first(p.first), second(p.second) {}
}
```

上面有四个地方可以定义类型`T1,T2`和`U1,U2`,意思是当类外`T1,T2`确定后，里面的模板`U1,U2`也可以变化

下面是一个有继承关系的例子

```cpp
class Base1 {}; // 鱼
class Derieved1 {}; // 鲫鱼

class Base2 {}; // 鸟
class Derieved2 {}; // 麻雀

pair<Derieved1, Derieved2> p;
pair<Base1, Base2> p2(p);

pair<Base1, Base2> p2(pair<Derieved1, Derieved2>()); // 构造函数
```

把一个由`(鲫鱼， 麻雀)`构成的pair放进(拷贝到)一个由`(鱼， 鸟)`构成的pair中，可以。反过来不可以。

