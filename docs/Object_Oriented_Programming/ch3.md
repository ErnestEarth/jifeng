# ch3 基础语法（2）

## 1. 构造函数

类的构造函数由编译器自动生成调用语句，用于对象数据成员的初始化，以及其它初始化工作。构造函数没有返回值类型，函数名与类名相同。类的构造函数可以重载，即可以使用不同的函数参数进行对象初始化。

```cpp
class Student {
    int ID;
public:
    Student(int id) {
        ID = id;
    }
    Student (int year, int order) {
        ID = year * 10000 + order;
    }
    // ...
};
```

**默认构造函数**：不带任何参数的构造函数，称为**默认构造函数**，也称**缺省构造函数**。在定义元素为对象的数组时，类必须提供默认构造函数的定义。使用默认构造函数来生成对象时，对象定义的格式为 `ClassName obj;`，不能写成 `ClassName obj();`。

构造函数可以使用初始化列表来初始化数据成员，该列表在定义构造函数时使用，位置出现在函数题左花括号之前、函数参数列表圆括号之后，以冒号作为开头。

```cpp
class Student {
    int ID;
public:
    Student(int id) : ID(id) { }
    // ...
};
```

**委派构造函数**：在构造函数的初始化列表中，还可以调用其它构造函数，称为**委派构造函数**。

```cpp
class info {
public:
    Info() { Init(); }
    Info(int i) : Info() { id = i; }
    Info(char c) : Info() { gender = c; }
private:
    void Init() { /* ... */ }		// 其它初始化
    int id { 2024 };
    char gender { 'M' };
    // ...
};
```

**拷贝构造函数**：函数调用时以类的对象为形参或返回类对象时，编译器会生成自动调用**拷贝构造函数**，在已有对象基础上生成新对象。拷贝构造函数是一种特殊的构造函数，它的参数是语言规定的，是**同类对象**的常量引用。语义上表示用参数对象的内容初始化当前对象。

```cpp
class Person {
    int id;
    // ...
public:
    Person(const Person& src) { 
        id = src.id;
        // ...
    }
    // ...
};
```

**移动构造函数**：用来偷临时变量中的资源。临时变量被编译器设置为常量形式，使用拷贝构造函数无法将资源偷出来。所谓 “偷”，是对原对象的一种改动，违反了常量的限制。基于**右值引用**定义的移动构造函数支持接受临时变量，能偷出临时变量中的资源。

```cpp
class Test {
public:
    int * buf;
    Test() {
        buf = new int(3);
    }
    ~Test() {
        if (buf) delete buf;
    }
    // 拷贝构造函数
    Test(const Test& t) : buf(new int(*t.buf)) { }
    // 移动构造函数
    Test(Test&& t) : buf(t.buf) {
        t.buf = nullptr;
    }
};
```

## 2. 析构函数

一个类只有一个析构函数，名称是 `~类名`，没有返回值，没有参数。编译器在对象生命期结束时自动调用类的析构函数，以便释放对象占用的资源，或其它善后处理。

```cpp
class ClassRoom {
    int num;
    int* ID_list;
public:
    ClassRoom() : num(0), ID_list(0) { }
    // ...
    ~ClassRoom() {						// 析构函数
        if (ID_list) delete[] ID_list;	// 释放内存
    }
};
```

## 3. 运算符重载

**赋值运算符重载**：

```cpp
ClassName& operator= (const ClassName& right) {
    if (this != &right) {	// 避免自己赋值给自己
        // 将 right 对象中的内容复制到当前对象中
    }
    return *this;
};
```

**流运算符重载**：流运算符函数是全局函数，不能作为类的成员函数来定义。在具体的类中，我们需要将这两个函数声明成友元函数。

```cpp
class Test {
    int id;
public:
    Test(int i) : id(i) {  }
    // ...
    friend istream& operator>> (istream& in, Test& dst);
    friend ostream& operator<< (ostream& out, const Test& src);
};

istream& operator>> (istream& in, Test& dst) {
    in >> dst.id;
    return in;
}
ostream& operator<< (ostream& out, const Test& src) {
    out << src.id << endl;
    return out;
}
```

**函数运算符重载**：使对象看上去像是一个函数名。

```cpp
class Test {
public:
    int operator() (int a, int b) {
        return a + b;
    }
};

istream& operator>> (istream& in, Test& dst) {
    in >> dst.id;
    return in;
}

int main() {
    Test sum;
    int s = sum(3, 4);	// sum 看上去像是一个函数，称为 “函数对象”
    cout << s << endl;	// 输出 7
}
```

**下标运算符重载**：如果返回值类型是引用，则数组运算符调用可以出现在等号左边，接受赋值，否则只能出现在右边。

```cpp
char week_name[7][4] = { "mon", "tue", "wed", "thu", "fri", "sat", "sun"};

class WeekTemp {
    int temp[7];
public:
    int& operator[] (const char* name) {	// 字符串做下标
        for (int i = 0; i < 7; i++) {
            if (strcmp(week_name[i], name) == 0)
                return temp[i];
        }
    }
};

int main() {
    WeekTemp beijing;
    beijing["mon"] = -3;
    cout << beijing["mon"] << endl;		// 输出 -3
}
```

**自增自减运算符重载**：通过在函数参数中的哑元参数（`dummy`）来区分前缀与后缀的同名重载。

```cpp
// 前缀
ReturnType operator++ ();
ReturnType operator-- ();

// 后缀
ReturnType operator++ (int dummy);
ReturnType operator-- (int dummy);
```

## 4. 静态成员

在类型前面加上 `static` 修饰的数据成员，是属于类的静态数据成员，也称**类变量**。静态数据成员被该类的所有对象共享，即所有对象中的这个数据域实际上处于同一内存位置。静态数据要在实现文件中初始化。

返回值类型前面加上 `static` 修饰的成员函数，称为静态成员函数，它们**不能**调用非静态成员函数。

类的静态成员既可以通过对象来访问，也可以通过类名来访问。

```cpp
#include <iostream>
using namespace std;

class Test {
    static int count;
public:
    Test() { count++; }
	// Test(const Test& src) {
	// 	count = ++src.count;
	// }
    ~Test() { count--; }
    static int how_many() { return count; }
};

// 通过类名访问静态数据成员
int Test::count = 0;

// 通过对象访问静态成员函数
void print(Test t) {
    cout << t.how_many() << endl;
}

int main() {
	Test t1;
	cout << "Test#: " << Test::how_many() << endl;
    // 调用默认拷贝构造函数，count 的值仍然为 1
	Test t2 = t1;
	cout << "Test#: " << Test::how_many() << endl;
	
    // 调用默认拷贝构造函数，将 t2 拷贝给形参 t，count 的值仍然为 1
	print(t2);		
    // 函数返回后形参 t 调用析构函数，导致 count 的值变为 0
    // 若使用第 8~10 行的拷贝构造函数，那么此时 count 的值为 2，因为 t1 和 t2 还没有析构

	cout << "Test#: " << t1.how_many() << ", " << t2.how_many() << endl;

	return 0;
}

/*
使用默认拷贝构造函数的输出：
Test#: 1
Test#: 1
1
Test#: 0, 0

使用 8~10 行的拷贝构造函数的输出：
Test#: 1
Test#: 2
3
Test#: 2, 2
*/
```

## 5. 常量成员

使用 `const` 修饰的数据成员，称为类的常量数据成员，在对象的整个生命周期里不可更改。常量数据成员只能在构造函数的初始化列表中被设置，不允许在函数体中通过赋值来设置。

若用 `const` 修饰成员函数，则该成员函数在实现时不能修改类的数据成员，即函数体中不能有改变对象状态的语句。

若对象被定义为常量，则它只能调用 `const` 修饰的成员函数，其它普通成员函数不允许调用。

## 6. 对象组合

可以在类中使用其它类来定义数据成员，称为**子对象**。这种包含与被包含的对象间的关系称为**组合**，组合关系可以嵌套。

子对象构造时若需要参数，则应在当前类的构造函数的初始化列表中进行。若使用默认构造函数类构造子对象，则不用做任何处理。

对象的构造与析构次序：

- 先完成子对象构造，再完成当前对象的构造
- 对象析构的次序与构造次序是相反的

```cpp
class C1 {
    int ID;
public:
    C1(int id) : ID(id) { }
    ~C1() { }
};

class C2 {
public:
    C2() { }
    ~C2() { }
};

class C3 {
    int num;
    C1 sub_obj1;
    C2 sub_obj2;
public:
    C3() : sub_obj1(123) { }
    C3(int n) : num(n), sub_obj1(123) { }
    C3(int n, int k) : sub_obj1(k) { 
    	num = n;
    }
    ~C3() { }
};
```

## 7. `default` 修饰符

如果用户没有为类实现以下成员函数，那么编译器会自动生成：

- 默认构造函数：空函数
- 默认析构函数：空函数
- 默认拷贝构造：按 `bit` 位复制对象所占内存的内容
- 默认移动构造：与默认拷贝构造一致
- 赋值运算符重载：与默认拷贝构造一致

**显式缺省**：在默认函数定义或声明加上 `= default`，可显式地指示编译器生成该函数的默认版本。

```cpp
class T {
    int data;
public:
    T() = default;	// 方式一
    T(int i) : data(i) { }
};

T::T() = default;	// 方式二
```