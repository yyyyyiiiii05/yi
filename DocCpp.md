# 数据类型 常量和变量

## 数据类型

数据类型定义了变量可以存储的数据的种类

**基本数据类型**：

int：整数类型。例如：`int a = 10;

float：单精度浮点数。例如：float b = 5.75;

double：双精度浮点数。例如：double c = 3.14159;

char：字符类型。例如：char d = 'A';  char 实际上是数字 通过ascii表进行转换char a = 97; char  a = 'A';

bool：布尔类型，存储true或false。例如：bool e = true;

**复合数据类型**：

array：数组类型。例如：int arr[5] = {1, 2, 3, 4, 5};

struct：结构体类型。例如：

**指针类型**：

存储内存地址的变量。例如：int* ptr = &a;

**引用类型**：

是已有变量的别名。例如：int& ref = a;

## 常量

### 字面常量

1.不带后缀 根据数据大小来确定字面量类型

13默认是int型 如果数大就按大小来确定数据类型

2.后缀来指定类型

U  L  UL  ULL  F  D

20050512L

48UL

### 字符串常量

用双引号就是字符串常量,不能修改

cout << "yiyiyi"<<endl;

### const修饰常量

```cpp
const修饰就不能修改

const修饰常量	

const int a = 100;

指向常量值的指针

const int *p = &a;

指针是常量

int * const p = &a;

指针和值都是常量

const int * const p = &a;
```

### 枚举常量

枚举类型通常用于表示一组相关的常量值，从而**提高代码的可读性和可维护性**。

将整形元素符号化 便于理解代码  如 case 1; 可以写成case Red;

```cpp
	enum Color {
    RED,
    GREEN,
    BLUE
	};
```

默认从0开始 也可以自己定义  不定义默认递增

```cpp
enum Color {
    RED = 1,
    GREEN,
    BLUE
};
```

也可以的用枚举类型来声明变量

```cpp
Color c = RED;
cout << c1 << endl;  // 输出1
```



## 变量

变量是用于存储数据的**命名存储位置**，其值在程序运行过程中可以改变





# 指针

## 指针

及时初始化或设为空指针 

int * p = null;

int * p = nullptr;

**指针运算**

具体用法 和迭代器一样

int num = 10;

int *p = & num;

p++;

p会增加4个字节

int num2 = 20

double * p2 = &num2;

p2= p2+4;

会增加4乘8  32个字节

具体用法在数组中

int v [] = {2,3,4,5,6,7};

数组v其实就是里面第一个元素的地址

```cpp
int * vp =v;

cout <<"first num is "<< *vp << endl;

cout <<"first num is "<< v[0] << endl;



cout <<"sec num is" << *(vp +1) << endl;

cout <<"sec num is" << v[1] << endl;
```

## 指针悬挂

指针指向区域已经被回收



## 动态内存管理 new delete

```cpp
int *p = new int;//申请空间    
*p = 10 ;
cout << *p <<endl;
delete p;//删除空间  


int *p = new int[5];//申请数组空间
p[0]=1;
p[1]=2;
cout << p[0] <<endl;
cout <<*(p + 1) <<endl;
delete [ ] p;//删除数组空间
```



## const修饰指针

```cpp
int a;

指向常量值的指针(常量指针)
const int *p = &a;

指针是常量(指针常量)
int * const p = &a;

指针和值都是常量(指向常量的指针常量)
const int * const p = &a;
```

总结

在*P前面就是修饰 *p  数值不能改  

在p前面就是修饰 p  指针不能改

前后都有都不能改

# 结构体

## 结构体

```cpp
struct Student
{
string name;
int age;
string gender = "顺";
};
结构体成员可以给默认值 如不赋值则使用默认
```

```
struct Student stu;

stu = {"zhuzhangyi",19,"nan"};

cout << stu.name <<endl; 

struct Student stu2 = {"张顺飞",30 ,"顺"};//声明赋值同步进行 
```

## 结构体数组

先创建结构体student

```
struct student arr[2];
//创建一个对象  是数组  数组里存这个结构体类型的对象
arr[0]= {---------};
arr[1]={---------};

struct stu arr[2]={
{---------------}
{---------------}
};
```

## 结构体指针

结构体对象是指针,存储的是另一个结构体对象的地址,一般会new开辟空间

存在结构体 Student 

````cpp
方法1  使用已存在对象地址 (很少用)
struct Student stu = {....};
struct Student *p = & stu;

方法2 (类似java new 对象  开辟空间)
struct Student *p = new  Student {"yi",18,"man"};
cout <<   *p -> name   <<endl;//通过指针访问结构体成员 用-> 不用. 
delete  p;//new 的空间记得清理
````

## 结构体指针数组

数组就是指针 

1使用已存在地址  已经创建student 结构体  创建数组对象  用指针接收数组

```cpp
struct Student arr[ ] = {{....},{....},{....}};
struct Student *p = arr;
```

2 new 出来对象  可以delete [ ] p;

```cpp
struct Student *p = new Student[3]{
{....}
{....}
{....}
};
```

# 引用

## 引用

给变量起别名  访问的是同一块内存空间

```cpp
int a = 10;
int & b = a;

```

不可以修改int & b = c;

修改a =20;

b也等于20

修改b = 30;

a也等于30

## 引用的本质

本质就是 指针常量

```cpp
int a = 10; 
int &b  = a;//实际上是 int * const b = &a;  指针指向的地址不可以改变 可以修改值
b = 20;  //*b = 20;
```



## 常量引用

修饰形参 防止误操作

有const就可以引用常量

```cpp
const int &ref = 10;//编译器修改为 int temp = 10; const int &ref = temp;
```

```cpp
void func1(const int &b){
//函数传入常量  无法 修改
cout<< b << endl;
}
int main(){
int a = 10;
func1(a);
return 0;
 }
```



# 函数

## 函数的地址传递

```cpp
void num(int  *a ,int  *b)
{
int tmp = *a;
*a = *b;  //参数a指针   **指向空间里的值**   改为b指针指向空间里的值
*b = tmp;
}
int main( )
int x = 1 , y=2;
num(&x,&y);
}
```

## 函数传入数组

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



## 函数的引用传参

函数三种传参

**值传递**:没法对实参本身产生影响

**地址传递**:可以对实参本身产生影响,但指针写起来麻烦

**引用传递**:像普通变量那样操作,对实参本身可以产生影响

由于a是 x 的引用，函数中的任何修改都会直接反映在 x 上

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

## 函数返回引用

不能返回局部变量的引用  用static

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
func1() = 100;
//返回值是个引用  也就是int &a=100;
```



## 函数返回指针

正常返回值 就算空间被清理  值返回了 就行了   

返回指针 函数结束 空间被清理  外面就无法用指针访问到内容  

所以函数返回指针 格外注意作用域问题

```cpp
int * func(){
	int *a = new int;//记住delete
	*a = 8;
	return a;
}
delete a;
```

##  局部变量的作用域

```cpp
1 手动new空间  记得delete 
int * add (int a, int b ){
int * sum = new int;
*sum =  a + b;
return  sum;
} 
delete --------------------------

2 static修饰
static int sum;
return & sum;
程序结束自动释放
```

## 函数返回数组

本质上就是返回指针  用上面方式  注意变量作用域	

1.static 

2.new delete 动态内存管理

## 函数默认参数

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

## 函数占位参数

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

## 函数重载

函数名相同 参数不同(类型不同,个数不同,顺序不同) 返回值相同

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



# 内存四区

## 程序运行前

### 代码区

存放代码 

特点 :共享 只读

### 全局区

全局变量

静态变量 static

常量(const修饰的全局常量,字符串常量)

## 程序运行后

### 栈区

由编译器自动释放

存放函数的参数值,局部变量

### 堆区

由程序员分配释放   运行结束系统释放

new在堆区开辟内存

# 类和对象

## 封装

### class

类里面可以根据权限分区

也是有属性和行为(方法)

**访问权限**

public     

成员 类内可以访问  类外可以访问

protected    

成员 类内可以访问  类外不可以访问   

继承子类可以访问父类protected成员  和private区别

private

成员 类内可以访问 类外不可以访问

```cpp
//创建类 
class Person
{
    public://访问权限
    string name;  //属性
    
    void Hi()    //行为
    {
        cout<<"Hi"<<endl;
    }

    protected: 
    string gender;

    private:
    int password;
};

   int main(){
    Person a;
    a.name="yi";
    a.Hi();
    cout<<a.name<<endl;

    //a.gender = "women";错误 protected无法访问

    return 0;
}
```



   



### struct 和class区别

struct默认是public

class默认是private

```cpp
struct C1
{
  int a;
};

class C2
{
  int b;
};

 int main(){
 C1 c1;
 c1.a = 1;

  C2 c2;
  c2.b = 1;//报错  class默认private
     
  return 0;
 }

```



### 成员属性私有化

将对象的属性private，同时提供public访问方法来控制对这些属性的访问和修改

对属性使用set  get方法 

就是封装      		

```cpp
//创建类 
class Person
{
  public:
  void setName(string name)
  {
    perName = name;
  }
  string getName()
  {
    return perName;
  }

  private://先私有

    string perName; //可读可写 set get
    
    int perAge = 18;//只读 get  

    int perPassword;//只写 set
};
int main(){
  Person p;
    
  p.setName("yi");
  cout<<p.getName()<<endl;
  return 0;
}
```



## 类和对象初始化

### 构造函数与析构函数

构造函数 创建对象

析构函数 清理堆中内容  如创建对象new出来的空间 在析构函数中delete

```cpp
class Person
{
  public:
    //构造函数  可以重载 可以有参数  如果不写 系统会默认生成
    Person()
    {
        cout <<"执行构造函数"<<endl;
    }
    
    //析构函数 不能重载 不能有参数 如果不写 系统会默认生成
    ~Person()
    {
cout <<"执行析构函数"<<endl;
    }
};

int main(){
    
    Person p;
    
    return 0; 
}
```



### 构造函数分类及其调用

```cpp
class Person
{
  public:
   int age;
  //默认构造函数
    Person()
    {
        cout <<"guozao"<<endl;
    }
    //有参构造
    Person(int a)
    {
      int age = a;
      cout <<"youcanguozao"<<endl;
    }
    //拷贝构造函数  传进来是引用常量对象	
    Person(const Person &p) 
    {
      age = p.age;
      cout<<"拷贝"<<endl;
    }
    
    ~Person()
    {
cout <<"jiexi"<<endl;
    }
};
//构造函数调用
void test01()
{
  //1.显示法
  Person p1;
  Person p2 = Person(10);
  Person p3 = Person(p2);
  //2.括号法
  Person p1;//默认无参
  Person p2(10);//有参
  Person p3(p2);//传入对象调用拷贝构造函数
  //3.隐式转换法
  Person p4 = 10;//相当于 Person P4 = Person(10);
  Person p5 = p4;
}

int main(){
  test01();
    return 0;
}
```



### 拷贝构造函数三种用途

现在编译器优化了 2 和 3 情况      编译器会尽量避免调用拷贝函数

1 复制对象 

```cpp
// 拷贝函数的用途
//1.使用一个已经创建完毕的对象来初始化一个新对象
void test01()
{
  Person p1(20);
  Person p2(p1);

}
```



2 将函数传入参数对象复制

```cpp
//2.值传递的方式给函数参数传值
void doWork(Person p)
{

}

void test02()
{
  Person p;
  doWork(p);//这个函数 传递对象 实际上是使用拷贝构造函数 传递复制对象 不会对对象本身产生影响
}



```



3 将返回函数返回对象复制

```cpp
//3.值方式返回局部对象
Person doWork2()
{
  Person p1;
  return p1;//并不会返回p1 而是拷贝新的对象返回
}
void test03()
{
  Person p = doWork2();
}
```



### 构造函数调用规则

一个类默认会有三个函数

默认构造函数 (无参)

默认析构函数  (无参)

默认拷贝构造函数  (默认对所有属性进行拷贝)



写了有参构造 就不提供无参构造

写了拷贝构造函数  编译器不会提供其他默认构造函数

写了拷贝构造函数  不写构造函数 会报错  系统不会生成默认构造函数



### 深拷贝与浅拷贝

**浅拷贝**

默认拷贝函数对对象中的所有成员进行逐字节拷贝

包括指针和动态内存地址

浅拷贝后的对象和原对象共享同一块内存区域

```cpp
class MyClass {
public:
    int* data;
    MyClass(int value) {
        data = new int(value);
    }
    ~MyClass() {
        delete data;
    }
};

// 浅拷贝示例
MyClass obj1(10);
MyClass obj2 = obj1; //默认拷贝函数   
                                   // obj2是obj1的浅拷贝，obj1和obj2的data指向同一块内存

```



**深拷贝**

深拷贝主要用于类中包含动态分配的资源（如指针、动态数组、文件句柄等）时，确保每个对象都有自己的独立副本，而不是简单的指针复制

实现深拷贝，需要**自定义拷贝构造函数**和**赋值操作符**。

```cpp
class MyClass {
public:
  int* data;

  //构造函数 传入一个值  获得地址给对象的data属性
  MyClass(int value) { 
    data = new int(value);
  }

    //自己实现拷贝构造函数  
    MyClass (const MyClass &p)
  {
    data = new int(*p.data);//对象中指向的动态内存进行单独分配和复制
  }

//解析函数中删除开辟的空间
  ~MyClass() {
    delete data;
  }
};
int main(){

  MyClass yi(100);
  cout<<*(yi.data)<<endl;
  MyClass shunfei(yi);
  cout<<*(shunfei.data)<<endl;

  return 0;
}
    
```



### 初始化列表

在对象创建时，直接对成员变量进行初始化，而不是在构造函数体内部进行赋值操作。

**1效率**：避免了默认构造和赋值操作，直接在成员变量初始化时完成赋值。

**2必要性**：对于常量成员、引用成员或者某些类对象成员，必须使用初始化列表来进行初始化。

**3清晰性**：提供了一种直观且明确的语法，使得成员变量的初始化顺序和方式一目了然。

```cpp
class Person {
public:

  int m_A;
  int m_B;
  int m_C;

  //传统初始化  构造函数
  Person (int a,int b,int c)
  {
    m_A = a;
    m_B = b;
    m_C = c;
  }

  //初始化列表初始化属性   
  Person(int a,int b,int c): m_A(a),m_B(b),m_C(c)
  {

  }

};
int main(){
  //构造函数
  Person p1(10,10,10);
  cout << p1.m_A<<p1.m_B<<p1.m_C<<endl;
  
  //初始化列表
  Person p2(30,20,10);
  cout << p2.m_A<<p2.m_B<<p2.m_C<<endl;
  return 0;
}
```



### 类对象成员

```cpp
class Phone {
  public:

 string m_PName;
 int m_PNum;

 Phone(string pName, int pNum):m_PName(pName),m_PNum(pNum)
 {
  
 }
};

class Person {
public:

string m_Name;
Phone m_Phone;//对象成员  须先创建对象Phone
   
                                  
   //使用初始化列表来创建成员对象                 m_Phone(pName,pNum)就相当于调用构造函数
   Person (string name,string pName,int pNum) : m_Name(name),m_Phone(pName,pNum)
   {
    //在构造函数体内赋值时，成员变量首先会调用默认构造函数进行初始化，然后再进行赋值操作。
    //这意味着成员变量会经历两次初始化：一次是默认构造，一次是赋值。
    // 使用初始化列表 可以直接在成员变量的初始状态中进行构造，避免不必要的默认构造和赋值过程。
       
   }

};

int main(){

Person yi("yi","apple",11);
cout<<yi.m_Name<<yi.m_Phone.m_PName<<yi.m_Phone.m_PNum<<endl;
 
  return 0;
}
```





### 静态成员变量

1.属于类的成员变量,所有对象的静态成员变量都再同一块内存区域中,所有实例共享同一个变量

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

(和构造函数拷贝函数没有冲突 就是类中函数的类型)

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

关键字this是一个指向非静态成员函数调用对象的指针   this本质是指针常量  指向不可以修改	

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

运算符就是函数 重载就是增加它可以运算的数据类型

### +重载

```cpp
class Person
{
    public:
    
    int m_A;
    int m_B;
    Person operator+(Person &p)//成员函数重载
    {
        Person temp;
        temp.m_A = this->m_A + p.m_A;//就相当于成员调用 所以this指的是调用的成员
        temp.m_B = this->m_B + p.m_B;
        return temp;
    }
};

    // Person operator+(Person &p1,Person &p2)//全局函数重载
    // {
    //     Person temp;
    //     temp.m_A = p1.m_A + p2.m_A;
    //     temp.m_A = p2.m_B + p2.m_B;
    //     return temp;

    // }

int main(){
    Person p1;
    p1.m_A = 10;
    p1.m_B = 10;
    Person p2;
    p2.m_A = 20;
    p2.m_B = 20;

//Person p3 = p1.operator+(p2); //成员函数重载本质  就是对象调用函数 传入另一个对象
//Person p3 = operator+(p1,p2);//全局函数本质调用
Person p3 = p1 + p2;//但是都可以写成这种形式
cout<<p3.m_A<<"---------"<<p3.m_B<<endl;

    return 0;
}


```





### <<左移运算符重载

```cpp
class Person
{
    public:
    int m_A;
    int m_B;

};

ostream & operator<<(ostream &out ,Person p)
{
    cout << p.m_A << p.m_B;
    return out;
}


int main(){
    
    Person p;
    p.m_A = 10;
    p.m_B = 10;

    cout << p << endl;

    return 0;
}

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



### 函数调用运算符重载  ( )    仿函数

```cpp
class MyPrint
{
    public:
    void operator()(string test)//仿函数 也是成员函数 通过对象调用
    {
        cout<<test<<endl;
    }
};

class Add
{
    public:
    int operator()(int num1,int num2)
    {
        return num1+num2;
    }
};

int main()
{
    MyPrint myPrint;
    myPrint("helloworld");

    Add add;
    int a = add(2,3);//创建对象调用
    int b = Add()(100,100);//Add()创建匿名对象 调用仿函数 也就是对象才能调用的函数
    cout<<a<<endl;

    return 0;
}
```



# 继承

### 继承语法和继承方式

继承方式只会缩小成员（包括成员函数和成员变量）在子类中的权限

protected会改变public成员  private会改变public成员和protected成员

 ```cpp

class Base {
public:
    int publicVar;
    void publicFunction() {
        cout << "Public Function" << endl;
    }
protected:
    int protectedVar;
    void protectedFunction() {
        cout << "Protected Function" << endl;
    }
private:
    int privateVar;
    void privateFunction() {
        cout << "Private Function" << endl;
    }
};

// public 继承
class DerivedPublic : public Base {
public:
    void accessFunctions() {
        publicFunction();       // 子类可以访问
        protectedFunction();    // 子类可以访问父类中的protected成员
        // privateFunction();   // 子类不可访问
    }
};

// protected 继承
class DerivedProtected : protected Base {
public:
    void accessFunctions() {
        publicFunction();       
        protectedFunction();    
        // privateFunction();   
    }
};

// private 继承
class DerivedPrivate : private Base {
public:
    void accessFunctions() {
        publicFunction();       
        protectedFunction();    
        // privateFunction();   
    }
};

int main() {
    //类外只能访问public成员  访问其他权限需要封装
    
    DerivedPublic objPublic;//创建public继承的子类对象
    
     // 可以访问父类中的public成员
    objPublic.publicVar = 10;
    objPublic.publicFunction(); 

    
    DerivedProtected objProtected;//创建protected继承的子类对象
    
    // 父类public成员(成员变量,成员函数)在子类中访问权限缩小为protected 类外不可访问
    //objProtected.publicVar = 10; 
    //objProtected.publicFunction();
    objProtected.accessFunctions(); //子类自己的public成员

    
    DerivedPrivate objPrivate;//创建private继承的子类对象
    
    // 父类public/protected成员(成员变量,成员函数)在子类中访问权限缩小为private 类外不可访问
    //objPrivate.publicVar = 10;
    //objPrivate.publicFunction();
 
    return 0;
}

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

为了解决菱形继承中基类重复的问题，引入了虚继承。

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

## 虚函数和纯虚函数

父类指针指向子类对象 要正确调用子类的函数  父类中需要是虚函数

```cpp
class Base
{
    public:
    // virtual void speak()//加上virtual 地址先虚拟
    // {
    //     cout<<"Base"<<endl;
    // }

    // 纯虚函数  写了函数实现也用不上不如不写
    virtual void speak() = 0;
    //只要有一个纯虚函数,这个类为抽象类
    //1.无法创建这个类的对象  2.所有子类必须是重写这个函数 否则为抽象类
};
class Derived :public Base
{
    public:
    virtual void speak()
    {
        cout<<"Derived"<<endl;
    }

};

void doSpeak(Base & a)//允许父子之间的类型转换  传入子类对象
{
a.speak();//调用再确定地址是哪个的 传猫就调用猫的 传狗就调用狗的 这就是动态多态
}

int main(){

    Derived deri;
    doSpeak(deri);

    Base * base = new Derived;//父类指针指向子类对象
    base->speak();
    return 0;
}
```



## 虚析构和纯虚析构

通过将父类的析构函数声明为虚函数，

可以确保无论父类的指针指向的是父类对象还是子类对象，

正确的析构函数都会被调用，从而避免资源泄漏

```cpp
class Animal
{
    public:
    Animal()
    {
        cout<<"animal构造函数"<<endl;
    }

    virtual void speak() = 0;

    // virtual ~Animal()
    // {
    //     cout<<"Animal虚析构"<<endl;
    // }

    virtual ~Animal() = 0;//纯虚析构  
    //只要有纯虚析构 是抽象类  
    //如果父类指针指向的是父类对象 可能要清理堆空间 所以类外要实现
};
Animal::~Animal()
{
    cout<<"Animal纯虚析构"<<endl;
}

class Cat :public Animal
{
    public:
    string *m_Name;
    Cat(string name)
    {
        cout<<"cat构造"<<endl;
        m_Name = new string(name);
    }
    virtual void speak()
    {
        cout<<*m_Name<<"Cat"<<endl;
    }
    
    ~Cat()//创建父类对象指向子类 要调用子类析构函数 父类必须是虚析构
    {
        if(m_Name != NULL)
        {
            cout<<"cat析构函数"<<endl;
            delete m_Name;
            m_Name = NULL;
        }
    }
};

int main()
{

    Animal * a = new Cat("yi");//父类类型指向子类对象 这就是多态
    a->speak();
    delete a;

    return 0;
}
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
template<class NameType,class AgeType = int>//默认类型int
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





# stl

standard template library

## iterator

An iterator is **an object (like a pointer) that points to an element inside the container**

## 范围for循环 

简化的循环结构，用于**遍历** 数组或容器中的每个元素。

```
for (元素类型 临时变量 : 数组变量或容器)
{

}


int main() {
    int arr[] = {1, 2, 3, 4, 5};

    for (int a : arr) {
        cout << a << endl;
    }
    return 0;
}
```

程序会输出数组每个元素	



## container

### vector

```cpp
#include <vector>
int main()
{
    vector<int> v = {1,2,3,4,5}; //创建vector容器v
    v.push_back(10);//尾插   vector头文件自带的尾插
    
    //用头文件中size函数来遍历
    for (int i = 0;i<v.size();i++)
    {
        cout <<v[i]<<endl;
    }

    //cpp11新特征 范围for循环 
    for (int temp: v)
        cout<<temp<<endl;

    //用iterator遍历   
	for(vector<int>::iterator it = v.begin();it != v.end();it++)
    {
        cout<<*it<<endl;//iterator类似指针 解引用
    }

    return 0;
}
```



### string

### deque

双端数组

### stack

栈

### queue

队列

### list

链表

stl中的链表是双向循环列表  每个节点都有 data prev指针 next指针   是一个循环

优点:不会浪费空间  增删方便

缺点:时间空间消耗大

### set/multiset

集合

关联式容器 插入之后会自动排序  二叉树实现

set不允许有重复  multiset可以有重复

```cpp
#include <set>
set<int,Compare>s1;
class Compare                
{
    bool operator()(int v1,int v2)
    {
        return v1 > v2;
    }
};

```

### map/multimap

map中所有元素都是pair

pair中第一个元素为键值key 第二个元素为value  

关联式容器  元素根据键值key自动排序

map  key不能有重复 

```cpp
map<int,int,Compare>m;

m.insert(pair<int,int>(1,10));
m.insert(pair<int,int>(2,20));
m.insert(pair<int,int>(3,30));
class Compare        //predicate
{
    bool operator()(int v1,int v2)
    {
        return v1 > v2;
    }
};
```

## 谓词predicate

谓词（Predicate）是一个函数或函数对象，它通常用于在算法中进行条件判断。

谓词的返回值通常是布尔类型（`bool`），表示某个条件是否满足。

C++标准库中的许多算法（如`std::find`、`std::count_if`、`std::remove_if`等）都接受谓词作为参数。

## lambda表达式

算法函数的谓词 基本上只是使用一次 我们就可以用lambda表达式 创建匿名函数 cpp11新特性

```cpp
[capture](parameters) -> return_type {
    // function body
}
capture: 捕获列表，用于捕获外部变量（如 [&] 捕获所有外部变量的引用）。
			[x]捕获外部变量 x 的值。lambda 表达式内部可以使用 x，但对 x 的修改不会影响外部变量  _引用
parameters: 函数参数列表。
return_type: 返回类型（可以省略，编译器会自动推导）
function body: 函数体，定义了 lambda 的行为。
```



## functional

内建函数对象    模板创建对象  对象是函数

```cpp
#include <functional>
int main()
{
negate<int>n; //n就是创建出的函数  功能为对int进行取反
cout<<n(50)<<endl;
    
plus<int>p;
cout<<p(20,20)<<endl;
    
//vector.....
sort(v.begin(),v.end(),greater<int>())//perdicate
    
return 0;
}

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

在指定范围内查找**第一个**满足给定条件的元素  返回迭代器 未找到会返回end

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// 自定义谓词函数
bool isEven(int n) {
    return n % 2 == 0;
}

int main() {
    vector<int> vec = {1, 3, 5, 6, 7, 9};

    // 使用find_if查找第一个偶数
    vector<int>::iterator it = find_if(vec.begin(), vec.end(), isEven);

    if (it != vec.end()) {
        cout << "找到第一个偶数: " << *it << endl;
    } else {
        cout << "未找到偶数" << endl;
    }

    return 0;
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



































































































































































































