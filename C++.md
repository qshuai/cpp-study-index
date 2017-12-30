# C++ primer plus读书笔记

### 基本知识

- 函数原型和函数定义：原型只描述函数接口，包括函数接受信息和返回信息；而函数定义是函数处理的代码；C和C++将库函数的这两个特性（原型和定义）分开了；库文件包含了函数的编译代码，而头文件中则包含了原型。
- 程序的其他部分是不会调用main()方法的，但是main()返回int值，这里会引起歧义，故在这里我们可以把计算机操作系统看作是调用程序，int值返回给了操作系统。
- 自然长度：指的是计算机处理起来效率最高的长度，如果没有非常有说服力的理由来选择其他类型，则应该使用int。
- 浮点数：带小数部分的数字，计算机将其分成两部分存储，和整型数值储存方式有天壤之别；一部分表示值，另一部分用于对只进行放大和缩小。举个例子：123.2387686， 第一个数为1.232387686, 第二个数为100（放大因子）；这里只是为了理解，其实C++在表示缩放因子时是基于2的幂，而不是10的幂。浮点数的优点是能够表示更大范围的数值，但是其运算速度比整型慢，而且精度降低。
- 表达式转化为语句：只需将表达式后面加上分号就可以了，例如 `a = 5` 是表达式, `a = 5;` 是语句。
- 如果在程序代码最开头没有对所有函数进行申明，那么函数定义的顺序是有要求的，函数的定义一定要在函数调用之前定义，不然编译错误；如果在头文件之后进行了函数申明，则函数的定义顺序和位置没有规定。
- 函数重载：函数名相同，参数数量或参数类型不同，与返回值无关，这在c++中是允许的，被称为函数重载；注意，c++中如果函数名相同，参数数量和参数类型完全相同，而返回值不同，这是不允许的，编译失败，因为这种情况不在函数重载的范畴。
- c++不支持多返回值，如果有多个值要返回，需要使用数组或者其他方法。
- c++中的指针的值只能有三种情况：1指向变量， 2指向数组， 3指向0(称为空指针)；不允许其他情况存在。空指针在应用中经常作为忽略一个参数的方法，函数内可以通过判断指针是否为0(false)，`if (p)`。
- c++数组名称和字符串常量都是表示对应变量的地址，如果判断一个字符数组是否和某一字符串相等，不应写成`array="hello world"`,因为这相当于判断两个地址是否相等，答案是否定的。而应该使用strcmp()函数处理，该函数接受两个字符串地址作为参数，这意味着参数可以是字符串常量、数组名、地址。该函数在判断两个字符串相等时，返回0；前者小于后者时，返回负数；前者大于后者时，返回证书。字符判断是按照ASCII大小进行的。需要注意的是strcmp()函数，是通过结尾空值字符定义的，而不是由其所在数组的长度定义的，故在c++中，存在即使两个字符串的长度不同，但仍然相等的情况。`char array[20] = "hello world"; int res = strcmp(array, "hello world\0hello golang");` res结果为0。如果使用string类就可以省去很多繁琐的逻辑，例如：`string str = "hello world"; int b = str == "hello"`, 结果b=1;和strcmp不同的是，如果相等就返回true，即为1；如果不相等就会返回false，即为0.另外string类和字符串常量都是以空字符为结尾判定。
- c++使用argument表示实参，使用parameter表示形参。
- c++函数将数组作为参数传递的情况：`int sum(int a[], n)`;注意以下情况：`sizeof a`将返回该数组占用的字节数，即所有元素占用空间的总和；但是将数组名作为参数传递给函数时，`sizeof a`会返回改地址占用的字节数，即为4。所以在将数组作为参数传递的时候需要额外传递长度。
- c++的参数传递是按值传递的，这是c++的特性，而当参数为数组时，在函数内部能够修改数组的内容，这和c++本身按值传递的特性并不冲突，因为此时传递的值为一个地址，则可以看做一种副作用，为了防止在函数内部对数组的修改，除非函数本身的作用，可以使用const关键字，这不要求数组本身为const,如果此时还要对数组进行修改，则编译错误`read-only variable is not cassignable`。同时我们发现在对参数使用const关键字之后，这个变量具有只读的特性。
- c++允许将非const变量的地址赋值给const类型的指针，但是不能将const变量的指针赋值给非const类型的指针。
- `cin >> x >> y;`相当于`cin >> x;` `cin >> y;`
- 类型别名 	`typedef double another`，即创建了double类型的一个别名another。通常使用在对一个定义的长类型进行缩短。
- c++提供3总表示C风格字符串的方法：字符数组、字符串常量、字符串指针。
- 宏：定义一种固定格式，当使用宏时，将对应的数字替换成宏定义中的符号标记。然而宏不能按值传递，而仅仅是替换。比如定义宏：`#define SQUARE(X) X*X` 此时以下调用无法得出正确结果`SQUARE(3 + 4)`,而他的执行流程是这样的`3 + SQUARE(4)`。而C++得内联函数解决了这一问题。
- extern的作用：告诉编译器，在某个cpp文件中，存在一个函数/全局变量。
- symbol（符号）：把函数名或者全局变量名称为符号。
- 当局部变量被定义时，系统不会对其初始化，您必须自行对其初始化。定义全局变量时，系统会自动初始化为下列值.
- 字符串连接使用`+`。
- 重复字符组成字符串：const std::string str(name.size(), '*')。
- const修饰的string只能在第一次初始化的时候能够使用=运算符，之后将不能使用=和+运算符。而const int则可以使用+运算符。
- 对于连续的输入，则在两个输入之间使用空格隔开，`std::cin >> n >> m;`。
- \r表示光标回到当前行的首位。
- \t占8个字符宽度。
- 字符串操作函数strcpy(str1, str2), strncpy(str1, str2, n), strcat(str1, str2), strncat(str1, str2, n), strcmp(str1, str2), strlen(str), atof(str), atoi(str)。
- string类也可以使用strcpy(),strcat(),strcmp()函数；s.c_str()将string类转换为C风格字符串。s.assign(str, n)将C风格字符串str中的前n个字符分配到string类s中。
- string类比较可以直接使用==， >, <等比较运算符。
- string类的方法：size(), length(), empty(), substr(n, m), find(str, pos), erase(pos, n), append(str, pos, n), replace(pos, n, str, m)或replace(pos, n, str, pos1, m), insert(pos, str, n)或insert(pos, str, pos1, n).
- 数组排序方法：冒泡排序法(逐一比较并交换)、选择排序法(找到最小的元素并交换)。数组查找法：顺序查找法(循环一遍，直到找到相等元素)、二分查找法(对于有序数组的优化查找方法).
- setprecision(n)函数可以对cout输出指定有效数字位数，该函数被包含在iomanip头文件里面，使用方法为：`cout << setprecision(5);`。
- 在一个函数中throw exception可以在另一个调用者处catch到。
- 使用指针遍历数组更高效。
- 数组名称为右值，不能被赋值。
- 使用指针作为函数的参数，可以实现一个函数能够访问另一个函数的局部变量。避免使用全局变量，直接操作变量的好处是不使用返回值，当然也就不受返回值数量的限制。
- 函数指针的作用是动态的调用函数（参数列表相同，但操作不同）,函数指针的定义：double (*f) (int, double)。
- 默认c++的数组没有获取长度的方法，可以使用`sizeof(array)/sizeof(array[0])`获取。
- static的作用：一是隐藏功能，对于static修饰的函数和全局变量而言；二是保持持久性功能，对于static修饰的局部变量而言。
- explicit关键字修饰类构造函数，作用是该指定的构造函数不能隐式调用，只能显式调用。比如 Object为类，`Object o("hello")`为显示调用构造函数`Object(const char *)`；如果`Object o = "hello"`则为隐式调用。如果该构造函数使用`explicit Object(const char *)`修饰，则第二种情况将不会隐式调用。
- inline函数适用于函数代码少(没有循环等复杂结构)，频繁调用的函数。
- 字符数组只有在初始化的时候直接使用字符串赋值，其他情况则不能直接赋值。
- 没有指定类的访问控制属性，则默认为private。
- 类的默认构造函数只有在类中没有定义**任何构造函数**时编译器才会自动创建默认构造函数。
- 在应用程序的整个生命周期里，最先生成的对象最后被析构(这里的对象可以相同也可以不同)，析构栈，程序中的所有对象共用析构栈。构造函数根据程序的执行顺序依次进行。
- 将类实例化多个对象时，成员遍历分别创建，成员函数则为共享状态。
- c++指针类型：数据指针、函数指针、数据成员指针、成员函数指针。
- 类的成员函数的参数可以和类的成员变量同名，但是在引用类成员变量的时候使用this，不然默认为参数。类的成员函数默认传递this参数，形式为 classname const* this，表示此指针不能指向其他对象。如果函数后含有const修饰，则编译器翻译成const classname const* this，表示此指针不能指向其他对象而且其指向对象的值不能改变。
- 被const修饰的对象不能调用类的非const成员函数。const修饰的对象的成员变量不能被修改，但是被mutable修饰的成员变量可以被修改。被const修饰的对象在定义的时候必须对对象成员变量进行初始化。
- 类的const修饰的成员变量在构建对象之后不能被修改，但是可以通过构造函数进行初始化, 但是只能通过构造函数参数列表进行初始化。
- 类的静态成员变量需要在类声明外进行初始化赋值，格式：type classname::variable = value.
- 类的静态成员函数可以通过类名或者对象名访问，类的静态成员函数只能访问类的静态成员变量，并且静态成员函数不能被const修饰。
- 友元函数和友元类：类的友元函数声明在该类下面，该函数能够访问该类的所有成员，友元函数的定义在类的外面，或者另一个类里面，友元函数是单向的。友元类能够访问声明友元类的所有成员。关键字friend。
- 类的继承中基类的友元关系不能继承，同时基类的友元对派生类没有访问权限。
- 类的静态变量在所有派生类都只有一个对象。基类中的私有静态变量和私有变量，派生类无法访问。
- 派生类会继承基类的除私有成员、构造函数、析构函数之外的所有成员。
- 赋值兼容规则：在需要基类对象的任何地方都可以使用**公有**派生类的对象来替换。赋值兼容规则是c++多态性的重要的基础。
- 派生类的构造函数要负责对基类成员进行初始化。
- 类的多重继承格式：`class A : public B, public C{};`
- 多重继承中，基类被多次继承的问题，通过在继承的时候声明virtual基类。eg:C多重继承了B1、B2, 同时B1、B2都继承自基类A。如果`class B1 : public A{}; class B2 : public A{}; class C : public B1, public B2{};`这样就会出现基类A的构造函数被调用两次。这时候需要virtual关键字。`class B1 : virtual public A{}; class B2 : virtual public A{}; class C : public B1, public B2{};`这样共同的基类A的构造函数只会被调用1次。
- 通过virtual继承类，如果基类没有不带参数的构造函数，那么通过virtual继承的类(派生类)必须对基类进行初始化，即使此派生类被其他类继承，继承的类都需要对virtual声明继承的类进行初始化。
- C++多态包括：重载多态、强制多态、类型参数化多态、包含多态。
- 虚函数只能是类中的函数，并且不能是静态的成员函数。
- 存在虚析构函数，但不存在虚构造函数；基类的析构函数为虚函数，则所有派生类析构函数都为虚函数。
- 纯虚函数，结构为：`virtual int test(arglist) = 0;`,纯虚函数没有完整的函数定义，只是为派生类保留一个函数格式。含有纯虚函数的类为抽象类，抽象类不能被创建对象。如果派生类没有重写基类的纯虚函数，则派生类的此函数仍为纯虚函数。
- 向标准输出中输入字符串`std::fprintf(stdout, "%s", "hello");`

###奇形怪状

- C++独有的变量初始化方式：`float num(12.89);`或者 `float num = {12.89};` 相当于 `float num = 12.89;`
- unsigned本身就是unsigned int的缩写，故存在这样的写法：unsigned num = 23;
- delete只能删除new创建的内存地址;
- 数组的名称就是数组第一个元素的地址；比如a为一个数组，那么`a==&a`,然而含义却不相同，a表示第一个元素的地址，而&a这代表整个数组的地址。如果不相信可以通过一个简单的测试，`a + 1 != &a + 1`。另外可以是用`*(a + 2) = 5`为数组a中的第三个元素赋值。
- 如果给cout提供一个指针，他将打印地址，但如果指针的类型为`char *`, 则cout将显示指向的字符串，如果要显示字符串的地址，则必须将这种指针强制转换为另一种指针类型，如下 `char * input; cout << (int *) input << endl;`
- 如何访问结构体字段：如果结构标识符是结构名，则使用句点(.)运算符；如果标识符是指向结构的指针，则使用箭头(->)运算符。

### 专业名称：

- generic programming						泛型编程
- OOP-object oriented programming			面向对象编程

### 数据类型

- 基本类型

```
数值类型
	整型(包含signed和unsigned)
		char		1byte
		short		2byte
		int			4byte
		long		8byte
		long long	8byte
	
	浮点型
		float			4byte			//6位有效小数
		double			8byte			//15位有效小数
		long double	16byte			//18位有效小数
```

- 复合类型

```
数组:三个要素(元素类型、数组标识符、元素个数)
	int arrayname[5] = {1, 2};
	int arrayname[5] {1, 2};

字符串：存储在内存的连续字节中的一系列字符
	char a[12] = {'h', 'e', 'l', 'l', 'o'};		//not a string, a char array
	char a[12] = {'h', 'e', 'l', 'l', 'o', '\0'};			//a string	strlen(a)返回5，说明'\0'不计入字符长度中;sizeof(a)返回12
	char a[12] = "hello"		//字符串隐私包括结尾的空字符
	char a[] = "hello"			//字符串隐私包括结尾的空字符, 让编译器自动计算
	
	char a[12] = "hello\0word";
	cout << strlen(a) << endl;		//返回5，也就是说字符串在遇到第一个\0之后将会认为字符串结束，忽略剩余的字符
		
	//"S"和'S'是不同的，'S'为字符常量，在ACSII系统上其实是83的另一种写法；而"S"为字符'S'和'\0'组成的字符数组
	
	//长度限制：sizeof(a) >= strlen(a) + 1
	
	//cin使用空白(空格、制表符、换行符)来确定字符串的结束位置
	char a[20];
	cin >> a;
	cout << a << endl;			//输入hello world; 输出hello
	
	//cin.getline()和cin.get()能够读取输入的一行，知道换行符结束；
	//不同之处为getline()不保存换行符，在储存的时候讲换行符换成空字符\0
	
	//string对象
	string s = "hello world ";
	string t = "hello golang";
	int len = s.size();
	s += t;
	s = s + t;
	...
	
	//string类和字符数组的区别
	string s;
	char t[20];

	getline(cin, s);
	cin.getline(t, 20);

	cout << s <<endl;
	cout<< t <<endl;
	
	//字符串const指针，
	int main() {
		using namespace std;
			
		const char * variable = "hello world";
			
		cout << variable << endl;
		cout << &variable << endl;
		cout << *variable << endl;
	
		return 0;
	}
	//output:
		hello world
		0x7fff5e79ca20
		h
	//原因："hello world"实际表示的是字符串地址，因此这条语句将"hello world"的地址赋给了variable指针；
	//字符串字面值是常量，这就是为什么代码在声明中使用关键字const的原因。
	//以这种方式使用const意味着可以用variable来访问字符串，但不能修改它。

结构
	struct Person
	{
		char name[20];				//分号	另一种方式std::string name;
		unsigned char age;
		double money;
	};
	
	int main()
	{
		using namespace std;
	
		Person p =					//或在一行初始化Person p ={"Andy", 78, 23343.89};
		{
			"Andy",					//逗号
			78,
			23343.89
		};
	
		cout << p.name <<endl << p.age <<endl << p.money << endl;
	}
	
	
	//定义struct的同时创建变量
	struct Person
	{
		char name[20];				//分号	另一种方式std::string name;
		unsigned char age;
		double money;
	}onev, twov;						//onev和twov是两个变量，类型为Person struct
	
共用体
	struct Person
	{
		std::string name;
		unsigned char age;
		double money;
		union
		{
			char s_id;
			int i_id;
		};
	};
	
	int main()
	{
		using namespace std;
	
		Person p ={"Andy", 78, 23343.89};
	
		if (p.age < 100)
		{
			p.s_id = 'a';
		}else{
			p.i_id = 23;
		}
	
		cout << p.s_id << endl;
		cout << p.i_id << endl;
	}
	
枚举
	enum color{orange, pink, blue, red, green, yellow, borwn};
	//color为枚举名称；orange、pink...为枚举量，对应的值为整数0~6
	enum play{basketball = 1, football = 4; pingpong = 89};	//显式设置枚举值
	
	int main()
	{
		using namespace std;
		color one;
		one = pink;
		cout << one <<endl;
	}
	
指针
	int main()
	{
		using namespace std;
		int num = 6;
		int * p_num;
		p_num = &num;
		*p_num = *p_num +1;
	
		cout << p_num <<endl;
		cout << num <<endl;
	}	

```

注意：char和其他的整型数值不同，既不是没有符号，也不是有符号，是否有符号由C++实现决定；
如果有必要，可以显式的将类型设置为signed char或者unsigned char；

```
char foo;					//may be signed, may be unsigned
unsigned char foo;		//definitely unsigned
signed char foo;			//definitely signed
```

### New关键字

int * p = new int;				delete p;

int * p = new int [10];			delete [] p;
p = p + 1;						//p将指向下一个元素

### C++自动类型转换

- 将一种算术类型的值赋给另一种算术类型的变量时，C++将对值进行转换；
- 表达式中包含不同的类型时，C++将对值进行转换；
- 将参数传递给函数时，C++将对值进行转换。

### C++强制类型转化

-格式
	
	(type) variable			//C风格
	type(variable)			//C++风格：像函数调用一样

### 运算符

- 算术运算符

	+

	-

	*

	/		//如果操作数都为整数，这结果会省略小数部分

	%		//求模运算符的操作数必须为整数

### 进制表示

- 第一位为1~9，则为十进制
- 第一位为0，第二位为1~7则为八进制
- 如果前两位是0x或0X，则为十六进制

>其中8、10、16为基数
>
>cout默认以10进制输出，通过联合dec、hex、oct控制符使用，可以分别输出10进制、16进制、8进制格式

```
	uint num = 233;

	cout << num <<endl;
	cout << hex << num << endl;
	cout << oct << num << endl;
```

>一个字节是8个二进制位，或者2个16进制位

### 格式化

	%d %f %s %c	
	
### 编译

	//Unix
	CC main.cpp					//single source file   不支持iostream
	CC main.cpp another.cpp		//multi source file
	
	cpp main.cpp					//不支持iostream
	
	c++ main.cpp					//能支持iostream
	
### 运算符重载

	<< 位运算(左移)/输出
	>> 	位运算(右移)/输入
	&	位运算/取地址符号
	*	乘号/解引用符号

### 使用命名空间下的元素

1、 在函数外引入命名空间

```
using namespace std;

int main(）
{
	、、、			//使用std中的元素
}

void test(int n)
{
	、、、			//使用std中的元素
}

double sqrt(double d)
{
	、、、			//不使用std中的元素
}

```	

2、 在需要使用的函数内部使用

```
int main(）
{
	using namespace std;
	、、、			//使用std中的元素
}

void test(int n)
{
	using namespace std;
	、、、			//使用std中的元素
}

double sqrt(double d)
{
	、、、			//不使用std中的元素
}

```	

3、 使用命名空间中特定的元素

```
void test()
{
	using std::cout;
	
	cout << "hello world";
}
```

4、 非using形式，即在特定语句中显式调用元素

```
void test()
{
	std::cout << "hello world";
}
```

### for循环的另外一种用法

```
int main() {
    using namespace std;

    int i[5] = {23, 34, 78, 89};
    for (int a : i)
        cout << a << endl;

    return 0;
}
//output:
23
34
78
89
0


int main() {
    using namespace std;

    char * c = "hello world";

    while (*c)			//直到遇到\0
    {
        cout << *c << endl;
        c++;
    }
}
```

### 指针常量与指向常量的指针的区别

技巧：在分析到底是指针的值还是指针指向的值不能修改，我们可以先将const关键字剔除，可以清楚的看到我们定义的是一个指针规定type的指针，即变量本身是指针类型。然后将const关键字加到原来的地方，如果const修饰的是type，那么表示该指针变量指向的值是只读的；如果const修饰的指针本身，那么就表示该指针的值不能修改，也就是该地址只能指向给定的地址，而不能指向其他地址。

```
int main() {
    using namespace std;

    int i = 0;
    const int *p = &i;		//const修饰的是指针指向的值
    int *const q = &i;		//const修饰的是指针本身

    *p = 78;		//invalid
    *q = 90;		//valid
    
    int n = 90;
    p = &n;		//valid
    q = &n;		//invalid
}
```
甚至我们能够这样书写
```
int main() {
    using namespace std;

    int i = 0;
    const int *p = &i;
    const int *const q = &i;  //理解为指向const变量的const指针

    *q = 90;			//invalid

    int n = 90;
    q = &n;			//invalid

    cout << q << endl;
}
```

### 函数指针
- 函数名就是函数指针
- double *test(int) 	表示：test()是一个返回double指针的函数
- double (*test)(int)	表示：test是一个指向返回double数据的函数

```
double test(int n);

int main()
{
    double (*pf)(int);		//pf是此种类的函数，只要返回类型与参数列表完全一致
    pf = test;				//可以将函数地址赋值给pf
    (*pf)(5);					//函数调用
    pf(5);					//也可以这样调用，C++的便利
}

double test(int n)
{
    return n;
}
```

### 动态变量初始化

```
int * i = new int (34);				//基础类型初始化使用小括号
int * a = new int [4] {1,2,3,4};			//数组和结构体初始化使用大括号
student * s = new student {"andy", 34, 23434};
```

### 变量初始化

int			0
char		'\0'
float		0
double		0
pointer	NULL

### 常量定义

```
#define identifier value
const type variable = value;
```

### 字符串字面值与结束符

```
#include <iostream>

using namespace std;
int main(){
	char a[20] = "hello\0world";
	cout << a << endl;
	cout << a[10] << endl;
}

//output
hello
d
```

### try catch结构
```
#include <iostream>

using namespace std;

int main(){
	try{
		throw domain_error("you are error");
	} catch (domain_error){
        cout << "hello world";
    }
}



//在一个函数中抛出异常，可以在另一个调用处捕获
int main(){
    try{
        show();
    }catch(domain_error e){
        cout << e.what() << endl;
    }

    return  0;
}

void show(){
    throw domain_error("hello world");
}

```

### vector迭代
```
void show(const vector<string> & name) {
    for (vector<string>::const_iterator iter =  name.begin(); iter != name.end(); iter++ ){
        cout << *iter << endl;
    }
}

//简写
void show(const vector<string> & name) {
    for (auto iter =  name.begin(); iter != name.end(); iter++ ){
        cout << *iter << endl;
    }
}

//或者
void show(const vector<string> & name) {
    for(vector<string>::size_type i = 0; i != name.size(); i++){
        cout << name.at(i) << endl;
    }
}
```

### const和指针
```
    int i = 9;
    const int *p;
    p = &i;
    *p = 45;			//error
    i = 89;			//correct
    
    //以上例子要好好理解.const最重要的作用是在函数参数的修饰，被修饰的对象将无法修改，因为函数体内只能操作形参，而不能直接操作实参，故无法修改
    //概念：指向const对象的指针，指向对象的const指针，指向const对象的const指针
```
### 字符串遍历
```
    char str[] = "hello world";
    char *p = str;
    //char *p = "hello world";
    while(*p){
        cout << *(p++);
    }
```

### 隐式类类型转换
```
//隐式转换条件：
//有一个构造函数：参数只有一个，而且参数满足这样的格式 const type & name
//调用方式：类名(其他类型)
#include <iostream>
#include <string>

using namespace std;
class point{
private:
    string s;

public:
    point(const string & n){
        s = n;
    }

    void show(){
        cout << s << endl;
    }
};

int main()
{
    string s = "hello world";
    point p = point("string");
    p.show();

    p = point(s);
    p.show();

    return 0;
}
```

### 对象数组

- 构造函数至少有两个参数

	>数组的每一个元素必须在声明数组的时候初始化，不然数组初始化没有相应数据填充内存。

	```
	//correct
	Point p[3] = {Point(2, 3), Point(3, 5), Point(3, 8)};
	
	//error
	Point p[3];
	p[0] = Point(2, 3);
	```
	
- 构造函数中至少需要一个参数

	```
	//correct
	Point p[3] = {2，3，4}; //简单方式初始化：相当于p[0] = 2;
	
	//error
	Point p[3];
	p[0] = Point(2);
	```	
	
- 含有没有参数的构造函数

	>也适合构造函数参数都有默认值的情况

	```
	//correct
	Point p[3];
	```
### 多行宏定义


```
#include <iostream>

#define test(a, b)                                          \
{                                                           \
    std::cout << ((a) > (b) ? (a) : (b)) << std::endl;      \
}                                                           \


int main() {
    test(23 + 3 + 3434, 123 / 34);

    return 0;
}
```

### 迭代器

```
template<typename T>
void show(const std::vector <T> &t) {
    for (auto ii : t) {
        std::cout << ii << std::endl;
    }
}

int main() {
    int a[3] = {1, 2, 3};
    std::vector<int> t;

    t.assign(a, a + 3);
    show<int>(t);

    return 0;
}
```














