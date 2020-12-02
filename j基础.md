java是由sun在95年推出的高级程序设计语言，后被甲骨文（Oracle）收购
java分为三个体系：
    JavaSE - java平台标准版
    JavaME - java平台微型版
    JavaEE - java平台企业版
可运行在多个平台，如Windows、Mac OS、及其他多种Unix版本的系统

主要特性：
    面向对象 - 提供类、接口和继承等面向对象的特性
    分布式   - 支持Internet应用的开发
    健壮     - 强类型机制、异常处理、垃圾的自动收集等
    安全     - 
    可移植   -
    ...

开发环境配置：
    下载JDK后，配置环境变量
    系统变量中新增三个属性，JAVA_HOME、PATH、CLASSPATH
    (jdk1.5后不需要配置CALSSPATH环境变量)
    JAVA_HOME = "jdk安装目录"
    PATH = “%JAVA_HOME%\bin”;"%JAVA_HOME%\jre\bin"

JDK与JRE区别：
    JDK是java开发工具包，是整个java核心，包含JRE和一堆工具tool.jar和java标准类库（rt.jar）
    JRE是java运行环境，包括JVM和java核心类库等

基础语法：
    对象：对象是一个实例，有状态和行为
    类：类是一个模板，描述一类对象的行为和状态
    方法：就是行为，一个类可以有多个方法
    实例变量：每个对象都有独特的实例变量，对象状态由实例变量决定
    大小写敏感：java是大小写敏感的
    类名：类名首字母大写，若有多个单词组成，每个单词首字母大写
    方法名：方法名首字母小写，若有多个单词组成，后面每个单词首字母大写
    源文件：源文件名必须与类名相同
    主入口方法：所有java程序由public static void main(String[] args)方法开始

    标识符：
        类名、方法名、变量名都称为标识符。
        所有标识符应以大小写字母、数字、下划线、美元符组成
        标识符首字母不能是数字
        标识符大小写敏感
        标识符不能是关键字（关键字是右特殊含义的标识符，不能随意使用）

    修饰符：
        两类修饰符：访问控制修饰符、非访问控制修饰符
            访问控制修饰符：default、public、protected、private
            非访问控制修饰符：final、abstract、static、synchronized

    变量：
        局部变量、类变量（静态）、成员变量（非静态）

    数组：
        存储在堆上的对象，相同数据类型的数据集合
    
    枚举：
        1.5后引入枚举，限制变量只能为预设的值

    关键字：
        不能用于常量、变量、任何标识符的名称
        保留字 goto、const、null
    
    注释：
        用来解释和说明的文字
        单行注释 //
        多行注释 /*...*/
        文档注释 /** ...*/
    
    进制：
        x进制表示逢x进1
        1byte = 8bit

    原、反、补码：
        计算机是以二进制的补码来进行计算
        原码：最高位符号位，0表示正，1表示负，其余表示数值大小
        反码：正数的反码和原码相同，负数的反码与原码符号为相同，数值为取反
        补码：正数的补码和原码相同，负数的补码是在反码基础上加1

    继承：
        一个类可以由其他类派生，重用已存在类的方法和属性，被继承的类为超类或父类，派生类为基类或子类

    接口：
        接口可理解为对象间相互通信的的协议，接口在继承中扮演重要角色

对象和类：
    对象：是类的实例，有状态和行为
    类：是一个模板，描述一类对象的行为和状态
    一个类包含以下类型变量：
        局部变量 - 在方法、构造方法或者语句块中定义的变量
        成员变量 - 在类中，方法体之外定义的变量
        类变量   - 在类中，方法体之外定义的变量，必须声明为static类型
    构造方法：
        构造方法与普通方法类似，只是不需要返回值 方法名与类名一致
        默认java编译器会提供一个无参构造方法，如果显示的定义构造方法，默认不提供
        public class Puppy{
            public Puppy(){
            }
            public Puppy(String name){
            }
        }
    创建对象：
        对象是根据类创建的，使用new关键字创建，
        声明 - 声明一个对象，包含对象名称和对象类型
        实例化-使用关键字new来创建一个对象
        初始化-使用new创建对象时，会调用构造方法初始化对象
        public class Puppy{
            //有参构造方法
            public Puppy(String name){
                System.out.println(name);
            }
            public static void main(String[] args){
                //创建实例对象
                Puppy py = new Puppy("tom");
            }
        }
    访问实例变量和方法：
        访问类中的变量 对象名.变量名
        访问类中的方法 对象名.方法名
    
    源文件声明规则：
        当在源文件中定义多个类，并有import语句与package语句时
        - 一个源文件只能有一个public类
        - 一个源文件可以有多个非public类
        - 源文件的名称应与public类同名
        - 有package语句应定义在首行
        - 有import语句定义在package语句后面

    import语句：
        导入其他不同路径下的类

基本数据类型：
    变量是申请内存来存储值，创建内存时需要在内存中申请空间
    内存管理系统根据变量的类型为变量分配存储空间，分配的空间只能用来存储该类型数据
    java两大数据类型：内置数据类型、引用数据类型
    内置数据类型：
        八种基本数据类型：byte、short、int、long、float、double、char、boolean
        byte:
            byte数据类型是8位、有符号，以二进制补码表示的整数。-128 ~ 127，默认值为0
        short：
            short数据类型是16位、有符号，以二进制补码表示的整数。-32468 ~ 32767，默认值为0
        int:
            int数据类型是32位、有符号，以二进制补码表示的整数。-2^31 ~ 2^31 - 1，默认值为0
        long:
            long数据类型是64位、有符号，以二进制补码表示的整数。-2^63 ~ 2^63 - 1,默认值为0L或0l
        float:
            float数据类型是单精度、32位浮点数，默认值为0.0f
        double:
            double数据类型是双精度、64位浮点数，默认位0.0d
        char:
            单一的16位Unicode字符， \u0000 ~ \uffff,可存储任何字符
        boolean:
            表示一位的信息，true和false，默认值为false
    引用类型：
        引用类型是一个对象类型，值指向内存空间的引用，即地址
        对象和数组都是引用类型，所有引用类型默认值为null
    常量：
        程序运行时不可改变，final关键字修饰常量，常量名一般大写
        byte、short、int、long可用十进制、十六进制、八进制表示
        前缀为0表示八进制、前缀为0x表示十六进制
    类型转换：
        byte、short、char -> int -> long -> float -> double
        容量大的数据类型转为容量小的数据类型要进行强制转换
        变量相加存在类型转换问题，常量相加，会将结果与所存储的数据类型范围比较，在范围内不出问题
    
    ASCII:
        0       48
        'A'     65
        'a'     97

变量类型：
    声明变量格式：
        变量类型 变量名 = 变量值;
    支持同时声明多个相同类型变量，用逗号隔开
    变量类型有：
        局部变量、成员变量、类变量
        局部变量 - 声明在方法、构造方法、语句块中的变量。
            访问修饰符不能用于局部变量
            局部变量在栈上分配
            局部变量没有默认值，必须初始化才能使用
        成员变量 - 声明在类中，方法、构造方法、语句块外的变量
            对象被实例化后，每个变量的值跟着确定，跟着对象创建而创建，对象销毁而销毁
            访问修饰符可修饰成员变量
            成员变量具有默认值，整型变量为0,0L，布尔值为false，浮点数为0.0f/0.0d,引用类型为null
        类变量 - 也称为静态变量，在类中以static关键字声明，在方法、构造方法、语句块之外
            类变量，只在加载类时一份拷贝，无论创建多少对象都只有一份拷贝
            静态变量存储在静态存储区
        
修饰符：
    用来定义类、方法或者变量
    两类：访问修饰符、非访问修饰符
        访问修饰符 - 保护对类、变量、方法、构造方法的访问
            默认的，default。同一包可见，不写修饰符
            私有的，private。同一类可见,隐藏类的实现细节和保护类的数据，不能修饰类和接口
            受保护的，protected。同一包和所有子类可见，不能修饰类和接口
            共有的，public。所有类可见
        注：子类访问权限不能低于父类访问权限
        非访问修饰符 
            static - 静态变量独立于对象，只存在一份拷贝，静态方法不能访问非静态变量
            final  - 修饰类、方法、变量，修饰类不能被继承、修饰方法不能被重写、修饰变量为常量
            abstract 修饰类为抽象类，抽象类不能实例化，类不能同时被abstract和final修饰
                        继承抽象类的子类必须实现父类所有抽象方法，除非该子类为抽象子类，抽象方法没有方法体
            synchronized 声明的方法同一时间只能被一个线程访问。
            transient 修饰变量不被序列化
            volatile  修饰的成员变量在每次被线程访问时，都强迫从共享内存中重读该成员变量的值

运算符：
    算术运算符、关系运算符、逻辑运算符、赋值运算符、位运算符、其他运算符
    算术运算符：+、-、*、/、%、++、--（/需要小数只需将一个数变为浮点数，++或--单独使用没区别）
    关系运算符：==、=!、>、<、>=、<=
    逻辑运算符：&&(左右条件都为真结果为真，左条件为假，有条件不需要计算，结果为假)、||(与&&相反)、!、&、|
    赋值运算符：=、+=、-=、*=、/=、%=、<<=、>>=、&=、^=、|=
    位运算符：  &、|、^、~、<<、>>、>>>（）
    其他运算符：条件运算符？:、instanceof运算符
        
循环结构：
    while、do-while、for、java5后引入用于数组的增强型for循环
    while(布尔表达式){
        //循环体
    }
    do{
        //循环体
    }while(布尔表达式);
    for(初始化;布尔表达式;迭代){
        //循环体
    }
    for(声明语句 : 表达式){
        //循环体
    }
    break关键字 - 用于循环语句和switch语句，跳出整个语句块，
    continue关键字 - 跳过该语句后面的语句，执行下一次循环
    return关键字 - 结束方法

条件语句：
    if语句、switch语句
    if(布尔表达式){
        //布尔表达式为true执行
    }
    if(布尔表达式){
        //布尔表达式为true执行
    }else{
        //布尔表达式为false执行
    }
    if(布尔表达式1){

    }else if(布尔表达式2){

    }
    ...
    }else{

    }
    switch(表达式){
        case value1:
        //语句
        break;//可选
        case value2:
        //语句
        break;//可选
        ...
        default://可选
        //语句
    }
    注：表达式类型可为byte、short、int、char、enum、String

数组：
    用来存储固定大小的同类型数据
    数组声明：
        数据类型[] 数组名;
        如：int[] arr;
    创建数组：
        数组名 = new 数据类型[size];
     数据类型[] 数组名 = new 数据类型[size];
     数据类型[] 数组名 = {value0, value1, value2,...};
     数组的元素通过索引来进行访问，从0开始
     数组长度： 数组名.length;
     数组遍历：循环； 数组名[索引];

     冒泡排序：相邻元素两两比较，大的往后排，最大值出现在最大索引位置，从左往右重复操作直到排完
     选择排序：从起始索引0，依次和后面的元素比较，小的排在起始位置，直到排完，再从索引1开始重复操作

Java内存分配：
    栈(存储局部变量)、堆(new出来的)、方法区、本地方法区、寄存器
    局部变量:在方法定义中或方法声明上定义的变量

方法：
    方法的定义：
        修饰符 返回值类型 方法名(参数类型 参数名){
            //方法体
            retrun 返回值;
        }
    无返回值时 使用void，同时return 语句可省略
    参数可以有多个或者没有，方法是值传递不是引用传递
    方法重载：
        同一类中方法名相同，参数列表不同的方法叫方法重载，参数列表不同指参数个数、顺序、参数类型各不相同
    可变参数：
        java1.5后，支持同类型可变参数
        参数类型... 参数名
    finalize()      垃圾回收前调用，清除回收对象

Object类：
    Object类是所有类的父类，所有类都继承于Object类
    方法：
        Object clone()      创建并返回一个对象的拷贝,调用该方法要实现Cloneable接口
        equals(Object obj)  判断两个对象的引用是否指向同一个对象，即比较两个对象的  地址是否相等
        Class getClass() 获取对象的类 class java.xx.xx.className
        finalize()          默认由对象的垃圾回收器调用
        int hashCode()      获取对象的HashCode值
        notify()            唤醒在该对象上等待的线程
        notifyAll()         唤醒在该对象上等待的所有线程
        wait()              让当前线程进入等待状态 

包装类：
    Byte(byte)、Short(short)、Integer(int)、Long(long)、Float(float)、
    Double(double)、Character(char)、Boolean(boolean)
    int类型转String:
        String.valueOf(int a)
        new Integer(int a).toString()
        Integer.toString(int a);
    int类型转String:
        Integer.parseInt(String s)
    进制转换：
        Integer.toStirng(int a, int radix)  十进制转为其他进制（2-36）
    Integer直接赋值，值在-128和127之间，会直接从缓冲池中获取数据，不在范围内都会创建对象

Number & Math
    基本数据类型对应的包装类：Byte、Short、Integer、Long、Float、Double、Character、Boolean
    Byte、Short、Integer、Long、Float、Double都是抽象类Number的子类
    xxxValue()      将Number转换为对应的数据类型
    compareTo()     将Number对象与参数进行比较
    equals()        判断Number对象是否与参数相等
    valueOf()       返回Number对象指定的基本数据类型
    parseInt()      将字符串解析为int类型
    Math类：数学运算的属性和方法
    abs()           返回参数绝对值
    ceil()          向上取整
    floor()         向下取整
    round()         四舍五入
    pow()           次方
    sqrt()          算术平方根
    random()        返回0到1之间的数，不包含1

Character类：
    isLetter()      是否是字母
    isDigit()       是否是数字
    isUpperCase()   是否是大写字母
    isLowerCase()   是否是小写字母
    toUpperCase()   转为大写字母
    toLowerCase()   转为小写字母
    toString()      转为字符串

String类：
    构造方法：
    String()
    String(byte[] bytes)
    String(byte[] bytes, int index, int length)   字节数组一个部分转为字符串
    String(char[] ch)
    String(char[] chs, int index, int length)   字符数组一个部分转为字符串
    String(String str)      
    方法：
        boolean contains()          是否包含指定的字符序列
        boolean startsWith(String prefix) 字符串是否以指定前缀开始
        boolean endsWith(String suffix) 字符串是否以指定字符串结尾
        boolean equals(Object o)    比较字符串和对象
        boolean isEmpty()           字符串是否为空

        char charAt(int index)      根据索引获取字符串字符
        int length()                返回此字符串的长度
        int indexOf(char ch)        返回指定字符第一次出现的索引位置
        int indexOf(String str)     返回指定字符串第一次出现的索引位置
        int lastIndexOf(char ch)    返回指定字符最后一次出现的索引位置
        int lastIndexOf(String str) 返回指定字符串最后一次出现的索引位置
        String substring(int begin) 从指定位置截取新字符串
        String substring(int begin, int end) 从指定位置开始到指定位置结束截取新字符串(包左不包右)

        byte[] getBytes()           按默认字符集将字符串转换为byte数组
        byte[] getBytes(String charsetName) 按指定字符集将字符串转为byte数组
        char[] toCharArray()        字符串转为新的字符数组
        String valueOf(Object o)    任意类型数据转为字符串        
        String concat(String str)   字符串拼接
        String toLowerCase()        转为小写字符串
        String toUpperCase()        转为大写字符串

        int hashCode()              返回字符串哈希码
        int compareTo(Object o)     字符串和另一个对象比较
        int intern()                
        String trim()               去掉两端的空格
        String replace(char ol , char ne) 将字符串指定字符替换所有ol
        String replaceAll(Stirng regex, String replacement) 给定的replacement替换所有匹配的正则
        String[] split(String regex) 根据正则匹配拆分字符串
        
    String类不可变性：
        字符串实际上是一个char数组，并且char数组使用关键字final修饰

    String s1 = new String("123")和String s2 = "123"区别？
        前者会创建两个对象，后者会创建一个对象
    字符串如果是变量相加，先开空间，在拼接，常量相加，先相加，再去常量池找，有直接返回没有创建
    String类作为参数传递和基本类型作为参数传递是一样的

StringBuffer & StringBuilder
    因为String是不可变的，当需要修改字符串时使用StringBuffer或StrinBuilder
    StringBuffer与StringBuilder主要区别在于StringBuffer是线程安全的，所以大多数追求效率使用StringBuilder，默认容量大小16
    方法：
        StringBuffer append(String s)   将指定字符串追加到此字符序列
        StringBuffer reverse()
        delete(int start, int end)      移除
        insert(int offset, int i)
        replace(int start, int end, String str) 替换
        int capacity()                  当前容量

    String、StringBuffer、StringBuilder区别：
        String - 字符串常量，字符串长度不可变，字符串是由字符数组存储数据，而字符数组被声明为final，赋值后不可更改
        StringBuffer - 字符串变量，如果频繁对字符串内容修改，使用StringBuffer,线程安全
        StringBuilder - 字符串变量，线程不安全
        操作少量数据使用String;单线程操作大量数据使用StringBuilder；多线程操作大量数据使用StringBuffer

Arrays类:
    java.util.Arrays类提供的所有方法都是静态的，用于操作数组
    fill(int[] a, int val)   给数组赋值
    sort(Object[] a)         给数组排序
    equals(long[] a, long[] b) 比较数组
    binarySearch(Object[] a, Object key)  查找数组元素

Collections类：
    
日期时间：
    java.util包提供Date类来封装当前日期和时间
    构造方法:
        Date()
        Date(long mill)
    方法：
        boolean after(Date date)    是否在指定日期后
        boolean before(Date date)   是否在指定日期前
        long getTime();             获取毫秒数
        setTime(long time)          毫秒数设置时间
    java.text包下的SimpleDateFormat类
        SimpleDateFormat格式化日期：
            SimpleDateFormat sdf = new SimpleDateFormat(String format);
            String format(Date date);
            如：SimpleDateFormat sdf = new SimpleDateFormat(“yyyy/MM/dd HH:mm:ss”);
            // 2020/10/22 13:52:28
        SimpleDateFormat解析字符串为时间：
            Date parse(String date);
    休眠：
        Thread.sleep(long mill)     程序休眠指定毫秒数
    获取当前时间毫秒数：
        System.currentTimeMillis();
    Calendar类：
        设置和获取日期数据的特定部分，抽象类
        Calendar c = Calendar.getInstance();
        获取对象信息
        get(Calendar.YEAR)     //年
        get(Calendar.MONTH)+1  //月
        get(Calendar.DATE)     //日
        get(Calendar.HOUR_OF_DAY)//时
        get(Calendar.MINUTE)    //分
        get(Calendar.SECOND)    //秒
        get(Calendar.DAY_OF_WEEK)//星期
    GregorianCalendar类：
        是Calendar类的实现类
        构造方法：
            GregorianCalendar()
            GregorianCalendar(int year,int month,int date)
            GregorianCalendar(int year,int month,int date,int hour,int minute,int second)
        方法：
            int get(int field)  获取指定字段时间值
            Date getTime()      获取当前时间
            boolean isLeapYear(int year) 给定时间是否是闰年
    
正则表达式：

Stream、File、IO:
    什么是流？流是抽象的概念，是对输入和输出设备的抽象，在java中对数据的输入和输出操作都是以流的形式进行，可理解为一个数据序列
    什么是IO流？IO流包括输入和输出流，输入流指将数据以字符或字节形式从外部媒介读取到内存中，输出流指将内存中的数据写入到外部媒介
    读取控制台输入：
        java控制台输入由System.in完成
        BufferedReader br = new Bufferreader(new InputStreamReader(System.in));
        读取一个字符使用read();返回结束返回-1
    控制台读取字符串：
        br.readLine()；
    控制台输出：
        控制台输出由print()和println()完成，都由PrintStream定义
        PrintStream继承了OutputStream类，实现了write()

    读写文件：
        输入流用于从源读数据，输出流用于向目标写数据
        IO流：字节流、字符流
            字符流：Reader、Writer
                Reader: BufferedReader、InputStreamReader、StringBuffer、PipeReader、CharArrayReader、FilterReader
                    InputStreamReader: FileReader
                    FilterReader: PushbackReader
                Writer: BufferedWriter、OutputStreamWriter、PrinterWriter、StringWriter、PipeWriter、CharArrayWriter、FilterWriter
                    OutputStreamReader: FileWriter
                
            字节流：InputStream、OutputStream
                InputStream: FileInputStream、FilterInputStream、ObjectInputStream、PipeInputStream、SequenceINputStream、
                            StringBufferInputStream、  ByteArrayInputStream
                    FilterInputStream: BufferedInputStream、DataInputStream、 PushbackInputStream
                OutputStream: FileOutputStream、FilterOutputStream、ObjectOutputStream、PipeOutputStream、ByteArrayOuputStream
                    FilterOuputStream: BufferedOutputStream、DataOutputStream、PrintStream
        
        FileInputStream: 用于从文件读取数据
            创建对象：
                InputStream in = new FileInputStream(String filepath);
                或 File f = new File(String path);
                   InputStream in = new FileInputStream(f);
            方法：
                close()             关闭文件输入流，并释放有关资源
                int read(int r)     读取指定字节的数据，到达末尾返回-1
                int read(byte[] r)  返回读取的字节数
                int available()
        FileOutputStream: 创建文件并向文件写数据
            如果该流在打开文件进行输出前，目标文件不存在，那么该流会创建该文件。
            创建对象：
                OutputStream out = new FileOutputStream(String filepath);
                或  File f = new File(String path);
                    OutputStream out = new FileOutputStream(f);
            方法：
                close()             关闭文件的输出流，并释放相关资源
                write(int w)        把指定字节数写到输出流
                write(byte[] w)     把指定数组的字节写到输出流

    File:
        java文件以抽象的方式代表文件名和目录路径名。
        主要用于文件和目录的创建、查找和删除等
        构造方法：
            File(File parent, String child);
            File(String filepath);
            File(URI uri);
        方法：
            String getName()        返回抽象路径名表示的文件或目录名
            String getParent()      返回抽象路径名的父路径名
            File getParentFile()    返回抽象路径名的父路径名的抽象路径名
            String getPath()        返回字符串形式抽象路径名
            boolean isAbsolute()    抽象路径名是否为绝对路径
            String getAbsolutePath()返回抽象路径名的绝对路径字符串
            boolean canRead()       文件是否可读
            booleancanWrite()       文件是否可写
            boolean exists()        文件或目录是否存在
            boolean isDirectory()   文件是否是一个目录
            boolean isFile()        是否是一个文件
            boolean createNewFile() 文件不存在创建，存在不创建
            long length()           文件长度
            boolean delete()        删除文件或目录
            String[] list()         返回目录中的文件和目录的名称数组
            String[] list(FilenameFilter filter)过滤后目录中文件和目录名称数组
            File[] listFiles()      返回目录中的文件和目录数组
            File[] listFiles(FileFilter filter) 过滤后目录中的文件和目录数组
            boolean mkdir()         创建目录
            boolean mkdirs()        创建所由路径目录
        
Scanner:
    可通过Scanner类来获取用户的输入
    java.util.Scanner类
    创建：
        Scanner sc = new Scanner(System.in);
    方法：
        String next()       获取输入的字符串
        String nextLine()   获取输入的字符串
        Xxx nextXxx()       获取输入的对应数据类型
        boolean hasNext()   判断是否有下一个数据
        boolean hasNextLine()判断是否有下一个数据
        boolean hasNextXxx()
    next()与nextLine()区别：
        next():当输入内容遇到空白符，读取结束
        nextLine():以Enter为结束符，可获得空白符

异常处理：
    异常是一种错误，但并不是所有错误都是异常
    三种类型的异常：
        检查性异常：无法预见，编译时不能忽略，要处理的异常
        运行时异常：运行时异常编译时可忽略的
        错误：错误不是异常
    Exceptiom类：
        所有异常类都是从java.lang.Exception类继承的子类
        Exception类是Throwable类的子类，另一个子类是Error
    运行时异常：
        ArithmeticException                 算术异常
        ArrayIndexOutOfBoundsException      数组越界异常
        ClassCastException                  类型转换异常
        IllegalArgumentException            非法参数异常
        NullPointerException                空指针
    编译时异常：
        ClassNotFoundException              类找不到
        InterruptedException                线程被中断
    方法：
        String getMessage()                 返回异常信息
        printStackTrace()                   
    异常捕获：
        try/catch关键捕获异常，可能出现的异常代码放入try块中，catch块用于处理发生的异常
        try{
            //
        }catch(ExceptionName e){
            //
        }
        多重捕获：
            try{
                //
            }catch(异常类型1 变量1){
                //
            }catch(异常类型2 变量2){
                //
            }
    throw/throws关键字：
        如果一个方法没有处理编译时异常，那么必须使用throws关键字来声明该方法，放在方法名之后,多个用逗号隔开
        修饰符 返回值 方法名(参数列表) throws 异常类型{
            //
        }
        throw关键字抛出一个异常，throw new 异常类();
    finally关键字：
        用在try块后面，无论是否发生异常，都会执行
    注：当tyr块中出现异常，异常代码后面的代码将不再执行直接跳转找catch块中，
        无论是否发生异常finally都会在最后执行到,除非在在catch中中止虚拟机
    自定义异常：
        编译时异常，继承Exception类
        运行时异常，继承RuntimeException类


