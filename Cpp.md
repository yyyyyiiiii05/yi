# C++ 代码的编译过程

可以分为以下几个主要步骤，每个步骤完成特定的任务，将源代码逐步转化为可执行程序：

### 1. **预处理（Preprocessing）**

**输入**：源代码文件（`.cpp` 或 `.h`）。
 **输出**：预处理后的代码。

主要任务：

- 处理以 # 开头的预处理指令，例如：
  - 宏替换（`#define`）
  - 条件编译（`#ifdef`、`#ifndef` 等）
  - 包含头文件（`#include`）
- 去除注释。

完成后会生成一个扩展的源代码文件，通常以 `.i` 结尾。

------

### 2. **编译（Compilation）**

**输入**：预处理后的代码。
 **输出**：汇编代码。

主要任务：

- 将 C++ 源代码转化为中间表示（如抽象语法树或中间代码）。
- 优化代码（如移除死代码、优化循环等）。
- 转换为目标处理器的汇编语言（通常以 `.s` 为后缀）。

------

### 3. **汇编（Assembly）**

**输入**：汇编代码（`.s` 文件）。
 **输出**：目标文件（机器码，通常是 `.o` 或 `.obj` 文件）。

主要任务：

- 汇编器（Assembler）将汇编语言代码转化为目标机器语言（二进制代码）。
- 目标文件通常是不可直接执行的。

------

### 4. **链接（Linking）**

**输入**：目标文件和库文件。
 **输出**：可执行文件。

主要任务：

- 将多个目标文件（如果有）进行合并。
- 链接标准库（如 `libc++` 或 `libstdc++`）、第三方库。
- 解决函数和变量的符号引用（符号表解析）。

完成后生成一个可执行文件（通常是 `.exe` 或无后缀的二进制文件）。





# 数据类型,常量与变量

## 字符与字符串

单个字符   一个 `char` 字符只能存储一个字符（如 `'a'`、`'1'`

```cpp
char c1 = 'A';
```

char * 是一个指针，指向以 \0 结尾的字符数组（即 C 风格字符串）

```cpp
char * c2 = "c2";
const char * c2 = "c2"; // 推荐在 C++ 中使用 const 修饰   字符串常量
```

`char c3[4]` 是一个字符数组，可以存储固定长度的字符串。必须预留一个额外的空间来存储字符串的结尾标志 `\0`

```cpp
char c3[4] = "c3";
```

std::string无需多言

```cpp
std::string str = "java";
```



## 常量

### 字面常量
字面常量是直接出现在代码中的固定值，例如：
- `42`（整数字面量）
- `'A'`（字符字面量）
- `"Hello"`（字符串字面量）

### 字符串常量
- 字符串字面量的类型是 `const char[N]`。
- 使用时，字符串常量可以**退化为**指向它的 `const char*` 指针。
- 可以通过 `std::string` 的构造函数将字符串常量转为 `std::string` 类型：
```cpp
void f(std::string s) { }
f("Hello");  // 自动将字符串常量转为 std::string
```

### `const` 修饰常量
- **`const` 修饰变量的值**，使变量成为常量：
  ```cpp
  const int a = 100;  // a 是常量，值不能修改
  ```
- **指向常量值的指针**（指针本身可变，但指针指向的值是常量）：
  ```cpp
  const int *p = &a;  // p 指向一个常量整数
  ```
- **指针本身是常量**（指针值不能修改，但可以修改指针指向的数据）：
  ```cpp
  int b = 200;
  int * const p = &b;  // p 是常量，不能指向其他地址
  ```
- **指针和值都是常量**：
  ```cpp
  const int * const p = &a;  // p 和 *p 都不能修改
  ```

### 枚举常量
- 枚举类型用于表示一组相关的常量值，**提高代码可读性和可维护性**。
- 默认情况下枚举值从 `0` 开始，也可以自定义起始值，未定义的值会递增：
  ```cpp
  enum Color {
      RED = 1,  // 从 1 开始
      GREEN,    // 自动为 2
      BLUE      // 自动为 3
  };
  ```
- 可以通过枚举类型声明变量：
  ```cpp
  Color c = RED;
  std::cout << c << std::endl;  // 输出 1
  ```

---

## 变量
变量是用于**存储数据的命名存储位置**，其值在程序运行过程中可以改变。

变量像是一个容器  变量类型决定了数据的类型和在内存中占用的大小，无论数据是否填满其分配的空间。



# 内存管理

## 内存区

1. 代码区

存放代码 

特点 :共享 只读

2. 全局区

全局变量

静态变量 static

3. 栈区

由编译器自动释放

存放函数的参数值,局部变量

4. 堆区

由程序员分配释放   运行结束系统释放

new在堆区开辟内存

5. 常量区

存储常量(如字符串常量,const修饰的全局变量等)的内存区域。这部分内存是只读的，且通常在程序执行期间不会改变。

## 内存分配

malloc和free 

默认返回void*类型的指针

new和delete



# 指针

## 指针

```cpp
int var = 10;
int * ptr2 = &var;
int* *ptr3 = &ptr2;//二级指针 
```

## 四种状态

1. **指向对象**：指针指向有效的对象，可以安全解引用。
2. **指向对象的紧邻空间**：指针超出了对象的范围，不能解引用。
3. **空指针**：指针不指向任何对象，解引用会导致错误。
4. **无效指针**：指针未初始化或指向已释放的内存，操作无效指针会导致未定义行为。

## 指针运算

指针可以像迭代器一样进行运算，操作中依据指针类型会增加相应大小的字节数。  

```cpp
int arr[5] = {1,2,3,4,5};
int* p = arr; 
p++;             // p 移动到数组下一位（指针会+4字节）
```

## const修饰指针

- pointer to const  

指向常量类型的指针

```cpp
 const int * p = &a;
int const * p = &a;
```

- const pointer   

指针是常量

```cpp
int * const p = &a;
```

- all const 

指针和值都是常量

```cpp
const int * const p = &a;
```



## 指向数组的指针

```cpp
int ia[3][4] = {
    {1, 2, 3, 4},
    {5, 6, 7, 8},
    {9, 10, 11, 12}
};
int (*p)[4] = ia;  // p 指向 多维数组 ia 的第一个数组
```



## 智能指针

### shared_ptr

用一个原始指针创建共享指针对象时,共享指针会管理这个原始指针,并且初始化引用计数为1,表示当前有一个对象在管理这个资源

```cpp 
std::shared_ptr<int> ptr1(new int(10)); // 引用计数为 1
```

当你将一个共享指针对象赋值给另一个对象时，或者使用拷贝构造函数创建新的智能指针对象时

引用计数会增加（`++count`），表示多了一个共享这个资源的智能指针。

现在,ptr1和 ptr2都指向同一个资源,它们共享所有权    引用计数增加到 2,表示有两个智能指针正在管理这个资源

```cpp
std::shared_ptr<int> ptr2 = ptr1;  // 引用计数从 1 增加到 2
```

每当一个智能指针对象被销毁时，它的引用计数会减少（`--count`）。如果这个引用计数减少到 `0`，表示没有智能指针再管理该资源，此时资源会被释放。



```cpp
//创建对象
std::shared_ptr<Student> stu2(new Student(12,"sdaf"));
std::shared_ptr<Student> stu3 = std::shared_ptr<Student>(new Student(13,"sdaf"));
std::shared_ptr<Student> stu4 = std::make_shared<Student>(14,"sdaf");
```

使用make_shared来创建智能指针对象  内存安全效率高  避免使用new

### unique_ptr

`std::unique_ptr` 是一个基于 RAII 的智能指针，用于独占管理动态分配的资源，能够在离开作用域时自动释放内存。

与 `std::shared_ptr` 不同，`std::unique_ptr` 只能由一个对象管理资源，不允许多个对象共享同一资源，只能通过 `std::move` 转移所有权。

```cpp
std::unique_ptr<Student> uptr2(new Student(12,"sdaf"));
std::unique_ptr<Student> uptr3 = std::unique_ptr<Student>(new Student(13,"sdaf"));
std::unique_ptr<Student> uptr4 = std::make_unique<Student>(14,"sdaf");
```

make_unique.........





# 引用

## 定义

引用是给已有变量**起别名**，它与原变量**共享同一块内存**。

```cpp
int a = 10;
int &b = a;  // b 是 a 的引用
```

- **引用必须在定义时绑定到一个变量**，并且之后不能更改绑定对象。  
  
  ```cpp
  int a = 10;
  int &b = a;  // 正确
  int c = 20;
  // int &b = c;  // 错误，b 已经是 a 的引用，不能再引用 c
  ```
  
- **引用与原变量相互影响**：修改 `a`，`b` 会同步更新；修改 `b`，`a` 也会同步更新。
  
  ```cpp
  a = 20;  // b 也等于 20
  b = 30;  // a 也等于 30
  ```

## 本质

引用的本质是一个**指针常量**，即**指针指向的地址不可变**，但可以通过指针修改该地址处的值

```cpp
int a = 10;
int &b = a;    // 等效于：int *const b = &a;  b 是指向 a 的指针常量
b = 20;          // 实际等效于：*b = 20;
```

## 左值引用和右值引用

- 左值引用（Lvalue Reference）

引用一个左值

```cpp
int a = 10;
int& ref = a; // ref 是 a 的左值引用
```

- 右值引用（Rvalue Reference）

右值引用是对一个右值(临时对象,字面量等)的引用

```cpp
int&& rref = 10; 
```

## 常量引用（`const` 引用）

`const` 修饰符可以创建**常量引用**，允许引用**常量,字面值或临时对象**(右值)

而非`const` 引用（即普通左值引用 `int&`）只能绑定到左值

```cpp
const int a = 10;
const int & b = a;//引用一个常量
const int &ref = 10;  //引用一个右值
int& ref2 = 42;       // 错误：非 const 引用不能绑定到临时对象
```

**编译器处理方式**：  编译器在后台会隐式地创建一个临时变量来存储这个常量值，然后让 ref 引用这个临时变量。

```cpp
int temp = 10;  // 编译器创建临时变量
const int &ref = temp;  // ref 引用这个临时变量
```

## 引用类型成员变量

引用类型的成员变量**只能通过初始化列表**进行初始化，因为引用一旦绑定，不能再更改，因此必须在对象构造时立即初始化

```cpp
class MyClass {
    int &ref;
public:
    MyClass(int &a) : ref(a) {}  // 只能在初始化列表中初始化
};
```



# 函数

## 传参

### 规则

1. **左值和右值**：
   - 左值（lvalue）是指有持久存储地址的表达式，可以出现在赋值操作的左侧。例如，变量名就是左值。
   - 右值（rvalue）是临时对象，通常出现在赋值操作的右侧，比如字面量和表达式的结果。

2. **函数参数传递**：
   - 如果函数参数是以左值引用（`T&`）的形式声明，那么在调用函数时必须传递一个左值。
   - 如果函数参数是以右值引用（`T&&`）的形式声明，那么在调用函数时必须传递一个右值。
   - 如果参数是普通类型（`T`），则可以接受左值和右值，因为在传递时会进行拷贝或移动。

3. **常量引用**：
   - 如果函数参数是以常量左值引用（`const T&`）的形式声明，那么可以传递左值和右值，但不能在函数内部修改该参数。



### 函数传入数组

```cpp
传数组就是传指针 
void func(int arr[]); 
void func(int arr[10]);
void func(int * arr); //都一样

传数组要带长度
void func(int arr[],length);

void func(int *arr, int length) {
  
}
int main( ) {
int myarr[] = {1, 2, 3, 4, 5};
func(myarr,5);//不可以直接  func( myarr) ;这样传的是一个地址  函数中只能访问到这一个地方
return 0;
}
```

### 传递引用

```cpp
vodi func1(int &a,int &b){
}
int main( ){
    int x =1;
    int y =2;
    func1(x,y);
    cout << x <<y<<endl;//对实参本身有影响
}
```

### 函数默认参数

```cpp
int func2 (int a = 10);//如果声明有默认参数 函数实现就不能有默认参数 

int func(int a, int b = 10,int c = 20){  //如果b有参数 他右边的都得有默认参数
       int sum = a+b+c;
        return sum;
    }
    int main(){
        func(10,10,10);//传参了就用传的参 没传参就用函数默认参数
        return 0;
    }
```

### 函数占位参数

void func (int)  写个数据类型就好

占位参数也是可以有默认参数

```cpp
void func (int a,int = 10){//有默认参数的占位参数
}
int main(){
    func(10,10)//掉用这个函数必须要传参
    return 0;
}  
```



## 返回值

要注意返回值作用域

### 函数返回引用

不能返回局部变量的引用

```cpp
int & func1( ){
    static int a = 10;//static修饰 保证调用完毕返回的内容还存在栈区
    return a;
}
int main(){
int &b = func1( ):
return 0;
}
```

函数的调用可以作为左值

```cpp
//返回值是个引用  也就是int &a=100;
func1() = 100;
```

### 函数返回指针

```cpp
int * func(){
	int *a = new int;//记住delete
	*a = 8;
	return a;
}
delete a;
```

### 函数返回数组

本质上就是返回指针  



## 函数重载

- 函数名相同。
- 参数列表（类型、数量或顺序）不同。
- 返回类型不参与重载的区分。

```cpp
void func(int a,int b);
void func(int b,int a);
void func(int a,int b,int c);
```

```cpp
//引用传参的重载
void func(int &a);
void func(cost int &a);//前面说的 相当于int tmp = 10;  const int &a = tmp;

int a=10;
func(a);//传入第一个 
func(10);//传入第二个  因为const修饰引用常量
```

```cpp
//函数重载碰到默认参数 如果都可以传参 就会报错
void func (int a);
void func (int a ,int b =10);

func(10);  //报错 两个都满足
```

## 函数指针

返回值类型 函数指针 参数类型  创建一个函数对象  接受一个函数 

```cpp
int add(int a, int b) { //有此函数
    return a + b;
}
//定义函数指针类型对象指向函数add
int(*fptr)(int,int) = &add; //&取地址可有可无
//调用
fptr(1,2);
```

## lambda表达式

```cpp
[capture](parameters) -> return_type {
    // body
}
```

**`capture`**：用于指定在Lambda表达式中可以访问的外部变量。可以按值捕获、按引用捕获或捕获所有外部变量。

​	 `[=]`：按值捕获所有外部变量(不建议)   `[&]`：按引用捕获所有外部变量 

**`parameters`**：指定参数，与常规函数参数类似。

**`return_type`**：指定返回类型（C++14以前需要手动指定，如果能够推导出则可以省略）。

**`body`**：函数体，包含实际的操作逻辑。



## std::function可调用对象封装器

声明一个 `std::function` 类型的变量

它可以存储任何符合<>内签名的可调用对象（如普通函数、Lambda 表达式、仿函数，甚至绑定的成员函数等）

```cpp
std::function<int(int)> f ; // <返回值(参数类型,参数类型)>
std::function<int(int)> flamb = [](int a){  //lambda
        return a;
};
std::vector<std::function<int(int)>> vf;
vf.emplace_back(flamb);
```



## std::bind

`std::bind` 用于将函数与参数绑定生成可调用对象（函数对象）。

它可以将函数的部分参数提前绑定，生成一个新的可调用对象（如 `std::function` 或 lambda)

```cpp
int add(int a, int b) {
    return a + b;
}
auto new_add = std::bind(add,10,std::placeholders::_1);
new_add(5);//参数传给placeholders

std::vector<std::function<int(int)>> vf;
vf.emplace_back(std::bind(add, std::placeholders::_1, 10));
```

std::placaholders   最多10个 

绑定成员函数





# 类和对象

- 访问权限

public: 公有成员可以在任何地方访问

protected: 保护成员只能在类的内部和派生类中访问

private: 私有成员只能在类的内部访问，派生类和外部都无法访问

- struct 和class区别

struct默认是public

class默认是private

- 类默认提供的三个函数：
  
  1. 默认构造函数（无参）
  2. 默认析构函数（无参）
  3. 默认拷贝构造函数（按成员属性逐一拷贝）
  
  如果定义了有参构造函数，则编译器**不再提供默认的无参构造函数**。
  
  如果定义了拷贝构造函数，编译器将**不会提供其他默认构造函数**。



## **构造函数分类及其调用**

### **1. 构造函数**
- 在对象创建时自动调用，用于初始化成员变量。
- 可以通过普通构造、拷贝构造或移动构造实现不同的初始化逻辑。

---

### **2. 拷贝构造函数**
- 创建一个新对象，并将已有对象的数据拷贝到新对象中。
- 使用 `const ClassName&` 作为参数，避免修改原对象和无限递归调用。

#### **调用场景：**
1. 使用一个已存在的对象初始化新对象。
   ```cpp
   MyClass obj1(10);
   MyClass obj2 = obj1;   // 拷贝构造
   ```
2. 函数以值传递方式传参。
   ```cpp
   void doWork(MyClass obj) { }  
   doWork(obj1);  // 调用拷贝构造
   ```
3. 函数以值返回对象。
   ```cpp
   MyClass createObject() {
       MyClass temp(20);
       return temp;  // 拷贝构造
   }
   MyClass obj = createObject();
   ```

#### **拷贝构造示例：**
```cpp
class MyClass {
public:
    int* data;
    MyClass(int value) : data(new int(value)) { }
    MyClass(const MyClass& other)
    {
        if(other.data == nullptr)
        {
            this->data = nullptr;
            return;
        }
        this->data = new int (*other.data);//深拷贝
    }
    ~MyClass() { delete data; }
};
```

#### **深拷贝与浅拷贝：**
- **浅拷贝**：多个对象共享同一块资源，可能导致内存管理问题。
- **深拷贝**：每个对象都有独立的资源  如拷贝后 指针分配新的内存并复制内容

**浅拷贝示例：**

```cpp
MyClass obj1(10);
MyClass obj2 = obj1;  // data 指向相同内存区域
```

**深拷贝示例：**
```cpp
MyClass(const MyClass& other) {
    if(other.data == nullptr)
    {
        this->data = nullptr;
        return;
    }
    data = new int(*other.data);  // 分配新的内存并复制内容
}
```

---

### **3. 移动构造函数**
- 使用右值构造对象
- 用于从一个对象**转移资源**到另一个对象。
- 参数是一个**右值引用** (`ClassName&&`)。
- 通常用于动态分配资源的优化，避免不必要的深拷贝。

#### **调用场景：**
1. **函数返回局部临时对象**：
   ```cpp
   MyClass createObject() {
       return MyClass(10);  // 返回右值
   }
   MyClass obj = createObject();  // 调用移动构造
   ```

2. **显式调用 `std::move`**：
   ```cpp
   MyClass obj1(10);
   MyClass obj2 = std::move(obj1);  // 调用移动构造
   ```

3. **临时对象赋值**：
   ```cpp
   MyClass obj = MyClass(20);  // 调用移动构造
   ```

#### **移动构造函数示例：**

虽然是data(other.data)浅拷贝 但是给原对象data置为空 这样类似深拷贝 且不会造成double free 

在拷贝构造中  原对象还要 所以要新开辟空间   移动构造直接用就行  原对象切割了 

```cpp
class MyClass {
public:
    int* data;
    MyClass(int value) : data(new int(value)) { }
    MyClass(MyClass&& other) noexcept : data(other.data) {
        other.data = nullptr;  //  符合移动语义
    }                                          
    ~MyClass() { delete data; }
};
```

---

### **4. 赋值运算符重载**

- 赋值和构造不一样 赋值时一个已存在的对象赋值给另一个存在对象 所以要注意更多
- 可拷贝可移动
- 通常需要自定义赋值运算符，特别是当类中涉及动态分配资源时。

**赋值运算符重载示例：**

```cpp
class MyClass {
public:
    int _a;
    int* _data;
    MyClass(int value) : data(new int(value)) { }
    MyClass& operator=(const MyClass& other) {
        if (this == &other) return *this;  // 防止自赋值 
        this->_a = other._a;
        if (_data) delete _data;  // 释放自身原有资源 
        this->_data = new int(*other._data);  // 分配新资源并复制内容                                                                        
        return *this;                                       
    }
    ~MyClass() { delete data; }
};
```

移动

```cpp
Student& Student::operator=(Student&& student)noexcept
{
	if (this == &student)return *this;
	this->_age = student._age; 
	if (_data) delete _data;  // 释放自身原有资源 
	this->_data = student._data; //符合移动语义
	student._data = nullptr;
	this->_thread = std::move(student._thread);
	return *this;
}
```



### **5. 初始化列表**

- 在构造函数中使用初始化列表，可以直接初始化成员变量，而不是先默认构造再赋值。
- **必须**使用初始化列表初始化的成员：
  - `const` 成员    //必须直接使用初始化列表初始化 创建成员之后无法再赋值
  - `引用`类型成员  //
  - 没有默认构造函数的类成员。

#### **初始化列表示例：**
```cpp
class MyClass {
public:
    const int id;
    int& ref;
    MyClass(int value, int& reference) : id(value), ref(reference) { }
};
```

### 静态成员变量

1.**属于类的成员变量**,所有对象的静态成员变量都再同一块内存区域中,所有实例共享同一个变量

   修改对象a m_A为100 对象b的 m_A也会变成100

2.类内声明,类外初始化 要有个初始值

3.是全局变量  静态成员变量存在于程序的整个生命周期，直到程序结束	

4.可以通过类或对象两种方式访问         

```cpp
class Person {
public:

static int m_A;//类内声明

//静态成员变量也有访问权限  
private:
static int m_B;
};

int Person::m_A = 100;//类外初始化

int main(){

Person p1;
//1通过对象访问
cout<<p1.m_A<<endl;

Person p2;
p2.m_A = 200;//所有对象的静态成员变量使用同一块内存 修改p2 p1的成员也会改变
cout<<p1.m_A<<endl;

//2通过类名访问
cout<<Person::m_A<<endl;

  return 0;
}
```



### 静态成员函数

属于类本身  可以在没有创建类对象的时候被调用

1类中所有对象共享同一个函数

2静态成员函数**只能**访问静态成员变量

```cpp
class Person {
public:

static int m_A;

static void func()//静态成员函数
{ 
  m_A = 100;//静态成员函数只能访问静态成员变量
  cout<<"static void func"<<endl;
}

private:
static void func2()
{
//静态成员函数也有访问权限
}

};

int Person::m_A = 0;

int main(){

//1.通过对象访问
Person p;
p.func();

//2.通过类名访问
Person::func();

  return 0;
}
```



### this指针

关键字this是一个指向非静态成员函数调用对象的指针   this本质是**指针常量**  指向不可以修改	

使用关键字 this来访问当前对象的成员变量和成员函数。

它在每个非静态成员函数内部都是隐式可用的

非静态成员函数访问的是非静态成员 非静态成员是存储在对象中的 所以可以用this

1.指向被调用的成员函数所属的对象

2.在类的非静态成员函数中返回对象本身,可使用return *this

返回对象本身可以使函数链式调用

```cpp
class Person {
public:
int age;
Person(int age)
{
  this->age=age;//1指向被调用的成员函数所属的对象
}
Person &add (Person &p)//传入的是引用 返回的也是引用
{
 return *this;//2返回对象本身
 }
};

int main(){

  Person yi(10);

  return 0;
}

```



### const修饰的 常对象 常函数

常量成员函数 在函数签名的末尾加上const关键字 常量成员函数可以访问对象的所有成员 

但不能修改它们，除非这些成员被声明为 mutable

​	

```cpp
class Person {
public:

int m_A;
mutable int m_B;

void showPerson(int a) const
{
  //常量成员函数无法修改对象的成员  除非成员被mutable修饰
  //m_A = a;
  //this->m_A = a;
  this -> m_B = 100;
}

void func () 
{

}

};

int main(){

//常对象不能修改属性
const Person p;
//p2.m_A = 0; 
p.m_B = 0;

//常对象只能调用常函数
p.showPerson(1);
//p.func(); ×
  return 0;
}

```





## 友元friend

在类中声明一个函数或者类是我的friend  这个friend就可以访问类中的私有和保护成员

### 1全局函数做友元

```cpp
class MyClass {
private:
    int value;

public:
    
    // 声明友元函数  这样全局函数就可以访问类中私有成员
    friend void displayValue(const MyClass& obj);
    
};

// 定义友元函数
void displayValue(const MyClass& obj) {
   :cout << "Value: " << obj.value << endl;//可以访问private成员
}

int main() {

    displayValue(obj);  // 输出: Value: 10
    
    return 0;
}

```



### 2类做友元

```cpp
class MyClass {
private:
    int value;

public:
    MyClass(int v) : value(v) {
      
    }

    // 声明友元类
    friend class FriendClass;
};

class FriendClass {
public:
    void func(const MyClass& obj) {
        cout << "Value: " << obj.value << endl;//在MyClass类中声明友元FriendClass  
                                                                         //所以这个类中可以访问MyClass类中的privite成员
    }
};

int main() {
   MyClass yi(10);
   FriendClass shunfei;
   shunfei.func(yi);  // 输出: Value: 10
    return 0;
}
```



### 3成员函数做友元

```cpp
//我们希望OtherClass的成员函数可以访问MyClass的私有成员
class MyClass;//前向声明  因为函数display参数中用到了MyClass类  但是我们还没创建

class OtherClass {
public:
    void displayValue(const MyClass& obj);//在类内声明 类外定义 在其他类中声明友元就可调用私有成员
};


class MyClass {
private:
    int value;

public:
    MyClass(int v) : value(v) {}//初始化列表

    // 声明友元成员函数   ohterclass类种的displayvalue函数可以访问myclass类中的私有成员
    friend void OtherClass::displayValue(const MyClass& obj);
};

void OtherClass::displayValue(const MyClass& obj) {
    cout << "Value: " << obj.value << endl;
}


int main() {
    MyClass obj(10);
    OtherClass otherObj;
    otherObj.displayValue(obj); //类中函数在MyClass类中声明有元 可调用MyClass类中私有成员 输出: Value: 10   
    return 0;
}
```





## 运算符重载

是成员函数

运算符就是函数 重载就是增加它可以运算的数据类型

### +重载

定义

```cpp
MyString &MyString::operator+(const MyString &other) {
    if(other._data ==nullptr){
        return * this;
    }
    char * temp = new char[strlen(_data)+strlen(other._data)+1];
    strcpy(temp,_data);
    strcat(temp,other._data);

    delete [] _data;
    _data = temp;
    return * this;
}
```

调用

p1+是函数  传入p2

```cpp
char * _data = p1 + p2;     
```



### <<

```cpp
std::cout << p1;
```

其背后的流程可以分解为：

1. **编译器寻找匹配的重载函数**： 编译器会找到形如：

   ```cpp
   std::ostream& operator<<(std::ostream& os, const Person& person);
   ```

2. **实参绑定**：

   - `std::cout` 被绑定为 `os` 参数。
   - `p1` 被绑定为 `person` 参数。

3. **函数执行**： 进入重载函数：

   ```cpp
   std::ostream& operator<<(std::ostream& os, const Person& person) {
       os << "Name: " << person.name << ", Age: " << person.age;
       return os;
   }
   ```

实际上输出是 <<p1  替换为os    << "Name: " << person.name << ", Age: " << person.age;

```cpp
std::cout<< "Name: " << person.name << ", Age: " << person.age;
```



### 递增运算符重载

```cpp
class MyInteger
{
    friend ostream & operator<<(ostream & out,MyInteger);
    public:
    MyInteger()
    {
        m_Num = 0;
    }

    MyInteger & operator++()//前置递增
    {
        m_Num++;
        return *this;
    }
    MyInteger operator++(int)//占位参数 表示后置递增
    {
        MyInteger temp = *this;
        m_Num ++;
        return temp;
    }
    private:
    int m_Num;
};
ostream & operator<<(ostream & out,MyInteger myint){
    cout << myint.m_Num <<endl;

    return out;
}

int main(){
    MyInteger myint;
    // cout << ++myint <<endl;
    cout << myint++ <<endl;
    
    return 0;
}
```



### =重载

```cpp
class Person
{
    public:
    int * m_Age;

    Person(int age){//构造函数
    m_Age = new int (age);
    }
    
    ~Person()//析构函数 清理堆中空间
    {
        if(m_Age != NULL)
        {
            delete m_Age;
            m_Age = NULL;
        }
    }

    Person & operator=(Person &p)//重构= 实现深拷贝
    {
        if (m_Age !=NULL)
        {
            delete m_Age;
            m_Age = NULL;
        }
        m_Age = new int(*p.m_Age);
        return *this;
    }

};

int main()
{
    Person p1(18);
    Person p2(20);

    p2 = p1;//p2.operator=(p1);

    cout<<*p1.m_Age<<endl;
    cout<<*p2.m_Age<<endl;
    return 0;
}
```



### 关系运算符重载 <   >   ==   !=

```cpp
class Person
{
public:
string m_Name;
int m_Age;

Person(string name,int age)
{
 m_Name = name;
 m_Age = age;
}
bool operator==(Person &p)//传入引用  其他逻辑运算符都是一样 返回bool
{
if(this->m_Name == p.m_Name && this->m_Age ==p.m_Age)
{
    return true;
}
return false;
}
};
int main()
{
    Person p1("张顺意",19);
    Person p2("张顺飞",39);

    if(p1 == p2)
    {
        cout<<"same"<<endl;
    }
    else{
        cout<<"not the same"<<endl;
    }


    return 0;
}
```



### 函数调用运算符重载  ( )    

仿函数  函数对象

```cpp
class Add {
private:
    int a,b;
public:
    Add(int x, int y) : a(x), b(y) {}

    // 重载函数调用运算符，不需要传入参数，直接使用成员变量 a 和 b
    int operator()() const {
        return a + b;
    }
};
int main()
{
	Add add(3, 4);  // 创建函数对象add
    int result = add();  //实质上是add对象调用了类中的 operator()函数
    return 0;
}
```



# 继承

### 继承方式

public protected private

继承方式只会缩小成员（包括成员函数和成员变量）在子类中的权限 权限变小

### 派生类的创建

创建派生类对象时  需要**先**创建基类对象

如果基类有默认构造函数 则自动调用基类默认构造函数   如果没有默认构造函数   则需要显式调用基类有参构造

先调用基类构造函数 再调用子类构造函数  析构时先调用子类析构函数 再调用基类析构函数

 ```cpp
class Base{
public:
    Base(int num1, int num2):privateNum(num1),protectedNum(num2){}
private:
    int privateNum;
protected:
    int protectedNum;
};
class Derived :public Base{
public:
    Derived(): Base(1,1){} //调用基类构造函数 创建基类对象
    Derived(int num1,int num2):Base(num1,num2){}
};
 ```





### 继承同名成员

访问父类中的同名成员需要加作用域 无作用域默认访问子类同名成员

如果子类出现和父类同名的成员 子类的同名成员函数会隐藏父类中所有同名成员函数

```cpp
class Base
{
    public :

    int m_A;
    Base()
    {
        m_A = 100;
    }

    void func()
    {
            cout<<"Base"<<endl;
    }
    void func(int a)//重载
    {
        cout<<"Base overloading"<<endl;
    }
    
    static int m_Static;
    static void funcStatic()
    {
        cout<<"BaseStatic"<<endl;
    }
    static void funcStatic(int a)
    {
        cout<<"BaseStaticOverloading"<<endl;
    }
};
int Base::m_Static = 100;

class Son :public Base
{
    public:

    int m_A;
    Son(){
    m_A = 200;
    }

    void func()
    {
            cout<<"Derived"<<endl;
    }

    static int m_Static;
    static void funcStatic()
    {
        cout<<"DerivedStatic"<<endl;
    }
    static void funcStatic(int a)
    {
        cout<<"DerivedStaticOverloading"<<endl;
    }
    
};
int Son::m_Static = 200;


int main(){

    Son s;

    cout<<s.m_A<<endl;//访问的是子类中的
    cout<<s.Base::m_A<<endl;//加了作用域 表示父类中的
    s.func();
    s.Base::func();
    s.Base::func(100);//调用父类中的重载函数
    
    
    //同名静态成员可以通过类名访问  这是他的特性
    cout<<Son::m_Static<<endl;
    cout<<Base::m_Static<<endl;
    cout<<Son::Base::m_Static<<endl;//访问父类作用域下
    s.funcStatic();
    s.Base::funcStatic();
    Son::funcStatic();
    Son::funcStatic(100);
    Son::Base::funcStatic();
    Son::Base::funcStatic(100);
    
    return 0;
}
```

### 多继承

c++一个类可以继承多个类   可以认多个爹   问题多 不建议使用

```CPP
class Son:public Base1,public Base2
{
};
```



### 菱形继承与虚继承

为了解决菱形继承中基类重复的问题，引入了**虚继承**。

虚继承确保在菱形继承结构中，最顶层的基类只会有一个实例

无论是Top Mid Bottom 都是用的同一份数据 

```cpp
class Top
{ 
    public:
    int a;
};
class Mid1 :virtual public Top{};
class Mid2 :virtual public Top{};
class Bottom :public Mid1,public Mid2{};

int main(){
    Bottom yi;

    yi.Mid1::a = 10;
    yi.Mid2::a = 20;
    yi.a = 100;

    //不使用虚继承   这些数据都各自独立
    cout<<yi.Mid1::a<<endl;
    cout<<yi.Mid2::a<<endl;
    cout<<yi.a<<endl;
    return 0;
}
```





# 多态

**类的多态**是面向对象编程中实现多态性的关键

它允许在类层次结构中，通过基类指针或引用调用子类的**方法**，而无需知道子类的具体实现。

类的多态通常通过**虚函数**和**继承**来实现，也称为**运行时多态**（动态多态）

## 虚函数

父类类型指针or引用指向子类对象  可以通过虚函数来调用子类方法   否则调用基类方法  这是一种封装思想

子类重写基类的虚函数时，重写的函数会天然是虚函数   无需额外标注virtual

可以使用 `override` 关键字来显式表明重写的意图 (好习惯 可以防止误输入)

```cpp
class Base {
public:
    virtual void func() { } // 虚函数
    virtual ~Base() { } // 虚析构函数
};
class Derived : public Base {
public:
    void func() override { } // 重写虚函数
};
int main() {
    Base* ptr = new Derived(); // 父类指针指向子类对象
    ptr->func();              // 输出：Derived::func()
    delete ptr;               // 确保调用子类析构函数
    return 0;
}

```

## 纯虚函数

在类中将一个函数声明为纯虚函数，派生类须重写（实现）该函数，否则为抽象类，无法实例化

```cpp
virtual void func () = 0;
```

## 纯虚类(抽象类)

**只要类中包含至少一个纯虚函数**，它就被称为抽象类。

抽象类不能被实例化，意味着你不能创建抽象类的对象，但可以通过它来定义派生类。

派生类必须重写所有的纯虚函数才能成为具体类(即可以实例化的类),否则为抽象类

## 虚析构和纯虚析构

虚析构函数是一个在基类中声明为`virtual`的析构函数

确保在通过基类指针删除派生类对象时，派生类的析构函数能够被正确调用，避免资源泄露或未定义行为。

```cpp
class Base
{
public:
Base() = default;
virtual ~Base() { //虚析构
    std::cout<<"~Base()"<<std::endl;
};
};
class Derived:public Base
{
public:
    Derived() = default;
    ~Derived() override {
        std::cout<<"~Derived()"<<std::endl;
    } ;
};
```

# 文件操作

保存程序运行时的数据	

需要包含头文件    #include < fstream >     // fileStream

头文件中三个类  ofstream  ifstream  fstream   写   读   读写

## 1.文本文件 文件以ascii码形式存储在计算机中

写文件

1. 包含头文件

   #include < fstream> 

2. 创建流对象

   ofstream ofs;  //output file  将程序内容输出到文件中

3. 打开文件

   ofs.open("文件路径",打开方式);   //ofs.open("test.txt",ios::out);  

4. 写数据
   ofs<<"写入的数据"<<endl;

5. 关闭文件

   ofs.close();  

```cpp
int main()
{  
    ofstream ofs;
    ofs.open("D:/cunchuweizhi/desktop/Code/test.txt",ios::out);
    ofs<<"yiyiyiyiyiyi"<<endl;
    ofs<<"Yiyiyiyiu"<<endl;
    ofs.close();
    return 0;
}
```

读文件

1. 包含头文件

   #include < fstream> 

2. 创建流对象

   ifstream ifs;  //input file  将文件内容input到程序中

3. 打开文件

   ifs.open("文件路径",打开方式);  

4. 读数据

5. 关闭文件

   ifs.close();  

   ```cpp
   int main()
   {
       ifstream ifs;
       ifs.open("D:/cunchuweizhi/desktop/Code/test.txt",ios::in);
       if(!ifs.is_open())//没打开就返回1
       {
           cout<<"打开失败"<<endl;
           return 0;
       }
       
       char buf[1024] = {0};
       while(ifs>>buf)
       {
           cout<<buf<<endl;
       }
   
       ifs.close();
       return 0;
   }
   
   ```

   

## 2.二进制文件



# 模板

## 函数模板

建立一个通用函数或类，其类内部的类型和函数的形参类型不具体指定，用一个虚拟的类型来代表

 ```cpp
//声明模板 
template <typename T1,typename T2>  //定义了多个数据类型  一定要用 否则会报错
void swap(T1 &a, T2 &b)
{
    T1 temp1 = a;
    T2 temp2 = b;
}
//使用函数模板
swap(a,b);//自动类型推导   
swap<int,string>(a,b);//指定类型

 ```

普通函数和函数模板重载   函数模板也能重载

普通函数能实现 优先调用普通函数

## 类模板

```cpp
template<class NameType,class AgeType = int>//默认类型int    //class也可以写成typename
class Person
{
    public:
    NameType m_Name;
    AgeType m_Age;
    Person(NameType name,AgeType age)
    {
        this->m_Name = name;
        this->m_Age = age;
    }
};
    
int main()
{
    Person<string,int>p1("yi",18);
    Person<string>p2("顺飞",18);//模板参数列表中有默认类型 不写类型就用默认
    return 0;
}
```



### 类模板对象做函数参数

将类模板创建出的对象传入函数的三种方法

```cpp
template<class T1,class T2>//模板类
class Person
{
    public:
    T1 m_Name;
    T2 m_Age;
    Person(T1 name,T2 age)
    {
        this->m_Age = age;
        this->m_Name = name;
    }
    void showPerson()
    {
        cout<<"age"<<this->m_Age<<"name"<<this->m_Name<<endl;
    }
};
//函数传入类模板创建的对象 
//1.指定传入类型
//在这种方法中，函数的参数类型是明确指定的，该函数只能接受 Person<string, int> 类型的对象。
void printPerson1(Person<string,int>&p1)
{
    p1.showPerson();
}
void test1()
{
    Person<string,int>p1("1",1);
    printPerson1(p1);
}

//2.参数模板化
//这种方法使用模板参数在函数中处理Person类模板的对象。这使得函数可以接受任意类型的 Person 对象。
template<class T1,class T2>
void printPerson2(Person<T1,T2>&p2)
{
    p2.showPerson();
}
void test2()
{
    Person<string,int>p2("2",2);
    printPerson1(p2);

}
//3.整个类模板化
//这种方法将整个对象作为模板参数传递，使得函数能够接受任何类型的对象，只要该对象具有 showPerson 方法。
template<class T>
void printPerson3(T &p3)
{
    p3.showPerson();
}
void test3()
{
    Person<string,int>p3("3",3);
    printPerson1(p3);
}

int main()
{
    test1();
    test2();
    test3();
    return 0;
}
```

### 类模板与继承

```cpp
template<class T>
class Base
{
    public:
    T m;
};

template<class T1,class T2>
class Son:public Base<T2>//T2类型传给父类
{
    T1 obj;
};

int main()
{
    Son<int,char>S2;
    return 0;
}

```

### 类模板 构造函数,成员函数的类外实现

```cpp
template<class T1,class T2>
class Person
{
    public:
    T1 m_Name;
    T2 m_Age;
    Person(T1 name,T2 age);
    // {
    //     this->m_Age = age;
    //     this->m_Name = name;
    // }

    void showPerson();
    // {
    //     cout<<"name"<<this->m_Name<<"age"<<this->m_Age<<endl;
    // }
};

//构造函数类外实现
template<class T1,class T2>
Person<T1,T2>::Person(T1 name,T2 age)
{
    this->m_Age = age;
    this->m_Name = name;
}
//成员函数类外实现
template<class T1,class T2>
void Person<T1,T2>::showPerson()
{
    cout<<"name"<<this->m_Name<<"age"<<this->m_Age<<endl;
}
//总结  主要就是加个template声明和类模板作用域

int main()
{
    Person<string,int>yi("yi",19);
    yi.showPerson();
    return 0;
}
```



### 类模板分文件编写.hpp

将.h和.cpp写在一起 起名.hpp    也就是类模板声明和定义写一起



### 类模板与友元friend

```cpp
template<class T1,class T2>//模板类
class Person
{
    //全局函数 类内实现
    friend void printPerson(Person<T1,T2> p)
    {
        cout<<"age"<<p.m_Age<<"name"<<p.m_Name<<endl;
    }
    //全局函数 类外实现  略
    public:
    
    Person(T1 name,T2 age)
    {
        this->m_Age = age;
        this->m_Name = name;
    }

    private:
    T1 m_Name;
    T2 m_Age;
};


int main()
{
    Person<string,int>yi("yi",19);
    printPerson(yi);

    return 0;
}

```





# container

## iterator

An iterator is an object **(like a pointer)** that points to an element inside the container

for循环中判断迭代器是否遍历到最后一个元素使用 != 而非 < 进行判断,

C++程序员习惯性地使用 !=，其原因和他们更愿意使用迭代器而非下标的原因一样

因为这种编程风格在标准库提供的所有容器上都有效. 只有string和vector等一些标准库类型有下标运算符，而并非全都如此。

所有标准库容器的迭代器都定义了==和！=，但是它们中的大多数都没有定义<运算符。

因此，只要我们养成使用迭代器和 != 的习惯，就不用太在意用的到底是哪种容器类型。

## 范围for循环 

专门用于遍历容器、数组或其他支持迭代的对象

```cpp
int arr[] = {1, 2, 3, 4, 5};
for (const auto& a : arr) {
	cout << a << endl;
}
```



## emplace_back

`emplace_back` 是 C++ 标准库中 `std::vector` 和其他容器的一种成员函数，用于在容器的末尾添加新元素。

```cpp
vector_name.emplace_back(args...);
```

```cpp
std::vector<std::thread>threads;
threads.emplace_back(func, i); // 可以直接在容器中构造线程对象
```

`emplace_back` **直接在容器内部构造对象**，而不需要先构造对象再将其复制或移动到容器中，这样可以提高性能，尤其是在添加复杂对象时。

`push_back` 需要先先构造对象，再复制或移动到容器中  适合于已有对象添加到容器中



## container

### vector

**描述**：动态数组

- 提供动态扩展功能，支持随机访问

### stack

**描述**：栈（后进先出，LIFO）

- **操作限制**：只能对栈顶进行操作。
- 常用操作
  - `push`：插入元素到栈顶。
  - `pop`：删除栈顶元素。
  - `top`：获取栈顶元素。

### queue

**描述**：队列（先进先出，FIFO）

- **特点**：尾部插入，头部删除（像排队）。
- 常用操作
  - `push`：尾部插入元素。
  - `pop`：头部删除元素。
  - `front`：获取队头元素。
  - `back`：获取队尾元素。

### list

**描述**：双向链表

- 特点
  - 插入和删除操作效率高，适合频繁修改数据结构的场景。
  - 不支持随机访问，需通过迭代器遍历。
  - 是一个循环双向链表：尾部节点的 `next` 指针指向头部节点，头部节点的 `prev` 指针指向尾部节点。
- 适用场景
  - 数据经常增删，且对访问速度要求不高的场景。

### deque

**描述**：双端数组

- 特点
  - 支持两端高效的插入和删除操作。
  - 内部实现为分段连续存储，扩展时效率高于 `vector`。
  - 访问中间元素时效率低于 `vector`。
- 适用场景
  - 需要同时操作头尾的场景，如滑动窗口问题



### map / multimap

**描述**：键值对容器（关联式容器）

- 特点
  - 每个元素是一个 `std::pair`（键值对）。
  - key 作为键，value作为值。
  - 自动按 key排序
  - key不允许重复 (multimap允许重复 key)

```cpp
std::map<int, std::string> myMap;
// 方法 1: 使用 make_pair
myMap.insert(std::make_pair(1, "Apple"));
// 方法 2: 使用初始化列表
myMap.insert({2, "Banana"});
// 方法 3: 使用下标运算符
myMap[3] = "Cherry"; // 插入 key=3, value="Cherry"

myMap.erase(3);//删除key为3的pair
```



### set / multiset

**描述**：集合（关联式容器，基于二叉树实现）

- 特点
  - 插入元素后自动排序。
  - `set`：不允许重复元素。
  - `multiset`：允许重复元素。

```cpp
std::set<int, compare> s1; // compare 为排序谓词
bool compare(int v1, int v2) {
    return v1 > v2; // 降序
}
```





# stl

standard template library

## 谓词predicate

在C++中，谓词（Predicate）是一个返回布尔值的函数对象或函数。

谓词用于STL中的算法，例如 `std::sort`, `std::find_if` 等，可以帮助定义排序、过滤或搜索的条件。谓词可以是：

1. **一元谓词（Unary Predicate）**：接受一个参数，返回`true`或`false`。例如：

   ```cpp
   bool is_even(int n) {
       return n % 2 == 0;
   }
   std::vector<int> vec = {1, 2, 3, 4, 5, 6};
   auto it = std::find_if(vec.begin(), vec.end(), is_even);
   ```
   
2. **二元谓词（Binary Predicate）**：接受两个参数，返回布尔值。常用于排序算法中。比如自定义比较函数：

   ```cpp
   bool compare(int a, int b) {
       return a > b; // 降序排列
   }
   std::vector<int> vec = {3, 1, 4, 1, 5};
   std::sort(vec.begin(), vec.end(), compare);
   ```
   

- **Lambda表达式谓词**：

  ```cpp
  std::vector<int> vec = {1, 2, 3, 4, 5};
  auto it = std::find_if(vec.begin(), vec.end(), [](int n) { return n > 3; });
  ```



## algorithm

### 遍历

#### for_each

遍历范围 [first, last)内的每个元素，并对每个元素调用函数func();

for_each(v.begin(),v.end(),func());

#### transform

对范围内的每个元素应用指定的操作(一元或二元)，并将结果存储到另一个容器中

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <cmath>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    std::vector<int> result(vec.size());

    // 使用 lambda 表达式对范围内元素进行平方变换  然后从result.begin()开始导入
    std::transform(vec.begin(), vec.end(), result.begin(), [](int n) { return n * n; });

    std::cout << "平方后的元素: ";
    for (int n : result) {
        std::cout << n << " ";
    }
    std::cout << std::endl;

    return 0;
}


```

### 查找

#### find

```cpp
#include <iostream>
#include <vector>
#include <algorithm> // 包含find算法头文件

int main() {
    <int> vec = {10, 20, 30, 40, 50};

    // 使用find函数在vec中查找值为30的元素
    vector<int>::iterator it = find(vec.begin(), vec.end(), 30);

    // 检查元素是否找到
    if (it != vec.end()) {
        cout << "找到元素: " << *it << endl;
    } else {
        cout << "元素未找到" << endl;
    }

    return 0;
}

```

#### find_if

在指定范围内查找**第一个**满足给定条件的元素   返回指向该元素的迭代器    未找到会返回end迭代器

 一个一个传入谓词  谓词返回true则此元素满足条件  

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

while(true)
{
	std::cout << tip << std::endl;
	std::cin >> id;
	//find_if 从给的范围开始遍历 一个一个传入谓词 谓词返回true则此元素满足条件 返回指向该元素的迭代器    没找到返回end迭代器
	if (std::find_if(vStu.begin(), vStu.end(), [id](const Student& s) { return s.m_Id == id; }) == vStu.end())
	{
	break;
	}
	else
	{
	std::cout << "已经创建账号,请重新输入" << std::endl << std::endl;
	system("pause");
	system("cls");
	}
}
```

#### adjacent_find

adjacent  adj 相邻的

查找范围区间内第一个相邻重复的元素  返回第一个元素的迭代器 没找到就返回end迭代器

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    vector<int> vec = {1, 2, 3, 3, 4, 5};

    // 使用adjacent_find查找第一个相邻相等的元素
    vector<int>::iterator it = adjacent_find(vec.begin(), vec.end());

    if (it != vec.end()) {
        cout << "找到相邻相等的元素对: (" << *it << ", " << *(it + 1) << ")" << endl;
    } else {
        cout << "未找到相邻相等的元素对" << endl;
    }

    return 0;
}

```

#### binary_search

二分查找元素 返回bool

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5, 6, 7, 8, 9};

    // 使用binary_search查找元素5
    bool found = binary_search(vec.begin(), vec.end(), 5);

    if (found) {
        std::cout << "元素5存在于范围内" << std::endl;
    } else {
        std::cout << "元素5不存在于范围内" << std::endl;
    }

    return 0;
}

```

#### count

统计范围内指定元素出现次数

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 2, 2, 5, 2};

    // 使用count统计元素2在范围内出现的次数
    int count_of_twos = std::count(vec.begin(), vec.end(), 2);

    std::cout << "元素2出现的次数: " << count_of_twos << std::endl;

    return 0;
}

```

#### count_if

用于统计范围内满足**谓词条件**的元素个数

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// 自定义谓词函数
bool isEven(int n) {
    return n % 2 == 0;
}

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5, 6};

    // 使用count_if统计偶数的数量
    int even_count = std::count_if(vec.begin(), vec.end(), isEven);

    std::cout << "偶数的数量: " << even_count << std::endl;

    return 0;
}

```



### 排序

#### sort

可选填排序规则   无则为升序

#### random_shuffle

shuffle n洗牌

给定范围  打乱  洗牌算法

#### merge

将两个有序的容器合并 合并后的容器还是有序的  

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec1 = {1, 3, 5, 7, 9};
    std::vector<int> vec2 = {2, 4, 6, 8, 10};
    std::vector<int> result(vec1.size() + vec2.size());

    // 合并 vec1 和 vec2 到 result
    std::merge(vec1.begin(), vec1.end(), vec2.begin(), vec2.end(), result.begin());

    // 输出结果
    std::cout << "合并后的结果: ";
    for (int num : result) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    //合并后的结果: 1 2 3 4 5 6 7 8 9 10

    return 0;
}

```

#### reverse

给定范围  反转了

### 拷贝替换

#### copy

目标范围必须足够大，以容纳要复制的元素数量

```cpp
// 使用std::copy将source中的元素复制到destination中
    std::copy(source.begin(), source.end(), destination.begin());
```

#### replace

把一个区间内的旧元素替换为新元素

```cpp
// 使用std::replace将所有等于2的元素替换为99
    std::replace(data.begin(), data.end(), 2, 99);
```

#### replace_if

把区间内满足条件的元素替换为新元素

```cpp
// 使用std::replace_if将所有偶数替换为0
    std::replace_if(data.begin(), data.end(), [](int n){ return n % 2 == 0; }, 0);
```

#### swap

互换两个容器元素  同种类型容器

### 算数生成

include <numeric>

#### accumulate

计算范围中的和

```cpp
 // 使用std::accumulate计算data中所有元素的累积和，初始值为0
    int sum = std::accumulate(data.begin(), data.end(), 0);
```

#### fill

将指定范围内的所有元素填充为给定的值

```cpp
// 使用std::fill将data中的所有元素填充为7
    std::fill(data.begin(), data.end(), 7);
```



### 集合

操作两个容器

#### set_intersection

用于计算两个**有序序列**的交集

inter  section 

两容器交到一起的部分

```cpp
// 创建一个容器来存储结果
    std::vector<int> intersection;

// 使用std::set_intersection计算交集
    std::sort(vec1.begin(), vec1.end()); // 确保vec1是有序的
    std::sort(vec2.begin(), vec2.end()); // 确保vec2是有序的
//使用算法
    std::set_intersection(vec1.begin(), vec1.end(), vec2.begin(), vec2.end(),
                          std::back_inserter(intersection));
```

#### set_union

用于计算两个**有序序列**的并集

```cpp
// 创建一个容器来存储结果
    std::vector<int> union_result;

    // 使用std::set_union计算并集
    std::sort(vec1.begin(), vec1.end()); // 确保vec1是有序的
    std::sort(vec2.begin(), vec2.end()); // 确保vec2是有序的

    std::set_union(vec1.begin(), vec1.end(), vec2.begin(), vec2.end(),
                   std::back_inserter(union_result));
```

#### set_difference

用于计算两个**有序序列**的差集

a对b的差集是a在b中没有的

b对a的差集是b在a中没有的

```cpp
   // 创建一个容器来存储结果
    std::vector<int> difference;

    // 使用std::set_difference计算差集
    std::sort(vec1.begin(), vec1.end()); // 确保vec1是有序的
    std::sort(vec2.begin(), vec2.end()); // 确保vec2是有序的

    std::set_difference(vec1.begin(), vec1.end(), vec2.begin(), vec2.end(),//1对2的差集 结果是1中去除交集后的元素
                        std::back_inserter(difference));
```







# rand() srand()生成随机数

srand() 设置种子，rand 使用该种子生成随机数

```cpp
// 使用当前时间作为随机生成器的种子    类型为无符号整型
srand((unsigned int)time(NULL));

// 生成 [0, 10-1] 范围内的随机数
std::rand() % 10;//取模 这样剩下的就是小于取模的数的值 这里的是 0-9随机数   要取10-19就加10
```



# extern

在头文件中声明一个全局变量并希望在多个源文件中共享它，通常会使用 `extern` 关键字

用于声明一个变量或函数是在其他地方定义的，通常是在另一个文件中

C++ 中  函数默认是 `extern` 的，但 **变量** 不是。

函数的默认行为：

- 在 C++ 中，函数默认具有外部链接属性（即默认是 `extern`），这意味着它们可以在其他文件中使用，不需要显式地使用 `extern` 关键字。
  
  例如：
  ```cpp
  // file1.cpp
  void foo() { }
  
  // file2.cpp
  extern void foo(); // 可省略 extern
  ```

变量的默认行为：

- 全局变量则不同，它们在C++中 **不默认是 `extern`**，如果你希望在多个文件中共享全局变量，必须显式地使用 `extern` 关键字声明它。
  
  例如：
  ```cpp
  // file1.cpp
  int globalVar = 10;
  
  // file2.cpp
  extern int globalVar; // 需要显式声明
  ```







# std::call_once

`std::call_once` 是一个线程安全的函数，用于确保某个操作（通常是初始化）只会执行一次。

它接受一个 `std::once_flag` 和一个可调用对象（如函数或 lambda 表达式）。

```cpp
static std::once_flag s_flag;
std::call_once(s_flag, [&](){_instance = shared_ptr<T>(new T);});
```

具体工作原理：

1. 当你调用 `std::call_once` 时，它会检查传入的 `std::once_flag` 是否已经标记为“已调用”。
2. 如果没有，它会执行指定的可调用对象，并将 `std::once_flag` 标记为“已调用”。
3. 后续对同一 `std::once_flag` 的调用将不会再执行该可调用对象。

这种机制在多线程环境中特别有用，能防止多个线程同时初始化资源。





# singleton

- 传统的单例模板类


```cpp
#pragma once
#include<memory>
#include<mutex>
#include<iostream>

//定义一个模板类 Singleton，其中 T 是任意类型。
template<typename T>
class Singleton
{
protected:

    // = default; 是 C++11 引入的语法，用于指定一个类的特殊成员函数（如构造函数、析构函数、拷贝构造函数等）使用默认实现
	Singleton() = default;

    //删除拷贝构造函数和赋值运算符，确保无法复制或赋值该类的实例
	Singleton(const Singleton<T>&) = delete;
	Singleton& operator = (const Singleton<T>& st) = delete;

    static std::shared_ptr<T> _instance;//这就是单例成员 动态指针  而且封装
    //static修饰 属于类变量 所有实例共享一个变量

public:

    //静态成员函数 属于类本身  可以在没有创建类对象的时候被调用 1类中所有对象共享同一个函数  2静态成员函数只能访问静态成员变量
    static std::shared_ptr<T> GetInstance() 
    {
        //保证在多线程环境中，单例实例只会被创建一次，避免重复创建的问题  
        //无论谁get 只有第一次get会创建一个实例  这就是单例
        static std::once_flag s_flag;//声明一个静态的 once_flag，用于确保单例实例只被创建一次
        std::call_once(s_flag, [&](){_instance = std::shared_ptr<T>(new T);});
        //检查 s_flag 是否已被初始化。如果未初始化，则初始化并执行传入的 lambda 函数，在该函数中创建 _instance 的共享指针实例。

        return _instance;
    }

    void PrintAddress() 
    {
        std::cout << _instance.get() << std::endl;
    }

    ~Singleton() 
    {
        std::cout << "this is singleton destruct" << std::endl;
    }

};

//初始化静态成员 _instance 为 nullptr，确保在使用之前不会有未定义行为。
template <typename T>
std::shared_ptr<T> Singleton<T>::_instance = nullptr;

```

- 新特性


C++11 引入新特性使得单例模式的实现更加简单和安全。

在许多情况下，使用局部静态变量的方式已经足够满足需求，而不再需要使用复杂的单例模板类。

```cpp
class Singleton {
public:
    // 获取单例
    static Singleton& GetInstance() {
        static Singleton s; // 局部静态变量的实例 就可以作为单例返回
        return s;           // 返回实例的引用
    }
   	 // 禁止拷贝构造和赋值操作
    Singleton(const Singleton&) = delete; 
    Singleton& operator=(const Singleton&) = delete; 
private:
    // 构造函数私有化，禁止外部创建实例
  singleton_t() {}
  ~singleton_t() {}
};
```





# const

## 使用

`const`关键字用于声明常量，表示变量定义后不能修改。

1. 声明常量变量

```cpp
const int maxScore = 100; // 不能修改
```

2. const修饰指针

详见 指针-const修饰指针

3. 常量引用

详见 引用-常量引用

4. 常量成员函数

在类中，可以使用`const`声明成员函数，表示该函数不会修改类的成员变量：

```cpp
class MyClass {
public:
    void display() const {// 不能修改任何成员变量 }
};
```

5. 常量参数

可以将参数声明为`const`，以避免在函数中意外修改传入的变量：

```cpp
void printValue(const int value) {
    // value = 10; // 错误，不能修改参数
}
```

6. 常量表达式

使用`constexpr`可以定义编译时常量，适用于可以在编译时求值的表达式：

```cpp
constexpr int square(int x) {
    return x * x;
}
```

## 编译和跨文件处理

- 编译时替换

对于编译时已知值的 `const` 变量，如 `const int bufSize = 512;`，编译器会在代码中用到 `bufSize` 的地方直接替换成 `512`，这是一种优化手段，避免在运行时读取内存。

- 内部链接（Internal linkage）

默认情况下，`const` 变量只在声明它的源文件内可见，不会被其他文件访问。即使多个文件中定义了同名的 `const` 变量，编译器也会视为不同的变量。这是因为默认的 `const` 变量拥有内部链接。

- 跨文件共享同一个 `const` 变量

当你在多个文件中包含同一个 `const` 变量时，**如果不使用 `extern`，则每个文件都会创建自己的独立变量副本**。而使用 `extern` 声明后，多个文件共享同一个变量实例，且该变量只会在一个地方定义。

第一步：在头文件 `global.h` 中声明 `const` 变量

```cpp
extern const int bufSize2; // 声明一个外部的const变量
```

第二步：在一个源文件 `global.cpp` 中定义该 `const` 变量
```cpp
const int bufSize2 = 10; // 在global.cpp中定义变量
```

第三步：在其他文件中使用该变量
你可以在其他文件（例如 `main.cpp`）中包含 `global.h`，从而访问 `bufSize2`，此时它们都指向同一个变量。



## 顶层const/底层const

- **顶层 `const`**：修饰变量本身，表示变量或指针本身不可修改  是常量  所以可以做右值
  
  ```cpp
  const int a = 10;  // a 是常量，不能修改
  int* const p = &a;  // p 是常量指针，不能修改指向
  ```
  
  顶层const赋值给别人等于右值   如 const int 赋值给别人是int类型
  
  ```cpp
  const int a = 10;
  auto b = a;   //b为int类型 
  ```
  
- **底层 `const` 的特点**
  
  1. **指针指向的内容是常量**：
  
     ```
     const int *p = nullptr; // 底层const
     ```
  
     - 这里 `*p` 是底层 `const`，表示指针 `p` 指向的内容不能修改。
     - 但是指针 `p` 本身可以指向其他地址。
  
  2. **引用绑定到的内容是常量**：
  
     ```
     const int &ref = 10; // 底层const
     ```
  
     - `ref` 是一个引用，引用绑定的内容是常量，即无法通过 `ref` 修改值。
     - 这里的 `const` 修饰的是引用绑定的对象。

## const修饰指针类型别名

- typedef /using

因为是别名 const pstring就是const修饰了 char *   表示整个指针是常量

而const char * 是const修饰char 

```cpp
typedef char * pstring;
pstring a = 0; //char * a = 0;

const pstring cstr = 0; //char * const cstr = 0;
const char * cstr1 = 0;

const pstring *ps = 0; //char * const * ps = 0;
const char ** ps1 = 0;
```

- define


define只是简单的宏文本替换  没有上述问题  但是要注意定义多变量

```cpp
#define ptype int*;
ptype p1,p2;            // 即int* p1, p2;  p1为指针，p2是个int值
```



## const修饰成员函数

表示该函数不会修改类的成员变量（除非成员变量是 `mutable` 类型）

```cpp
class MyClass {
public:
    void print() const {  // 成员函数不可修改对象状态
        std::cout << value << std::endl;
    }
private:
    int value = 42;
};
```



## constexpr

## 常量表达式

值不会改变并且在**编译过程**就能得到计算结果的表达式

字面值属于常量表达式，用常量表达式初始化的`const`对象也是常量表达式

```cpp
    //max_files是一个常量表达式
    const int max_files = 20;
    //limit是一个常量表达式
    const int limit = max_files + 10;
    //staff_size不是常量表达式,无const声明
    int staff_size = 20;
    //sz不是常量表达式,运行时计算才得知
    const int sz = GetSize();
```

这样很难分辨一个值是不是常量表达式  可以用c++11特性 constexpr

## constexpr	

constexpr变量

声明在**编译时**求值的变量，这些变量在程序的整个生命周期中都是常量

```cpp
constexpr int x = 10;  // x 是一个常量表达式
constexpr int y = x + 20;  // y 也是常量表达式
```

与指针

const int 表示了指针指向 不可修改的int型

constexpr int 表示指针是常量表达式不可修改 指向int型

```cpp
const int * p = nullptr;

constexpr int *q = nullptr;
```



constexpr函数



constexpr对象



constexpr与常量表达式

```cpp
constexpr int array_size = 100;
int arr[array_size];  // 常量表达式 编译时确定大小
```



# try catch

```cpp
#include <iostream>
#include <stdexcept> // std::runtime_error
int main() {
    try {
        int a = 10,b = 0;
        if (b == 0) { // 可能引发异常的操作
            throw std::runtime_error("除数不能为零"); // 抛出异常
        }
        int result = a / b;
        std::cout << "结果是: " << result << std::endl;
    } catch (const std::runtime_error &e) {// 处理运行时错误
        std::cout << "捕获到异常: " << e.what() << std::endl;
    } catch (...) {// 处理所有其他类型的异常
        std::cout << "捕获到未知异常" << std::endl;
    }
    return 0;
}
```

1. **`try`块**：包含可能会抛出异常的代码。在这个例子中，如果`b`的值为零，就会抛出一个`std::runtime_error`类型的异常。

2. **`throw`语句**：用于抛出异常。在此示例中，`throw std::runtime_error("除数不能为零");`会抛出一个运行时错误。

3. **`catch`块**：捕获并处理抛出的异常。根据不同的异常类型，可以有多个`catch`块。在这个示例中，捕获了`std::runtime_error`类型的异常，并打印出异常信息。

4. **通用捕获**：使用`catch (...)`可以捕获所有未特定处理的异常。



# static

static成员变量

不属于任何对象  属于类  类成员变量   类中声明  通常在非内联文件中定义(.cpp)

```cpp
class Scm {
public:
    static int ints;
};
int Scm::ints = 0;
```



static成员函数

不属于任何对象 属于类 

static成员函数只能访问static成员变量





















































































































​	
