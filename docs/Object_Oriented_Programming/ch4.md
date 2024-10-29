# ch4 基础语法（3）

## 1. 继承

在已有类的基础上，可以通过**继承**来定义新的类，实现对已有代码的复用。常见的继承方式如下：

```cpp
class Derived : Base { .. };			// 默认继承方式为 private
class Derived : private Base { .. };
class Derived : public Base { .. };
```

被继承的已有类，称为**基类**（$\tt base\ class$），也称**父类**。通过继承得到的新类，称为**派生类**（$\tt derived\ class$），也称**子类**、**扩展类**。

基类的数据成员，通过继承成为派生类对象的一部分，需要在构造派生类对象的过程中调用基类构造函数来正确初始化。若没有显式调用，则编译器会自动生成一个对基类的默认构造函数的调用。若想要显式调用，则只能在派生类构造函数的初始化成员列表中进行，既可以调用基类中不带参数的默认构造函数，也可以调用合适的带参数的其他构造函数。

先执行基类的构造函数来初始化继承来的数据，再执行派生类的构造函数。对象析构时，先执行派生类析构函数，再执行由编译器自动调用的基类的析构函数。

在派生类中使用 `using Base::Base;` 来继承基类构造函数，相当于给派生类 “定义” 了相应参数的构造函数，如：

```cpp
#include <iostream>
using namespace std;
class Base {
    int data;
public:
    Base(int i) : data(i) {
        cout << "Base::Base(" << i << ")\n";
    }
};

class Derive : public Base {
    int data{2024};
public:
    using Base::Base;
    void print() {
        cout << "data=" << data << endl;
    }
};

int main() {
    Derive obj(365);
    obj.print();
    
    return 0;
}

/*
Base::Base(365)
data=2024
*/
```

虽然基类构造函数的参数默认值不会被派生类继承，但由默认参数导致的多个构造函数版本都会被派生类继承。如果基类的某个构造函数被声明为私有成员函数，则不能在派生类中声明继承该构造函数。如果派生类使用了继承基类构造函数，编译器就不会再为派生类生成默认构造函数。

## 2. 函数重写

派生类对象包含从基类继承来的数据成员，它们构成了**基类子对象**。基类中的私有成员，不允许在派生类成员函数中被访问，也不允许派生类的对象访问它们，真正体现**基类私有**。

对于基类中的公有成员，若是使用 `public` 继承方式，则成为派生类的公有成员；若是使用 `private` 继承方式，则只能供派生类成员函数访问，不能被派生类的对象访问。

基类已定义的成员函数，在派生类中可以重新定义它，称为**函数重写**（$\tt override$）。重写发生时，基类中该成员函数的其他重载函数都将被屏蔽掉，不能提供给派生类对象使用。可以在派生类中通过 `using Base::function;` “恢复” 指定的基类成员函数（即去掉屏蔽）。

```cpp
#include <iostream>
using namespace std;

class T {};

class B {
public:
    void f() { cout << "B::f()\n"; }
    void f(int i) { cout << "B::f(" << i << ")\n"; }
    void f(double d) { cout << "B::f(" << d << ")\n"; }
    void f(T) { cout << "B::f(T)\n"; }
};

class D1 : public B {
public:
    // using B::f;		// 使用 using 恢复基类函数
    void f(int i) { cout << "D1::f(" << i << ")\n"; }
};

int main() {
    D1 d;
    d.f(10);
    d.f(4.9);			// WARNING，执行自动类型转换，去掉第 16 行代码的注释，则正常执行
    // d.f();			// ERROR，被屏蔽，去掉第 16 行代码的注释，则正常执行
    // d.f(T());		// ERROR，被屏蔽，去掉第 16 行代码的注释，则正常执行
    
    return 0;
}

/*
D1::f(10)
D1::f(4)

去掉第 16 行代码的注释后的输出：
D1::f(10)
B::f(4.9)
B::f()
B::f(T)
*/
```

## 3. 虚函数

派生类对象转换成基类对象，称为**向上映射**，基类对象转换成派生类对象，称为**向下映射**。向上映射可以由编译器**自动完成**，是一种**隐式的自动类型转换**。凡是接受基类对象的地方，都可以使用派生类对象，编译器会自动将派生类对象转换为基类对象以便使用。

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    void print() { cout << "Base::print()\n"; }
};

class Derive : public Base {
public:
	void print() { cout << "Derive::print()\n"; }
};

void fun(Base obj) {
	obj.print();
}

int main() {
    Derive d;
    d.print();		// 输出 Derive::print()
    fun(d);			// 输出 Base::print()

	return 0;
}
```

对于被派生类重写的成员函数，若它在基类中被声明为虚函数，则**通过基类指针或引用**调用该成员函数时，编译器将**根据所指（或引用）对象的实际类型**决定是调用基类中的函数，还是调用派生类重写的函数。若某成员函数在基类中声明为虚函数，当派生类重写它时，无论是否声明为虚函数，该成员函数都仍然是虚函数。

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual void print() { cout << "Base::print()\n"; }
};

class Derive : public Base {
public:
	void print() { cout << "Derive::print()\n"; }
};

void fun(Base& obj) {	// obj 是 Base 类对象的引用
	obj.print();
}

int main() {
    Derive d;
    d.print();			// 输出 Derive::print()
    fun(d);				// 输出 Derive::print()
    
    Base b;
    fun(b);				// 输出 Base::print()

	return 0;
}
```

```cpp
// 虚析构函数示例
#include <iostream>
using namespace std;

class Base {
public:
    virtual void print() { cout << "Base::print()\n"; }
	virtual ~Base() { cout << "~Base()\n"; }
};

class Derive : public Base {
public:
	void print() { cout << "Derive::print()\n"; }
	~Derive() { cout << "~Derive()\n"; }
};

void fun(Base* obj) {
	obj->print();
}

int main() {
    Base* b = new Derive;
    fun(b);
	delete b;

	return 0;
}

/*
运行结果为：
Derive::print()
~Derive()
~Base()

若删除析构函数前面的 virtual，则运行结果为：
Derive::print()
~Base()
*/
```

使用 `final` 关键字修饰的虚函数，派生类不可对它进行重写 —— 改变函数定义（行为）。在派生过程中，`final` 可以在继承关系链的 “中途” 进行设定，禁止后续派生类对指定虚函数重写。

```cpp
class A {
public:
    virtual void fun() = 0;	// 表明这是一个纯虚函数
    // 包含了纯虚函数的类不允许定义对象，主要用于规定接口，通常称为接口类，或抽象类
};

class B : public A {
public:
    void fun() final;		// 到此为止，后续子类不可重写此接口函数
};

class C : public B {
public:
    // void fun();			// ERROR，不可重写
}
```

## 4. 自动类型转换

```cpp
#include <iostream>
using namespace std;

class Dst {
public:
    Dst() {
        cout << "Dst::Dst()\n";
    }
    // 方法一：在目标类中定义【源类对象作参数的构造函数】
    Dst(const Src& s) {
        cout << "Dst::Dst(const Src&) called\n";
    }
};

class Src {
public:
    Src() {
        cout << "Src::Src()\n";
    }
    // 方法二：在源类中定义【目标类型转换运算符】
    operator Dst() const {
        cout << "Src::operator Dst() called\n";
        return Dst();
    }
};

// 测试代码，注意两种方法不可同时使用
void func(Dst d) { }

int main() {
	Src s;
	Dst d1(s);		// 直接构造

	Dst d2 = s;		// 自动类型转换
	func(s);		// 自动类型转换

	return 0;
}
```

## 5. 禁止自动类型转换

```cpp
#include <iostream>
using namespace std;

class Src;
class Dst {
public:
    Dst() {
        cout << "Dst::Dst()\n";
    }
    
    explicit	// 方法一：不准用于自动类型转换，仅用于构造函数
    Dst(const Src& s) {
        cout << "Dst::Dst(const Src&) called\n";
    }
};

class Src {
public:
    Src() {
        cout << "Src::Src()\n";
    }
    
    explicit	// 方法二：不准用于自动类型转换
    operator Dst() const {
        cout << "Src::operator Dst() called\n";
        return Dst();
    }
};

// 测试代码
void func(Dst d) { }

int main() {
	Src s;
	Dst d1(s);			// 直接构造

	// Dst d2 = s;		// ERROR，禁止自动类型转换
	// func(s);			// ERROR，禁止自动类型转换
    // 因为两处都禁止自动类型转换，因此以上代码无法编译
    // 可以取消任意一处的 explicit 声明来解决此问题

	return 0;
}
```

使用 `= delete` 修饰的成员函数，不允许被调用。可以使用 `= delete` 删除普通函数（非成员函数），可以消除一些自动类型转换带来的隐患。

```cpp
#include <iostream>
using namespace std;

class T {
public:
    T(int) { 
		cout << "T::T(int) called\n";
	}
    // 若无下面这条语句，则 main 函数中所有语句均可以通过编译
    T(char) = delete;	// 该函数禁止调用，可消除自动转换带来的隐患
};

void fun(T t) { 
	cout << "fun(T) called\n";
}

void fun(int i) { 
	cout << "fun(int) called\n";
}

void fun(char c) = delete;

int main() {
    fun(1);
	// fun('X');		// ERROR，自动类型转换失败
    
    T ci(1);
	// T cc('X');		// ERROR，自动类型转换失败

	return 0;
}
```

## 6. 强制类型转换

- `dynamic_cast<Dst_Type>(Src_var)`

    `Src_var` 必须是引用或指针类型，`Dst_type` 类中含有虚函数，否则会有编译错误。若目标类与源类之间没有继承关系，则转换失败，返回空指针，注意并不是运行崩溃。

- `static_cast<Dst_Type>(Src_var)`

    基类对象不能转换成派生类对象，但基类指针可以转换成派生类指针。派生类对象或指针可以转换成基类对象或指针。没有继承关系的类之间，必须具有转换途径才能进行转换，要么自定义，要么是语言语法支持。

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual void func() { }
};

class Derive : public Base { };

class E { };

int main() {
    Derive d1;
	Base b1;

	// d1 = static_cast<Derive>(b1);	// ERROR，从基类无法转换回派生类
	b1 = static_cast<Base>(d1);			// OK，从派生类可以转换回基类
	// b1 = dynamic_cast<Base>(d1);		// ERROR，被转换的必须是引用或指针

	Base* pb1 = new Base();
	Derive* pd1 = static_cast<Derive*>(pb1);
	if (pd1)
		cout << "static_cast Base* to Derive* done.\n";
	pd1 = dynamic_cast<Derive*>(pb1);
	if (pd1)
		cout << "dynamic_cast Base* to Derive* done.\n";
	
	Derive* pd2 = new Derive();
	Base* pb2 = static_cast<Base*>(pd2);
	if (pb2)
		cout << "static_cast Derive* to Base* done.\n";
	pb2 = dynamic_cast<Derive*>(pd2);
	if (pb2)
		cout << "dynamic_cast Derive* to Base* done.\n";

	E* pe = dynamic_cast<E*>(pb1);
	if (!pe) 
		cout << "dynamic_cast Derive* to Base* failed.\n";
    
    // pe = static_cast<E*>(pb1);		// ERROR，没有继承关系不能转换
    // E e = static_cast<E>(b1);		// ERROR，没有提供转换途径

	return 0;
}
```

## 7. 函数模板

有些算法实现与类型无关，所以可以将函数的参数类型也定义为一种特殊的 “参数”，这样就得到了**函数模板**。例如任意类型两个变量相加的函数模板：

```cpp
template <typename T>
T sum(T a, T b) { return a + b; }

// 函数模板也可以有默认值
template <typename T0 = float,
		  typename T1,
		  typename T2 = float,
		  typename T3,
		  typename T4>
T0 func(T1 v1, T2 v2, T3 v3, T4 v4) { /* ... */ }
// ...
func(1, 2, 3);
func('a', 'b', "cde");
```

## 8. 类模板

在定义类时也可以将一些类型信息抽取出来，用模板参数来替换，从而使类更具有通用性，称为**类模板**。

```cpp
template <typename T> 
class A {
    T data;
public:
    // 类模板成员函数的定义方式一：在类模板中定义
    void print() {
        cout << data << endl;
    }
};

// 类模板成员函数的定义方式二：在类模板外定义
template <typename T>
void A::print() {
    cout << data << endl;
}
```

类模板的模板参数：

- 类型参数：使用 `typename` 或 `class` 标记

- 非类型参数：整数、枚举、指针、引用。如

    ```cpp
    template <typename T, unsigned size>
    class array {
        T elems[size];
        // ...
    };
    
    array<char, 10> array0;		// 用类模板实例定义对象
    ```

- 模板参数是另一个类模板，如

    ```cpp
    template <typename T,
    template <typename TT0, typename TT1> class A>
    struct Foo {
        A<T, T> bar;
    };
    ```

## 9. 成员函数模板

```cpp
// 普通成员函数模板
class normal_class {
public:
    int value;
    
    // 在类内定义
    template <typename T> void set(T const& v) {
        value = int(v);
    }
    
    template <typename T> T get();
};

// 在类外定义
template <typename T> 
T normal_class::get() {
    return T(value);
}

// 类模板成员函数模板
template <typename T0>
class A {
public:
    T0 value;
    
    // 在类内定义
    template <typename T1> void set(T1 const& v) {
        value = T0(v);
    }
    
    template <typename T1> T1 get();
}

// 在类外定义
template <typename T0> template <typename T1> 
T1 A::get() {
    return T1(value);
}
```

## 10. 模板特化

当有些类型不适用模板时，需要对模板进行特殊化处理，称为**模板特化**。

对函数模板，如果有多个模板参数，则特化时必须提供所有参数的特例类型，**不能部分特化**。

```cpp
// 特化函数 char* sum(char*, char*);

// 方法一：在函数名后用 <> 括起具体类型
template<>
char* sum<char*>(char* a, char* b) { /* .. */ }

// 方法二：由编译器推导出具体类型，函数名为普通形式
template<>
char* sum(char* a, char* b) { /* .. */ }
```

```cpp
// 函数模板特化示例
#include <iostream>
#include <cstring>
using namespace std;

template <typename T>
T sum(T a, T b) {
	return a + b;
}

template <>
char* sum(char* a, char* b) {
	char *p = new char[strlen(a) + strlen(b) + 1];
	strcpy(p, a);
	strcat(p, b);

	return p;
}

int main() {
    cout << sum(3, 4) << endl;				// 输出 7
	cout << sum(5.1, 3.14) << endl;			// 输出 8.24

	char *s1 = "Hello, ", *s2 = "world.";	// 输出 Hello, world.
	cout << sum(s1, s2) << endl;

	return 0;
}
```

对类模板，允许部分特化，即部分限制模板的通用性。

```cpp
// 通用模板类
template<class T1, class T2> class A { /* .. */ }

// 部分特化的模板类：第 2 个类型参数指定为 int
template<class T1> class A<T1, int> { /* .. */ }

// 若指定所有类型，则 template 后面的 <> 中留空
template<> class A<int, int> { /* .. */ }
```

```cpp
// 类模板特化示例
#include <iostream>
#include <cstring>
using namespace std;

template <typename T>
class Sum {
	T a, b;
public:
	Sum(T op1, T op2) : a(op1), b(op2) { }
	T DoIt() { return a + b; }
};

template <>
class Sum<char*> {
	char *str1, *str2;
public:
	Sum(char* s1, char* s2) : str1(s1), str2(s2) { }
	char* DoIt() {
		char *tmp = new char[strlen(str1) + strlen(str2) + 1];
		strcpy(tmp, str1);
		strcat(tmp, str2);

		return tmp;
	}
};

int main() {
    Sum<int> a(3, 4);
	cout << a.DoIt() << endl;				// 输出 7

	char *s1 = "Hello, ", *s2 = "world.";
	Sum<char*> b(s1, s2);
	cout << b.DoIt() << endl;				// 输出 Hello, world.

	return 0;
}
```