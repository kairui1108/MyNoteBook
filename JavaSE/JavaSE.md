# JavaSE 基础知识点

## 一. 数据类型

### 1. 整型

- int 32 位， 4 字节 （20亿）

- byte 8 位， 1 字节

- long 8 字节， short 2字节 (声明long型须加'l'or 'L')

### 2 浮点类型

- float 32 位， 4 字节 (声明需要加 'f' or 'F')

- double 64 位， 8 字节 (小数默认为double)

**正无穷大： Double.POSITIVE_INFINITY*

**负无穷大： Double.NEGATIVE_INFINITY*

**不是数字： Double.NaN*

> **浮点数=符号位+指数位+尾数位**

> *二进制无法精确表示 1/10 就好像十进制无法精确表示 1/3*

> *如果数值计算中不允许有舍入误差，应用 BigDecimal 类，这不是基本Java类型，而是Java对象。*

### 3 char 类型

- ' ' 单引号括起来的单个字符

- \u： 转义序列 \u

> 注释中的 \u

> // \u000A is a newline

> *注释中的 \u000A 会被替换为一个换行符，从而产生语法错误*

### 4 boolean 类型

- ture / false

>*整形值不能和Boolean相互转换*

## 二. 变量与常量

### 1. 声明： 变量类型 + 变量名

- 大小写敏感

- 不能用Java保留字

### 2. 变量初始化

- 不能使用未经初始化的变量

- 必须先用赋值语句对变量显式初始化

> *变量的声明尽量靠近变量第一次使用的地方*

### 3. 常量

- 关键字 final 指示常量

> *final 修饰的变量只能被赋值一次*

### 4.枚举类型

## 三. 运算符

### 1. 算术运算符

- +, -, *, /, %

> **整数除法只会保留整数部分如： 10/3 = 3**
>
> *整数被 零除会产生异常， 浮点数被 零除将得到无穷大或 NaN*
>
> strictfp 修饰下的main所有指令都将使用严格的浮点计算

- && 短路与：如果第一个条件为 false，则第二个条件不会判断，最终结果为 false，效率高

- & 逻辑与：不管第一个条件是否为 false，第二个条件都要判断，效率低

- || 短路或：如果第一个条件为 true，则第二个条件不会判断，最终结果为 true，效率高

- | 逻辑或：不管第一个条件是否为 true，第二个条件都要判断，效率低

### 2. 数学函数与常量

- **Math 类**

```java
double x = 4;
Math.sqrt(x); // 数值平方根
double y = Math.pow(x, a); // 幂运算，x的a次幂

Math.floorMod() // 整数余数 %
Math.sin()
Math.cos()
Math.tan()
Math.atan()

Math.PI //最接近 pi 的常量
Math.E //最接近 e 的常量

Math.multiplyExcat(1000000000, 3) //会产生一个异常，而不是像数学运算符一样返回错误的值

```

### 3. 类型转换

#### 1.自动类型转换

- *低精度自动向高精度转换，没有精度损失*

- *必要时，低精度会自动转换为高精度的类型*

![类型转换](http://pic.ruikai.ltd/img/202204091639296.jpg)

![类型细节](http://pic.ruikai.ltd/img/202204091639294.png)

#### 2.强制类型转换

```java
double x = 9.997;
int nx = (int) x; //nx=9  强制类型装换通过截断小数部分将浮点转换为整型

/*
    若要对浮点数四舍五入，以得到最接近整数
    应用 Math.round() 方法
*/

int n = (int) Math.round(x); //round 方法返回的是 long 类型，仍需要 用 (int) 强转为 int 

```

> **x += 3.5**  *如果x是整型，3.5会被强转。即运算符右侧的类型与左侧不同，就会发生强制类型转换*
>
> ***x += 3.5  ==> x = (int) (x + 3.5)***
>
> *三元运算符 true ? x : y; 类型会被转换为表达式中精度最高的类型*

## 四. 字符串

### 创建String对象

> 方式一： 直接赋值

> 方式二： 调用构造器

*内存分布不一样*

![String对象](http://pic.ruikai.ltd/img/202204091639291.png)

### 1. 子串

> **substring(index, index)**

### 2. 拼接

- 可以使用 + 拼接 两个字符串

- 将多个字符串放在一起，并用一个界定符分隔，可以用静态方法

> **String.join("/", str1, str2...)**

### 3. 不可变字符串

- 不能修改字符串中某一个字符

> *若要修改字符串，可以提取要保留的子串，再与希望替换的字符拼接*

### 4. 判断字符串是否相等

> str1.equals(str2) //*不能用 == 判断，== 判断的是地址是否相等*
>
> equalsIgnroeCase() //*忽略大小写*

### 5. 码点与代码单元

- > **代码单元** 即在具体编码形式中的最小单位。
  > 比如，UTF-16 中，一个代码单元为 16 位，UTF-8 中一个代码单元为 8 位
  > 一个代码点可能由一个或多个代码单元表示。
  > 在 U+10000 之前的代码点可以由一个 UTF-16 代码单元表示，
  > U+10000 及之后的代码点要由两个 UTF-16 代码单元表示
  > 在Java中，char类型描述了 UTF-16 编码中的一个代码单元。

```java
str.length() //返回utf-16编码表示给定字符串所需要的代码单元数量
str.chartAt(n) //返回位置n的代码单元
```

- > **码点** 即代码点，在 Unicode 代码空间中的一个值，取值 0x0 到 0x10FFFF，代表一个字符。也就是一个编码表中的某个字符对应的代码值一个字符就是一个代码点，一个代码点由一个或多个代码单元组成。
  > Unicode的码点分为17个代码级别，第一个级别是基本的多语言级别，码点从U+0000——U+FFFF，其余的16个级别从U+10000——U+10FFFF，其中包括一些辅助字符。
  > 基本的多语言级别，每个字符用16位表示代码单元，而辅助字符采用连续的一对连续代码单元进行编码。

```java
str.codePointCount(0, str.length()) //返回字符串的实际长度，即码点数量 
str.codePointAt(n) //返回给定位置开始的码点
```

### 6. API

> java.lang.String

- char charAt()

- int codePoint(int index)

- int compareTo(other)

  > 按照字典顺序，如果字符串位于other之前，返回负数；之后返回正数；相等则返回零

- int indexOf(str)

- int lastIndexOf(str)

- ......

### 6. 构建字符串

- StringBuilder( ) //不是线程安全的
- StringBuffer( ) //线程安全的

![String](http://pic.ruikai.ltd/img/202204091639287.png)

![String2](http://pic.ruikai.ltd/img/202204091639288.png)

## 五. 输入与输出

### 1. 读取输入

- *标准输入流* ：System.in  （即控制台窗口）

  > Scanner = new Scanner(System.in)

- API:

  - String nextLine()

    > *读取下一行内容，允许空格，读到回车终止*

  - String next()

    > *读取输入的下一个单词，以空格作为分隔符*

  - int nextInt()

  - double nextDouble()

  - boolean hasNext()

  - boolean hasNextInt()

  - boolean hasNextDouble()

> Scanner 类不适合从控制台读取密码，可以用Console实现
> ```char[] passwd = System.console().readPassword("Password: ");```

### 2. 输出

- System.out.println()
- System.out.println()
- *格式化输出*
  ```System.out.printf("hello, %s. Next year, you will be %d", name, age)```

### 3. 文件输入与输出

#### 读取文件

- ```Scanner in = new Scanner(Path.of("myfile.txt"), StandardCharsets.UTF_8)```

  > <font color="red">```API```</font>:根据给定路径名构造一个Path

#### 写入文件

- ```PrintWriter out = new PrintWriter("myfile.txt", StandardCharsets.UTF_8)```

  > 构造器中需要提供文件名和**字符编码**

> ##### **注释：**
>
> *用命令行启动程序时可以使用shell的重定向语法将文件关联到 System.in 和 System.out*
>
> ```java Project < inputFile.txt > outputFile.txt```

**除了scanner, 还可以用 IO 流来处理文件**

## 六. 控制流程

### 1. 块作用域

- 块（复合语句），若干Java语句用大括号组合起来

### 2. 条件语句

- if (condition) statement;
- if (condition) { }; //使用块（复合语句）
- if (condition) { } else if() { } else { };

### 3. 循环

- while(condition) statement;

- do statement while (condition);

- for (int i = 1; i <= 10; i ++) { }

- 增强for：for each 循环(for each element in a)

  > *for (variable: collection) statement;*

### 4. 多重选择

- switch (choice) { case 1: ... break; case 2: ... break; default: ... break;}

### 5. 终端控制流程的语句

- break: 退出循环语句
- break + 标签: 可以用于跳出多重嵌套的循环语句
- continue: 不再执行循环体的剩余部分，立刻跳到循环首部，如果是for循环，则跳到“更新”部分

## 七. 大数

### 处理任意长度的数字序列的数值

- #### BigInteger

  > ```API```: static BigInteger valueOf(long x)  返回任意值大整数
  >
  > ```API```: BigInteger add(BigInteger other)
  >
  > ```API```: BigInteger subtract(BigInteger other)
  >
  > ```API```: BigInteger multiply(BigInteger other)
  >
  > ```API```: BigInteger divide(BigInteger other)
  >
  > ```API```: BigInteger mod(BigInteger other)
  >
  > ```API```: BigInteger sqrt()
  >
  > ```API```: int compareTo(BigInteger other)

- #### BigDecimal

  > ```API```: BigDecimal add(BigDecimal other)
  >
  > ```API```: BigDecimal subtract(BigDecimal other) 
  >
  > ```API```: BigDecimal multiply(BigDecimal other)
  >
  > ```API```: BigDecimal divide(BigDecimal other)
  >
  > ```API```: BigDecimal divide(BigDecimal other, RoundingMode mode) //如果商无限小数，第一个divide会报错，RoundingMode.HALF_UP四舍五入
  >
  > ```API```: BigDecimal compareTo()BigDecimal other
  >
  > ```API```: static BigDecimal valueOf(long x) //也可以再传入一个指数

## 八. 数组

### 1. 声明数组

- 动态初始化

  > *先声明数组*：**数据类型 数组名[]**
  >
  > *创建数组*: **数组名 = new 数据类型[大小]**


- 静态初始化

  > **数据类型[] 数组名 = { 元素值, 元素值, }**

> *匿名数组* ： **new int[] {1, 2, 3}** 

### 2. 数组的使用

1. 数组是多个相同类型数据的组合，实现对这些数据的统一管理

2. 数组中的元素可以是任何数据类型，包括基本类型和引用类型，但是不能混用。

3. 数组创建后，如果没有赋值，有默认值

   ```java
   int 0, short 0, byte 0, long 0, float 0.0,double 0.0,char \u0000, boolean false, String null
   ```

4. 使用数组的步骤 1. 声明数组并开辟空间 2 给数组各个元素赋值 3 使用数组

5. 数组的下标是从 0 开始的。

6. 数组属于引用类型

### 3. 数组拷贝

```java
Arrays.copyOf(oldArray, oldArray.length * 2) //扩容
```

### 4. 数组排序

- 冒泡排序

  ```java
  for(int i = 0; i < arr.length -1; i ++) {
    for(int j = 0; j < arr.length - 1 - i; j ++) {
        if(arr[j] > arr[j + 1]) {
            temp = arr[j];
            arr[j] = arr[j + 1];
            arr[j + 1] = temp;
        }     
    }
  }
  ```

- Arrays 的API

  > Arrays.sort(array) //优化的快速排序（QuickSort）

### 5. 多维数组 （数组的数组）

#### 1. 声明数组

- 动态初始化

  > 类型[][] 数组名 = new 类型 [大小] [大小]

- 静态初始化

  > 类型[][] 数组名 = {{ }, { }, }

#### 2. 使用

- 多重循环遍历

## 九. 类与对象

### 1. 类与对象的关系

1) 类是抽象的，概念的，代表一类事物,比如人类,猫类.., 即它是数据类型. 
2) 对象是具体的，实际的，代表一个具体事物, 即 是实例. 
3) 类是对象的模板，对象是类的一个个体，对应一个实例
4) 对象在内存中的存在形式

![对象内存图](http://pic.ruikai.ltd/img/202204091639297.png)

### 2. 对象

  - 构造一个对象： new操作符 + 构造器（构造函数）

    > new Date() //对象被初始化为当前日期和时间

  - 访问属性

    > 对象名.属性名

  - 成员方法

    > 1）提高代码的复用性
    >
    > 2）可以将实现细节封装起来，供别人调用即可

### 3. 方法调用机制

  - 程序执行到方法时，会开辟一个独立的空间（栈空间）
  - 犯法执行完毕或执行到return时，就会返回
  - 返回调用方法的地方
  - 返回后再继续执行方法后面的地方
  - main方法（栈）执行完毕后整个程序退出

### 4. 方法传参机制

  - 基本数据类型，传递的是值（值拷贝），形参的改变不影响实参
  - 引用数据类型，传递的是地址（传递也是值，但值是地址），可以通过形参影响实参

### 5. 方法重载

  - 方法名必须相同
  - 形参列表必须不同（类型或个数或顺序至少一个不同，参数名无要求）
  - 返回类型无要求

  > *方法签名*：**方法的名字和参数列表，不包括返回类型**

## 十. JAR 文件

### 创建jar文件

- jar options file1 file2

  > jar cvf jarFileName file1 file2
  >
  > > jar cvf CalculatorClasses.jar *.class icon.gif

## 十一. 文档注释

### 生成注释

- 类注释

  > import 语句之后， 类定义之前

- 方法注释

  > 方法注释放在所描述方法之前

- 字段注释

  > 只需要对公共字段（通常是静态常量）

- 通用注释

  > @author  @version 等

- 包注释

  > 不同于上面的注释直接放于源文件，包注释有两种选择
  >
  > 1) 提供一个 package-info.java 
  > 2) 提供一个 package.html 

- 抽取注释

  ```java
  javadoc -d docDirectory packageName1 packageName2
  -d 指定html都将放置于的目录
  ```

## 十二. 继承

### 访问修饰符

- public  *对外公开*
- protected  *对子类和同一个包中的类公开*
- 默认  没有修饰符，向同一个包的类公开
- private  只有类本身可以访问，不对外公开
  ![访问修饰符](http://pic.ruikai.ltd/img/202204091639292.png)

### extends

- 父类，超类， 基类
- 子类，派生类，孩子类

### 方法重写（覆盖方法）

- @override
- 子类的方法和父类的方法**名称、返回类型、参数一样**
- 子类方法不能缩小父类方法的访问权限 *public>protected>default>private*

### super关键字

- 访问父类**非**private属性与方法

- 访问父类构造器 **super(参数列表)**

  > ```注意```： 只能放在构造器的第一句，只能出现一句

- super 和 this 的比较
  ![super and this](http://pic.ruikai.ltd/img/202204091639289.png)

### 多态

- 方法的多态 

  > 方法的重写和重载体现多态

- 对象的多态

  - *多态向上转型* ```可以调用父类中的所有成员（权限）， 不能调用子类特有成员```

    > 子类对象赋给父类引用（父类引用指向了子类的对象）
    >
    > 父类类型 引用民 = new 子类类型();

  - *多态向下转型* ```只能强转父类的引用，而不是对象```

    > 子类类型 引用名 = (子类类型) 父类引用

  - 编译类型与运行类型

    > 编译类型看 “=” 左边， 运行类型看 “=” 右边

### Object类：所有类的父类

- equals 方法

  - "==": *如果判断基本类型，判断值是否相等；如果判断引用类型，判断地址是否相等*
  - equals 方法是object的方法（默认判断地址‘==’），子类往往重写用于判断内容是否相等

  ```java
  public boolean equals(Object obj) {
    if (this == obj) { return true; }
    if (obj == null) { return false; }
    if (this.getClass != obj.getClass) { return false; }
    //再向下转型
    ...
    //使用 == 判断基本类型字段（属性），使用 Objects.equals() 比较对象字段（引用类型）
    return ...
  }
  ```

- hashCode() 方法

  - Object类的默认hashCode方法是从对象的存储地址得出散列码
  - 如果重新定义了equals方法，应重新定义hashCode方法 ```Objects.hash()```

- toString 方法

  - System.out.println(x) *会调用x.toString()*

  - 数组继承了object的toString方法

    > 调用静态方法打印数组 Arrays.toString(new int[] {1,2,3})
    >
    > 要打印多维数组，需要调用 Arrays.deepToString 方法

### 抽象类

- *abstract* 关键字

  - abstract 修饰方法，表示这是抽象方法，没有方法体，需要子类实现

    > 访问修饰符 abstract 返回类型 方法名(参数列表); //没有方法体

  - 一旦类包含了abstract方法，该类必须声明为abstract类

  - 抽象类不一定要包含abstract方法

  - 一个类继承了抽象类，则必须实现抽象类的所有抽象方法，除非该类也声明为abstract类

  - 抽象类不能用private、final、static来修饰（与重写相违背）

- 模板设计模式

```java
abstract public class Template { //抽象类-模板设计模式
  public abstract void job();//抽象方法

  public void calculateTime() {//实现方法，调用 job 方法
    //得到开始的时间
    long start = System.currentTimeMillis();
    job(); //动态绑定机制
    //得的结束的时间
    long end = System.currentTimeMillis();
    System.out.println("任务执行时间 " + (end - start));
  }
}

public class AA extends Template { 
    //计算任务
    //1+....+ 800000
    @Override
    public void job() { //实现 Template 的抽象方法 job
        long num = 0;
        for (long i = 1; i <= 800000; i++) {
        num += i;
    }
  }

```

## 十三. 反射

### 反射机制

- 反射机制允许程序执行期间借助 Reflection API 获得任何类的内部信息

- 加载完类之后，堆中就会产生一个Class类型对象一个类只有一个Class对象（包含了类的完整结构信息）

- 原理示意图
  ![reflection](http://pic.ruikai.ltd/img/202204091639286.png)

  > 1.在运行时判断任意一个对象所属的类
  >
  > 2.在运行时构造任意一个类的对象
  >
  > 3.在运行时得到任意一个类所具有的成员变量和方法
  >
  > 4.在运行时调用任意一个对象的成员变量和方法
  >
  > 5.生成动态代理

### 反射相关类

- java.lang.Class

  > *代表一个类，Class对象表示在某个类加载后在堆中的对象*

- java.lang.reflect.Method

  > *代表类的成员变量，Method对象表示某个类的方法*

- java.lang.reflect.Field

  > *代表类的成员变量，Field对象表示某个类的成员变量*

- java.lang.reflect.Constructor

  > *代表类的构造方法，Constructor对象表示构造器*

### Class 类

- 1.Class类也是类，也继承了Object类
- 2.Class类对象由**系统创建**（不是new出来的）
- 3.同一个类的Class类对象，在内存中只有一份，因为类只加载一次
- 4.每个类的实例都知道自己由哪个Class实例生成的
- 5.通过Class对象可以得到一个类的完整结构
- 6.Class对象存放于**堆**中
- 7.类的**字节码**二进制数据存放于**方法区**（包括方法名，变量名， 方法代码，访问权限）

### 获取Class类对象

- 已知一个类的全类名，且该类在类路径下，可以通过Class类的静态方法forName()获取

  > ```eg```: Class cls1 = Class.forName("java.lang.Cat");
  >
  > ```应用```: 多用于配置文件，读取类全路径，加载类

- 已知具体类，通过类的class方法获取（最安全可靠，性能最高）

  > ```eg```: Class cls2 = Cat.class;
  >
  > ```应用```: 多用于参数传递，比如通过反射达到对应构造器对象

- 已知某个类的实例，通过该实力的getClass方法获取Class对象

  > ```eg```: Class cls3 = cat.getClass(); //运行类型
  >
  > ```应用```:  通过创建好的对象获取Class对象

- 其他方式

  > ClassLoader cl = 对象.getClass().getClassLoader();
  >
  > Class cls4 = cl.loadClass("类的全类名");

- 基本数据

  > Class cls = 基本数据类型.class

- 包装类,可以通过.TYPE得到Class类对象

  > Class cls = 包装类.TYPE

### 类加载

#### 1.加载方式

- 静态加载: 编译时加载相关的类（依赖性强）
- 动态加载: 运行时再加载需要的类（降低依赖性）

#### 2.类加载时机

- 创建对象时（new） //静态加载
- 当子类被加载时，父类也会加载 //静态加载
- 调用类的静态成员时 //静态加载
- 反射 //动态加载

#### 3.类加载过程

- 过程图
  ![类加载过程图](http://pic.ruikai.ltd/img/202204091639293.png)
- 各阶段任务
  - 加载阶段：JVM将字节码从不同数据源转化为二进制字节流加载到内存中，并生成Class类对象
  - 连接阶段：验证```验证Class文件的字节流信息是否符合虚拟机要求```->准备```对静态变量分配内存并默认初始化（默认初始值，如0，0L，null， false```->解析```将常量池中的符号引用替换为直接引用```
  - 初始化节点：执行类中定义的Java程序代码（静态变量赋值和静态代码块）

## 十四. 接口

### 接口是更加抽象的抽象类

- 接口不能被实例化
- 接口中所有的方法都是 *public* 方法
- 接口中的抽象方法可以不用abstract
- 接口的字段都是 *public static final* 的常量
- 除了抽象类，实现接口的类必须实现接口的所有方法

### 接口与抽象类

- 每个类只能继承一个类，但一个类可以同时实现多个接口

- 接口不能继承其他的类，但可以继承多个别的接口

  > interface A extends B, C{}

- #### 实现接口与继承类

  - 接口与继承解决的问题不同

    > 继承价值主要在于解决代码的复用性和可维护性
    >
    > 接口价值主要在于设计号各种规范，让其他类实现这些方法

  - 接口比继承更加灵活

  - 接口一定程度上实现代码解耦

### 接口的多态特性

  - 多态参数
  - 多态数组
  - 多态传递（实现的接口实现了另一个接口）

## 十五. lambda 表达式

### 语法

```java
(parameters) -> expression
或者
(parameters) -> { statements; }
```

- 可选类型声明，编译器同意识别参数值
- 可选参数圆括号，只有一个参数时无需括号，但多个参数时需要
- 可选大括号，只有一个语句时，不需要大括号
- 可选的返回关键字：如果主体只有**一个**表达式返回值则编译器会**自动返回值**，**大括号需要指定**表达式返回一个值

## 十六. 内部类

### 内部类的分类

- 定义在外部类的局部位置（方法中、代码块）

  > (1)局部内部类 （有类名）
  >
  > (2)**匿名内部类**（没有类名）

- 定义在外部类的成员位置

  > (1)成员内部类
  >
  > (2)静态内部类 （static）

### 局部内部类

- 可以直接访问内部类的所有成员，包括私有的
- 不能添加访问修饰符，相当于一个局部变量，但可以用final
- 作用域仅在定义它的方法或代码块
- 外部类和局部内部类的成员重名时，要访问外部类的成员时可以使用 （外部类名.this.成员）

### 匿名内部类

- 既是一个类的定义，同时本身也是一个对象
- 可以直接访问内部类的所有成员，包括私有的
- 不能添加访问修饰符，相当于一个局部变量
- 匿名内部类不能有构造器，但可以提供对象初始化代码块
- 作用域仅在定义它的方法或代码块
- 外部**其他类**不能访问匿名内部类
- 常用于参数传递

```java
//基于类的匿名内部类
Father father = new Father("jack") {
    @Override
    public void test() {
        //匿名内部类重写了方法
    }
}

//基于抽象类的匿名内部类
//基于接口的匿名内部类
new Comparator() {
    @Override
    public int compare() {
        //重写方法
    }
}
```

### 成员内部类

- 成员内部类定义外部类的成员位置，并且没有static
- 可以添加访问修饰符
- 作用域与其他成员变量一样
- 外部类访问成员内部类时须创建对象再访问
- 外部类和局部内部类的成员重名时，要访问外部类的成员时可以使用 （外部类名.this.成员）

### 静态内部类

- 定义于外部类的成员位置，并且有static修饰 （有static修饰的成员内部类）

## 十七. 异常

### 执行过程中所发生的异常事件可以分为两大类

- Error（错误）：JVM无法解决的严重问题，如StackOverflowError和OOM

- Exception：因编程错误或偶然的外在因素导致的一般性问题

  - 运行时异常

  > 编译器检查不出来，一般是编程时的逻辑错误

  - 编译异常

  > 编译器要求的必须处置的异常，否则不能通过编译

  ![exception体系图](http://pic.ruikai.ltd/img/202204101510019.png)

### 异常处理

- try-catch-finally

  > 捕获异常，自行处理

  1) 如果try块中没有出现异常，则执行try块中的所有语句，不再执行catch块，若有finally，最后还要执行finally块中语句
  2) 如果出现了异常，则try块中剩下的语句不在执行，将执行catch块，最后执行finally块

```java
try{
    return 1;
} catch Exception e {
    return 2;
} finally {
    return 3;
}
//try 块中没有出现异常，catch块不执行，因为有finally块中的return（finally必须执行），所以finally中return执行，try中return不执行

try{
    //出现异常   
    return 1;
} catch Exception e {
    return 2;
} finally {
    return 3;
}
//try 中出现异常，try中return不再执行， 又因为finally有return，所以catch中return不执行，finally中return被执行

try{
    //出现异常    
    return 1;
} catch Exception e {
    int a = 1;    
    return a;
} finally {
    a += 1;
}
//try 中出现异常， catch被执行，执行到return时会将 a = 1保存为临时变量 temp = 1;最后finally修改后再执行catch块中的语句，并将临时变量返回，而不是修改后的a
```

- throws/throw

  > 抛出异常，交给调用者处理
  >
  > throw和throws的区别
  > ![img](http://pic.ruikai.ltd/img/202204101535916.png)

- try-with-resources（带资源的try语句）

```java
try (Resource res = ...) //res实现了Closeable接口（AutoCloseable的子接口）
{
    work with res ...   
}
```

  > try 退出时，会自动调用res.close(),自动关闭资源（无论是否出现异常）
  >
  > try-with-resource也可以有catch、finally语句，这些语句将在资源被关闭后执行

### 自定义异常

1) 自定义类继承Exception或RuntimeException
2) 继承Exception则属于编译异常
3) 继承RuntimeException则属于运行异常

```java
class AgeException extends RuntimeException {
    public AgeException(String message) {
        super(message);
    }
}
```

## 十八. 泛型

### 泛型的应用

- 在编译时通过一个标识表示类中某个 属性/方法/参数 的类型
- 编译时，检查添加元素的类型，提高安全性
- 减少类型转换的次数，提高效率

### 泛型的语法

#### 1.泛型的声明

- 泛型类

  > *class 类名<K, V> {}*
  >
  > *interface 接口<T> {}*

- 泛型方法

- > 泛型方法可以定义于普通类或泛型类（区别方法使用泛型）
  >
  > *public static <T> T getMiddle(T... a) { }*

#### 2.泛型的使用

- 实例化

  > *在类名后面指定类型参数的值（类型）：* 
  >
  > List<String> strList = new ArrayList<String> ();

- 调用泛型方法

  >*调用泛型方法时，可以把<具体类型> 放在方法名***前面**：
  >
  >类.<string>getMiddle()

### 泛型使用细节

- 参数类型只能是引用类型，不能是基本类型

- 不能创建参数化类型的数组

- 在给泛型指定具体类型后，可以传入该类型或者其子类类型

- 没有指定类型是，默认泛型是 Object

- 静态方法不能使用类的泛型

  > 静态和类相关，类加载时，对象还没创建，如果静态方法使用了类的泛型，JVM 就无法完成初始化

- 泛型不具备继承性

  ```List<Object> list = new ArrayList<String>(); error```

### 通配符

- <?> : 表示支持任意泛型
- <? extends A>: 支持A 类及A 类的子类，规定了泛型的上限
- <? super A>: 支持A 类及A 类的父类，不限于直接父类，规定了泛型的下限

### 类型擦除（伪泛型）

- Java语法上支持泛型，但在编译阶段会惊醒“类型擦除”，将所有的泛型替换为具体的类型
- 消除类型参数声明，即删除`<>`及其包围的部分。
- 根据类型参数的上下界推断并替换所有的类型参数为原生态类型：如果类型参数是无限制通配符或没有上下界限定则替换为Object，如果存在上下界限定则根据子类替换原则取类型参数的最左边限定类型（即父类）。
- 为了保证类型安全，必要时插入**强制类型转换**代码。
- **自动产生“*桥接方法*”**以保证擦除类型后的代码仍然具有泛型的“多态性”。

## 十九. 集合  

### 集合框架体系

![集合框架体系图](http://pic.ruikai.ltd/img/202204131921290.png)

### 迭代器 Iterator

- next(), hasNext(), remove()

- 可以认为Java迭代器位于两元素之间

  > 当调用next 时，迭代器越过下一个元素，并返回越过的元素的引用，remove方法则删除上一次调用next返回的元素

### Collection 接口

- 有些Collection的实现类可以存放重复元素，有些不可以

- Collection的实现接口 List 是有序的， Set 是无序的

- Collection 没有直接的实现子类，是通过它的子接口List 和 Set 来实现的

- #### Collection接口的元素遍历方式

  - 1.使用迭代器Iterator
  - 2.增强for循环（简化版的iterator）

### List 接口

- List集合类中元素有序，且可重复

- List集合支持索引

- 常用方法

  - void add(int i, E element)
  - void addAll(int i, Collection<? extends E> elements)
  - E remove(int i) //删除指定位置元素并返回该元素
  - E get(int i) 
  - E set(int i, E element)
  - int indexOf(Object element)
  - int lastIndexOf(Object element)

- #### List 接口的元素的遍历方式

  - 1.iterator迭代器
  - 2.增强for
  - 3.普通for + 索引

#### List 实现类 ArrayList

- 底层维护的是一个动态的数组
- 线程不安全的， Vector与其基本等同，除了Vector是线程安全的
- 创建和扩容流程 *Debug*
  - 调用无参构造器时，车市elementData容量为零，第一次添加元素时扩容为10， 若再次扩容，则扩容**1.5倍**
  - 调用有参构造器时指定容量，则出书elementData容量为所指定的大小，若再次扩容，也是扩容**1.5倍**

#### List 实现类 LinkedList

- 底层维护了一个双向链表
- LinkedList中维护了两个属性first， last分别指向 首节点和尾节点
- 添加和删除效率高

### Set 接口

- Set集合类中元素无序，且不允许重复，最多只能有一个null

- Set集合类不能通过索引获取

- #### Set 接口的元素遍历方式

  - iterator 迭代器
  - 增强for

#### Set接口实现类 HashSet

- 底层是 HashMap（value 值都为空）
- 不保证顺序，更具hashcode确定索引
- 不能有重复元素，且只能有一个null

#### Set接口实现类 LinkedHashSet

- 是HashSet子类
- 底层是LinkedHashMap，维护了一个数组 + 双向链表
- 根据hashCode确定元素的存储位置，同时使用链表维护元素的次序

### Queue 接口

- 双端队列Deque接口

- ArrayDeque和LinkedList类实现了Deque接口

- 常用方法

  - add()
  - offer()

  > 入队，将给定元素添加到队列的队尾，如果成功就返回true，若队列已满，add会抛出异常，offer会返回false

  - remove()
  - poll()

  > 出队，若队列不为空，删除并返回队列头的元素，若空队列，remove抛出异常，poll返回null

  - element()
  - peek（）

  > 返回队列头元素但不删除，若空队列，第一个抛出异常，第二个方法返回null

### Map 接口

- Map 与Collection 并列存在，用于保存具有映射关系的元素

- key 和 value 可以是任意引用类型的数据

- key不允许重复，value可以重复

- key和value都可以为null，但key中只能有一个null

- 常用String类作为key

- #### Map 接口元素的遍历方式

  - map.keySet()  -> 返回所有的key，再通过map.get(key)获取value

    - 增强for 
    - 迭代器

  - 取出所有的values map.values() 

    - 增强for
    - 迭代器

  - 通过EntrySet获取 k-v (Map.Entry<K, V>)  ==》 Set set = map.entrySet()

    - 增强for
    - 迭代器

    > Map.Entry 提供的 getKey() 和 getValue()

#### Map接口的实现类 HashMap

- 底层维护的是  数组 + 链表 + 红黑树
- 线程不安全
- 若添加相同的Key，会覆盖原来的Value
- 底层机制 Debug
  - 1.HashMap底层维护了Node类型的数组table，默认为null
  - 2.创建对象是，加载因子初始化为0.75
  - 3.添加Key-Value时，通过Key的哈希值得到在table的索引，判断该索引处是否有元素，若无，直接添加；若有，比较两个Key是否相等，若相等，替换value；若不相等还需要判断是树结构还是链表结构，做出相应处理。如果添加时发现容量不足，需要扩容。
  - 4.第一次添加时table数组初始化容量为16，临界值时12（16*0.75），大于等于临界值时扩容
  - 5.以后在次扩容时table扩容为初始的两倍，临界值也发生改变
  - 6.Java8中，如果一条链表元素超过TREEIFY_THRESHOLD(默认8)，并且数组table大于等于MIN_TREEIFY_CAPACITY（默认64）时，将树华为红黑树，如果数组大小不满足，则数组扩容

#### Map接口的实现类 HashTable

- 线程安全的
- Key和Value都不能为null

#### Map接口的实现类 Properties

- 继承自HashTable
- 用于读取.properties配置文件

### Collections 工具类

- 用于操作Set、List、Map等集合的工具类
- 提供一系列静态方法对集合中元素进行排序、查询和修改等操作

## 二十. 并发基础

### 相关概念

#### 1.进程

- 进程指的是正在运行的程序的实例
- 进程是程序的一次执行过程，或是正在执行的程序
- 是动态过程，有它自身的产生、存在和消亡的过程

#### 2.线程

- 线程是有进程创建的， 是进程的一个实体，
- 线程是操作系统进行运算调度的最小单位，是进程的实际运行单位
- 一个进程可以拥有多个线程

#### 3.并发

- 同一时刻多个任务交替执行（单核cpu实现的多任务就是并发）

#### 4.并行

- 同一个时刻，多个任务同时执行（多核cpu可以实现并行）

### 线程的基本使用

#### 创建线程

- 继承Thread类

  > Thread类本身就实现了Runnable接口

- 实现Runnable接口

  > 实现Runnable接口更加适合多个线程共享一个资源的情况，且避免的单继承的限制

#### 线程状态

- NEW 

  > 新建，尚未启动的线程处于此状态

- RUNNABLE

  > 可运行，在Java虚拟机中执行的线程处于此状态

- BLOCKED

  > 阻塞，被阻塞等待监视器锁定的线程处于此状态（未获得锁）

- WAITING

  > 等待，等待另一个线程执行特定动作的线程处于此状态

- TIMED_WAITING

  > 计时等待，等待另一个线程执行特定动作达到指定等待时间的线程处于此状态

- TERMINATED

  > 终止，已退出的线程处于此状态

![线程状态转换图](http://pic.ruikai.ltd/img/202204141353597.png)

### 同步，线程的同步

#### 锁对象

1. ReentrantLock类

```java
var myblock = new ReentrantLock(); //锁对象，重入锁
myblock.lock();
try{
    do something
} finally {
    myblock.unlock();
}

ReentrantLock(boolean fair) //公平锁，倾向于等待时间最长的线程
```

2. synchronized关键字

```java
//同步代码块
synchronized (对象) { //得到对象锁才能操作代码块
    //需要同步的代码;
}   

//同步方法
public synchronized void method() {
    //需要同步的代码
}
// 同步方法（非静态的）的锁可以是this(默认)，也可以是其他对象（但要确保多线程的锁对象是同一个对象）
// 同步方法（静态的）的锁为当前类本身 lei.class

```

#### 释放锁

- 当前线程的同步方法、同步代码块执行结束
- 当前线程执行同步代码块、同步方法中遇到break、return时
- 当前线程执行同步代码块、同步方法中出现了未处理的Error或Exception，异常结束
- 当前线程在同步代码块、同步方法中执行了线程对象的wait()方法，当前线程暂停，并释放锁