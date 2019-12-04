# 继承

表示是一种的关系

父类的**数据**是被完整继承下来，**函数**只是继承调用权

```cpp

class Base
{

}

class Derived: public Base
{

}
```

构造顺序，由内而外
析构顺序，有外而内， base class的析构须是`virtual`


[Difference between private, public, and protected inheritance](https://stackoverflow.com/questions/860339/difference-between-private-public-and-protected-inheritance/1372858#1372858)


[Why do we actually need Private or Protected inheritance in C++?](https://stackoverflow.com/questions/374399/why-do-we-actually-need-private-or-protected-inheritance-in-c/374423#374423)

