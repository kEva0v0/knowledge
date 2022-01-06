# 多态、多重继承

嘛，快忘了，赶紧记录一下啦

> 参考资料《On Understanding Types, Data Abstraction, and Polymorphism》，下简称《Understand》

## 如何理解多态

**多态的概念**：同种代码，依据输入不同表现不同行为

**多态的作用**：接口与实现隔离

《Understand》一文中提到有两种主要类型：

- universal polymorphism

  - parametric polymorphism: 类型多态，可以理解为泛型T

  - inclusion polymorphism: 继承多态，一个类可以继承自不同的抽象接口

- ad-hoc polymorphism 特设多态

  - overloading: 重载

  - coercion: 抽象接口

## 多态的实现

### C++ 多态

- 泛型
```
template <typename T>
T max(T a, T b)
{
   return a > b ? a : b;
}

cout << max(1, 2) << endl;
cout << max(1.0, 2.0) << endl;
```
这是一个C++中非常典型的泛性编程思路，它依靠的是静态多态实现，即编译时，编译器会根据调用max的地方生成不同而生成不同的模版代码，例如：
```
template <>
int max(int a, int b)
{
   return a > b ? a : b;
}

template <>
double max(double a, double b)
{
   return a > b ? a : b;
}
```
这两个max函数具有不同的地址

- 虚函数
虚函数代表的是C++的动态多态实现方式，在类中以virtual关键词体现

```
class Parent {
    public:
        virtual void print(){ 
            cout << "This is Parent" << endl;
        }
        void haha() {
            return;
        }
}

class Child: public Parent {
    public:
        virtual void print(){ 
            cout << "This is Child" << endl;
        }
}

int main() {
    Child child1;
    child1.print();
    return 0;
}

```

通过维护一个vtable(虚函数表)来实现函数访问
比如上面这个例子,child1在内存中的vtable应该是：

Child::print() | Parent::haha()

发生了覆盖