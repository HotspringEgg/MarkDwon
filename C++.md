23.12.06
#C++基础
##三大特性
###访问权限
public protected private
类内部三种成员都可以互相访问，无访问权限限制
类外部只能通过对象访问成员，且只能通过对象访问public成员，不能访问protected和private成员
public可以被类的外部访问
protected可以被子类访问，不能被外部访问
private不能被子类访问，不能被外部访问
###继承
定义：从已有的类派生出新的类，而派生类继承了原有类的特征，包括方法。
####三种方式
实现继承：使用父类的属性和方法而不需要额外编码
接口继承；仅使用属性和方法的名称，子类必须提供实现的能力
可视继承：子窗体使用父窗体的外观和实现代码的能力（eg：GUI方面）
###封装
定义：将对象的数据(属性)和操作这些数据的方法(行为)组合到一个单独的单位或类中，并对外隐藏内部实现的细节
即：把客观事物抽象成“类”，让自己数据和方法只让可信的类或者对象操作，对不可信的进行信息隐藏。例如公共的数据或方法使用public修饰，而不希望被访问的数据或方法采用private修饰。
###多态
定义：同一事物表现出不同事物的能力，即向不同对象发送同一信息。不同对象在接收时会产生不同的行为。(重载，实现编译时多态，虚函数实现运行时多态)
允许将子类类型的指针传递给父类类型的指针。
####实现的两种方式
重写：是指子类，重新定义父类的虚函数的做法。（必须是虚函数）
因为。只有声明为虚函数才可以实现多态。若不是虚函数，则直接调用父类中的该函数。若子类中没有重写，则调用父类中的该函数。

Virtual void function () cost = 0 这是纯虚函数
1.有至少一个纯虚函数的类被称为抽象类，不能直接实例化一个抽象类，也不能创建该类的对象
    实例化：通过类来创建一个具体对象
常用做接口和行为的模板，具体实现留给子类
2.强制继承要求：必须在子类中被重写
3.接口编程：定义通用接口，实现取决于派生类

重载：是指允许存在多个同名函数，而这些函数的参数表不同。

##数据类型
整形:
int     4byte   ±2的31次方
short   2byte
long    4or8byte(32:4 64:8)
long long   8byte
(1byte = 8bit)
字符型：
char    1byte
布尔型：
bool    1byte
浮点型：
float   4byte
double  8byte
空：
void    指无类型，但用作指针时，大小通常为4byte（32）或者8byte（64） 
int 为计算机处理起来最有效率的长度，一般选用int
（eg：一个结构体由一个int和一个char组成，那么大小为4+1=5byte，但考虑内存对齐，结构体会被填充到4字节的倍数，使其变成8字节。准确大小最好使用sizeof）
##指针和引用
指针是地址变量，存放所指对象的地址
本身也有地址，有指向指针的指针
可以改变所指地址，也可以改变所知地址处存放的数据

引用是变量的别名，从一而终，不可变，必须初始化

不存在指向空值的引用，但存在指向空值的指针。
##关键字
###const
被const修饰的值不能改变，只可读取。且定义的时候必须赋初值

**常量指针**：**Pointer to Constant**
const 数据类型 * 指针变量 = 变量名
数据类型 const * 指针变量 = 变量名
（const在 * 左边 ——> 常量指针）
该指针指向一个只读的对象，不能通过该指针来改变该对象的值，但可以改变该指针所指的内存空间
强调指针对其所指对象的不可变性

**指针常量**：**Constant Pointer**
数据类型 * const 指针变量 = 变量名
（const在 * 右边 ——> 指针常量）
该指针所指的内存区域是固定的，必须在定义的时候初始化
强调指针的不可变性

tip：' * '前是指针所指的数据类型，如果要为一个指针常量赋值一个常量的地址则需要在' * '前声明所指的是一个常量
const int * const p = &n
如果不在声明中指明所指的数据类型是个const则会error
比如：
const int = n;
int * p = & n;
但是常量指针可以指向一个非常量，因为常量指针的约束仅仅在于不允许通过该指针修改所指向的数据，而不要求所指向的数据本身必须是常量。
###define, typedef和inline的区别
####define
\#define是一个预处理指令，用于创建“宏”
 1. 简单的字符串替代，没有类型检查
 2. 在编译的预处理阶段起作用
 3. 可以用来防止头文件重复引用
 4. 不分配内存，给出的是立即数，有多少次使用就进行多少次替换
   
eg:
    
    #define PI 3.14159
    #define SQUARE(x) ((x) * (x))
    
    // 使用宏
    double radius = 5.0;
    double area = PI * SQUARE(radius);

####typedef
typedef是用于为数据类型创建新的类型别名的关键字。它允许为现有的数据类型定义更容易理解的名称，从而提高代码的可读性和维护性。
1. 有对应的数据结构需要进行判断
2. 是在编译和运行时起作用
3. 在静态存储区中分配空间，在程序运行过程中内存只有一个拷贝

eg:
    typedef existing_type new_type_name;
    typedef int IntArray[10];
    IntArray = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

