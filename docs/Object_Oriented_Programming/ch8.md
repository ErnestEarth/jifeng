# ch8 基于接口组合，应对复杂变化

## 1. 已有资源的组合

使用已有代码的常用方式：**继承**、**组合**、**实例化**。

栈 —— 一种**后进先出**的数据结构。首先用一个常规方法实现一个栈。

```cpp
class MyStack {
private:
    int *m_data;
    int m_top;

public:
    MyStack() : m_top(-1) {
        m_data = new int[MAX_SIZE];		// MAX_SIZE 是一个事先定义好的常量
    }
    
    ~MyStack() {
        delete [] m_data;
    }
    
    bool empty() {
        return m_top < 0;
    }
    
    void push(int i) {
        if (m_top + 1 < MAX_SIZE) {
            m_data[++m_top] = i;
        }
    }
    
    void pop() {
        if (!empty()) --m_top;
    }
    
    int top() {
        if (!empty()) {
            return m_data[m_top];
        }
        else {
            return INT_MIN;				// INT_MIN 是一个标准库中事先定义好的一个常量
        }
    }
};
```

下面使用已有的资源 `vector` 的**组合**来实现一个栈：

```cpp
class VectorStack {
private:
    vector<int> m_data;

public:
    bool empty() {
        return (int)m_data.size() == 0;
    }
    
    void push(int i) {
        m_data.push_pack(i);
    }
    
    void pop() {
        if (!empty()) m_data.pop_back();
    }
    
    int top() {
        if (!empty()) {
            return m_data[m_data.size() - 1];
        }
        else {
            return INT_MIN;
        }
    }
};
```

## 2. 适当引入接口

对于**实现可变**，**使用不变**的类，需要一个统一的接口，以便于用户的使用，换言之，我们可以适当增加接口类。

把 `Stack` 这个概念用于抽象类予以定义，其功能定义表现为类中的纯虚函数。使用抽象类传递参数和调用接口的功能，可以让我们集中注意力到接口应有的功能上，保持接口类的稳定不变，隔离实现的细节。

```cpp
class Stack {
public:
    virtual ~Stack() { }
    
    virtual void push(int i) = 0;
    virtual void pop() = 0;
    virtual int top() = 0;
    virtual bool empty() = 0;
};
```

**继承**接口类，重写所有虚函数，将实现细节的变化封装到实现类中，增加新的实现类达到**实现可变**的目的。

```cpp
class VectorStack : public Stack {
private:
    vector<int> m_data;

public:
    bool empty() {
        return (int)m_data.size() == 0;
    }
    
    void push(int i) {
        m_data.push_pack(i);
    }
    
    void pop() {
        if (!empty()) m_data.pop_back();
    }
    
    int top() {
        if (!empty()) {
            return m_data[m_data.size() - 1];
        }
        else {
            return INT_MIN;
        }
    }
};
```

上面 `VectorStack` 的功能类似于一个转接器，将 `vector` 和 `stack` 实现了转接，通常称为**适配器**，上述程序设计模式称为**适配器模式**。使用组合实现适配，称作**对象 Adapter**。

另一种实现方式是使用**多重继承**来实现，但此方式是否合理尚存争论。使用继承实现适配，称作**类 Adapter**。

所谓**实例化**，就是可以将一些已有的模板直接实例化为具体数据类型即可使用的方式。

## 3. 接口不变时的功能变化

一个指向一段已释放的区域的指针，称为**悬挂指针**。此现象产生的原因是，起初多个指针指向同一个对象，当其中一个指针释放了这个对象时，其余指针就变成了悬挂指针。

原因在于共享着同一个基础对象的指针互相不知道对方的存在，自以为独占对象。我们只需要让这些指针互相知道对方的存在就可以了，不需要知道是谁，只需要知道**有几个**。

可以使用**引用计数**解决这个问题：跟踪基础对象被多少指针所共享，当引用计数为 $0$ 时再真正释放基础对象。

```cpp
#include <iostream>
using namespace std;

template <typename T>
class SmartPtr;				// 声明 “智能指针” 模板类

template <typename T>		// 使用模板，允许指针指向任何类型
class U_Ptr {				// 辅助指针，用于对引用次数进行计数
private:
    friend class SmartPtr<T>;
    
    U_Ptr(T *ptr) : p(ptr), count(1) { }			// 初始计数为 1
    ~U_Ptr() { delete p; }
    
    int count;
    T *p;
};

template <typename T>		// 使用模板，允许指针指向任何类型
class SmartPtr {			// “智能指针”
public:
    SmartPtr(T *ptr) : rp(new U_Ptr<T>(ptr)) { }
    SmartPtr(const SmartPtr<T> &sp) : rp(sp.rp) {	// 先复制
        ++rp->count;		// 拷贝构造函数，引用计数加一
    }
    SmartPtr& operator=(const SmartPtr<T>& rhs) {
        ++rhs.rp->count;	// 将 rhs 的引用计数加一
        if (--rp->count == 0)	// 原来指向对象的引用计数减一
            delete rp;			// 如果引用计数为 0 则释放基础对象
        rp = rhs.rp;		// 执行实际的赋值动作
        return *this;
    }
    ~SmartPtr() {
        if (--rp->count == 0)	// 析构函数，引用计数减一
            delete rp;			// 如果引用计数为 0 则释放基础对象
    }
    T & operator *() {
        return *(rp->p);
    }
    T* operator ->() {
        return rp->p;
    }
private:
    U_Ptr<T> *rp;
};

int main() {
    SmartPtr<int> ptr1(new int(2));
    SmartPtr<int> ptr2(ptr1);
    SmartPtr<int> ptr3 = ptr2;
    cout << *ptr1 << endl;
    *ptr1 = 20;
    cout << *ptr2 << endl;
    
    return 0;
}
```

`SmartPtr<int>` 与 `int*` 有相同的接口：操作符 `*` 和 `->`，赋值操作符与初始化（拷贝构造），释放（析构）。`SmartPtr<int>` 比 `int*` 增加了一些控制操作：拷贝构造时引用计数加一，析构时引用计数减一，直到引用计数为 $0$ 时释放，赋值时对当前引用计数和参数引用计数分别处理。这种**接口不变，功能变化**的模式称为**代理模式**，用于对被代理对象进行控制，如引用计数控制、权限控制、远程代理、延迟初始化（对于初始化时间比较长的操作，实际使用时再初始化，减少初始化次数）等。

## 4. 装饰

将主要功能类与附加功能类分离开，通过在主体上**添加装饰**来实现附加功能，而无需修改主体，称为**装饰模式**。

**装饰**和**策略**都是通过对象的组合修改对象的功能，以组合替代继承，更加灵活。不同点是：

- 策略模式修改了对象功能的内核，组件必须了解有哪些需要选择的策略
- 装饰模式修改了对象功能的外壳，组件无需了解有哪些可以装饰的内容

**装饰**和**代理**都用来改变对象的行为，可以把装饰看成是一连串的代理。不同点是：

- 装饰模式常用来对被装饰对象增加额外的行为，不影响被装饰对象的原有功能，不创建装饰对象，只是将新功能添加到已有对象上，经常多重嵌套装饰
- 代理模式常用来对被代理对象进行更精细的控制，被代理对象不存在时，通常需要创建被代理对象，多重嵌套的情况比较少见

```cpp
#include <iostream>
using namespace std;

class Component {
public:
    virtual ~Component() { }
    virtual void draw() = 0;
};

class TextView : public Component {
public:
    void draw() {
        cout << "TextView." << endl;
    }
};

// 装饰器接口
class Decorator : public Component {
    Component* _component;

public:
    Decorator(Component* component) : _component(component) { }
    virtual void addon() = 0;
    void draw() {
        addon();
        _component->draw();
    }
};

// 不同的装饰器
class Border : public Decorator {
public:
    Border(Component* component) : Decorator(component) { }
    void addon() { cout << "Bordered "; }
};
class HScroll : public Decorator {
public:
    HScroll(Component* component) : Decorator(component) { }
    void addon() { cout << "HScrolled "; }
};
class VScroll : public Decorator {
public:
    VScroll(Component* component) : Decorator(component) { }
    void addon() { cout << "VScrolled "; }
};

int main() {
    TextView textView;
    VScroll vs_TextView(&textView);
    HScroll hs_vs_TextView(&vs_TextView);
    Border b_hs_vs_TextView(&hs_vs_TextView);
    b_hs_vs_TextView.draw();
    
    return 0;
}
```

## 5. 责任传递与责任链

使用链式调用来组织程序行为的方法，称为**责任链**。将一系列的处理者连成一条链，将请求沿着这个链传递并由链上的处理者予以处理。

**责任链**和**装饰**都有调用链。不同点是：

- 责任链更强调**调用链的行为**
- 装饰更强调**调用链带来的组织结果**（组成结构）

也可以把**责任链**看成一连串**代理**。不同点是：

- 代理模式改变对象的行为，控制被代理对象
- 责任链组织多个对象的行为

```cpp
class MailRequest {
    bool _reject;
public:
    string getSender();
    string getTitle();
    string getBody();
    string getAll();
    
    void accept() { _reject = false; }
    void reject() { _reject = true; }
    
    bool isReject() { return _reject; }
};

class Handler {
    Handler *_successor;
public:
    Handler(Handler successor) : _successor(successor) { }
    virtual ~Handler() { }
    
    virtual bool doHandle(MailRequest *request) = 0;
    void handle(MailRequest *request) {
        if (!doHandle(request)) {
            if (_successor != NULL)
                _successor->handle(request);
        }
    }
};

class SenderFilter : public Handler {
public:
    SenderFilter(Handler *successor) : Handler(successor) { }
    
    bool doHandle(MailRequest *request) {
        if (isWhite(request->getSender())) {
            request->accept();
            return true;
        }
        if (isBlack(request->getSender())) {
            request->reject();
            return true;
        }
        return false;
    }
};

class TitleFilter : public Handler {
public:
    TitleFilter(Handler *successor) : Handler(successor) { }
    
    bool doHandle(MailRequest *request) {
        if (!isValid(request->getTitle())) {
            request->reject();
            return true;
        }
        return false;
    }
};

class BodyFilter : public Handler {
    string[] invalidTexts = {"XXX", "XXXX" /*...*/ }
public:
    BodyFilter(Handler *successor) : Handler(successor) { }
    
    bool doHandle(MailRequest *request) {
        for (auto s : invalidTexts) {
            if (request->getBody().find(s) != string::npos) {
                request->reject();
                return true;
            }
        }
        return false;
    }
};

class DefaultFilter : public Handler {
public:
    DefaultFilter(Handler *successor) : Handler(successor) { }
    
    bool doHandle(MailRequest *request) {
        request->reject();
        return true;
    }
};

// 测试代码
int main() {
    DefaultFilter f1(NULL);
    BodyFilter f2(&f1);
    TitleFilter f3(&f2);
    SenderFilter f4(&f3);
    
    Request *request = getRequest();
    f4.handler(request);
    if (request.isReject()) {
        cout << "Reject it." << endl;
    }
    else {
        cout << "Accept is." << endl;
    }
}
```