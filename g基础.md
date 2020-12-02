数据结构：
    Java中数据结构主要包括以下接口和类：
        枚举、位集合、向量、栈、字典、哈希表、属性

    Vector类：
        实现了一个动态数组，和ArrayList类似，Vector类是同步的
        主要用于数组大小不确定的情况，或可改变大小的数组
        构造方法：
            Vector()                    默认大小为10
            Vector(int size)            指定大小
            Vector(int size, int incr)  指定大小，每次增量为incr
            Vector(Collection c)        
        方法：
            addElement(Object obj)      增加元素到末尾，大小增加1
            int capacity()              容量大小
            clear()                     清除所有元素
            Object get(int index)       获取指定位置元素
            isEmpty()                   是否为空
            Object remove(int index)    移除指定位置元素
            int size()                  返回元素个数

    Stack类：
        栈是Vector的一个子类，先进后出
        方法：
            boolean empty()             堆栈是否为空
            Object peek()               堆栈顶部对象
            Object pop()                移除堆栈顶部对象，并返回
            Object push()               添加对象到栈顶
            int search(Object element)  返回对象在栈顶的位置索引

    Hashtable类：
        构造方法：
            Hashtable()     
            Hashtable(int size)
        方法：
            clear()                         清空元素
            boolean contains(Object value)  是否存在与指定值关联的键
            boolean containsKey(Object key) 是否存在该键
            boolean containsValue(Object value)是否存在值
            Object get(Object key)          返回指定键对应的值
            Enumeration keys()              返回键的枚举
            boolean isEmpty()               是否为空
            Object put(Object key, Object value)添加键值对
            int size()                      键值对数

    Properties类：
        继承于Hashtable，表示一个持久的属性集，属性列表中每个键和值都是一个字符串
        方法：
            String getProperty(String key)  根据指定键获取属性值
            list(PrintStream streamOut)     将属性列表输出到指定的输出流
            load(InputStream stream) throws IOException 从输入流中读取属性列表
            Enumeration propertyNames()     从输入流获取属性列表
            Object setProperty(String key, String value)    设置属性
            store(OutputStream stream, String des)
         
集合框架：
    集合框架是一个用来代表和操纵集合的统一架构，包含接口、实现、算法
    主要包含两种类型：集合（Collection）存储元素的集合、图(Map)存储键/值对映射
    集合框架位于java。util包中
    集合接口：
        Collection      不提供直接继承的类，只提供继承于子接口(List/Set)
        List            有序，可通过索引访问List中的元素，允许有相同的元素
        Set             无序，不允许有相同的元素
        SortedSet       继承于Set保存有序的集合
        Map             存储一组键值对对象，提供键值对的映射,键唯一
        Map.Entry       描述Map集合中的一个键值对
        SortedMap       继承于Map，使用key保持升序排序
        Enumeration     被迭代器取代
    Set和List区别：
        Set接口实例存储的是无序的，不重复的数据; List接口实例存储的是有序，可重复的数据
        Set检索效率低，增删效率高，增删不会使元素位置改变，实现类有HashSet、TreeSet
        List和数组类似，可动态增长，查找效率高，增删效率低，会导致元素位置改变，实现类ArrayList、LinkedList、Vector
    实现类：
        ArrayList       实现了List接口，可变大小的数组，线程不安全，增删慢，查询快
        LinkedList      实现了List接口，允许有null元素，主要创建链表数据结构，线程不安全，查询效率低
        HashSet         实现了Set接口，不允许出现重复元素，元素无序，允许包含null值，最多只有一个
        LinkedHashSet   具有迭代顺序的Set接口，哈希表和链表实现 
        TreeSet         实现类Set接口，可实现排序功能
        HashMap         实现了Map接口，根据键的HashCode值存储数据，访问速度快，允许一条键为null，线程不安全
        TreeMap         
        LinkedHashMap   继承于HashMap，使用自然顺序对元素进行排序
    迭代器遍历集合框架，是一个对象，实现类Iterator接口或ListIterator接口，可向前或向后双向遍历
    获取迭代器 调用集合的iterator()方法
    方法：
        Object next()       迭代器的下一个元素
        boolean hasNext()   是否还有元素
        remove()            将迭代器返回的值移除        
    遍历ArrayList:
        for循环遍历、迭代器遍历
    遍历Map:
        for循环（获取所有键的集合keySet(),遍历键，get(key)获取键值）
        迭代器（获取所有映射关系entrySet()，获取迭代器然后遍历）
        for循环另一种遍历（获取所有映射关系entrySet()，遍历key和value）    

ArrayList
    ArryaList底层是基于数组来实现容量大小动态变化，默认初始容量为10
    允许有null值存在
    ArrayList<E> list = new ArrayList<E>();
    E表示泛型数据类，只能为引用数据类型
    方法：
        boolean add([int index,] E element)     [指定位置]添加元素
        clear()                                 删除所有元素
        boolean contains(Object obj)            判断是否包含某个元素
        Object get(int index)                   获取指定索引的元素
        int indexOf(Object obj)                 获取指定元素的索引位置
        remove(Object obj)                      删除指定元素
        remove(int index)                       删除指定位置元素
        int size()                              获取集合大小
        isEmpty()                               集合是否为空
        subList(int fromindex,int toindex)      获取截取部分的动态数组
        Object set(int index, E element)        设置替换指定索引的元素，返回原元素
        sort(Comparator c)                      对集合排序
        toArray([T[] arr])                      将集合转为数组[到指定数组]
        ensureCapacity(int num)                 设置集合初始容量

LinkedList:
    链表是一种常见的基础数据结构，是一种线性表，链表可分为单向链表和双向链表
    单项链表包含两个值，当前节点值和指向下一个节点的链接
    双向链表有三个值，数值、向后的节点连接、向前的节点链接
    LinkedList相比ArrayList，增删效率更高，改查效率低
    只需要在末尾增加元素或只查询某一个元素可使用ArrayList
    循环访问列表中的某些元素或频繁增删元素使用LinkedList
    方法和ArrayList类似，但有不同的方法，
        addFirst(E e)           添加元素到头部
        addLast(E e)            添加元素到尾部
        boolean offer(E e)      链表末尾添加元素

HashSet
    HashSet是基于HashMap来实现的，不允许有重复元素
    允许有null值，无序，不是线程安全的
    无参构造函数默认创建大小为16的容器，加载因子为0.75
    HashSet不允许重复原因？
        查看add方法的源码发现是通过定义的全局HashMap对象调用put()来添加元素的
        由于Map集合的键值唯一，所以添加的元素不会重复
    
HashMap
    存储的内容为键值对映射，是根据键的HashCode值来存储数据，具有很快的访问速度
    最多允许一条记录为null，不支持线程同步，无序
    键不允许重复，重复会覆盖原来相同键的值
    方法:
        clear()             移除所有键值对
        boolean isEmpty()   集合是否为空
        int size()          获取集合的键值对数量
        put(K key, V value) 添加键值对
        remove(Object key)  删除指定的键的键值对
        containsKey(Object key)是否包含指定键对应的映射关系            
        containsValue(Object value)是否包含指定值对应的映射关系   
        replace(K key, V oldValue, V newValue)替换指定键的值
        Object get(Object key) 根据键获取值
        entrySet()          返回所有键值对的映射集合
        keySet()            返回所有键的集合
        values()            返回所有值的集合

序列化：
    一个对象可以被表示为一个字节序列，该字节序列该字节序列包括该对象的数据，有关对象的类新信息数据类信息
    将序列化对象写入文件之后，可以反序列化从文件中读取出来
    指堆内存中的java对象数据，通过某种方式把他存储到磁盘中这个过程叫序列化
    通常是将对象或数据结构转化为二进制的过程
    序列化作用：
        把内存中的对象保存到文件或数据库中
        用套接字在网络上传送对象
        通过RMI传输对象
    对象要序列化必须满足两个条件：
        实现Serializable接口、所有的属性必须是可序列化的，如果有不可被序列化的属性需用transien关键字声明
    ObjectInputStream类用来序列化一个对象，方法写数据
        public final void writeObject(Object x) throws IOException
    ObjectOutputStream类用来反序列化一个对象，方法读数据
        public final Object readObject() throws IOException,ClassNotFoundException
    
网络编程：
    java.net包中提供了两种常见的网络协议的支持
        TCP：TCP是传输控制协议，保障两个应用程序之间的可靠通信，通常用于互联网协议，TCP/IP
            TCP是一个双向的通信协议，，数据可通过两个数据流在同一时间发送
        UDP：UDP是用数据报协议，一个无连接的协议，提供应用程序之间要发送的数据的数据包
    Socket编程：
        客户端创建一个套接字并尝试链接服务器的套接字，建立连接后，服务器会创建一个Socket对象，
        客户端与服务器通过Socket对象的写入和读取来进行通信
    ServerSocket类：
        服务器端通过ServerSocket类来获取一个端口，并侦听客户端请求
        构造方法:
            ServerSocket() throws IOException
            ServerSocket(int port) throws IOException    创建绑定到特定端口的服务器套接字
            ServerSocket(int port, int backlog) throws IOException 
            ServerSocket(int port, int backlog, InetAddress address) throws IOException
        方法：
            int getLocalPort()                      返回套接字上侦听的端口
            Socket accept() throws IOException      侦听并接受套接字的链接
            setSoTimeout(int timeout)               通过指定超时值启用/禁用
            bind(SocketAddress host, int backlog)   将ServerSocket绑定到特定地址
    Socket类：
        客户端通过Socket类与服务器互通
        构造方法：
            Socket()
            Socket(String host, int port)           创建一个套接字并将其连接到主机上的指定端口号
            Socket(InetAddress host, int port)      创建一个套接字并将其连接到指定IP地址的指定端口
            Socket(String host, int port, InetAddress localAddress, int localPort)
            Socket(InetAddress host, int port, InetAddress localAddress, int localPort)
        方法：
            connection(SocketAddress host, int timeout)     连接到服务器，并指定超时值
            InetAddress getInetAddress()                    获取套接字连接地址
            int getPort()                                   返回套接字连接到的远程端口
            int getLocalPort()                              返回套接字绑定到的本地端口
            SocketAddress getRomteSocketAddress()           获取套接字连接的断电的地址
            InputStream getInputStream()                    返回套接字输入流
            OutputStream getOutputStream()                  返回套接字输出流
            close()                                         关闭套接字
    InetAddress类：
        static InetAddress getByAddress(byte[] addr)
        static InetAddress getByAddress(String host, byte[] addr)
        static InetAddress getByName(String host)
        String getHostAddress()                             返回IP地址字符串
        String getHostName()                                返回IP地址的主机名
        static InetAddress getLocalHost()                   返回本地主机

多线程：
    进程，包括由操作系统分配的内存空间，包含一个或多个线程
        线程不能独立存在，必须是进程的一部分
    多线程是多个任务的一种特别形式，多线程使用了更小的资源开销
    多线程能满足开发编写高效率的程序充分利用CPU
    
    线程的生命周期：
        新建状态 --> 就绪状态 --> 运行状态 --> 阻塞状态 --> 死亡状态
        新建状态：
            创建线程后，线程对象处于新建状态，直到调用start()方法
        就绪状态：
            调用start()方法后处于就绪状态，等待JVM线程调度器调度
        运行状态：
            就绪状态的线程获取CPU资源，可执行run()方法，进入运行状态，
            该状态下，可变为阻塞状态、就绪状态、死亡状态
        阻塞状态：
            线程执行了sleep，suspend等方法，失去所占有的资源，线程进入阻塞状态，
            休眠时间到或获得设备资源后可重新进入就绪状态。
            等待阻塞：运行状态中的线程执行wait()方法，使线程进入等待阻塞状态
            同步阻塞：线程在获取synchronized同步锁失败
            其他阻塞：通过调用线程的sleep或join方法发出的I/O请求时，线程进入阻塞状态
                当sleep超时，join等待线程终止或超时，或i/o处理完毕，重新进入就绪状态
        死亡状态：运行状态的线程处理完任务或者其他终止条件，该线程进去终止状态
    
    线程的优先级：
        取值范围从 1 到 10 ，线程优先级高获取资源的概率高，并不一定就先执行
    
    创建线程(三种方式)：
        实现Runnable接口、继承Thread类、通过Callable和Future创建线程
    Thread类：
        Thread类位于java.lang包下，不需要导包
        方法：
            start()             执行线程，JVM调用该线程的run方法
            run()               
            setName(String name)设置线程名
            getName()           获取线程名
            setPriority(int priority)设置优先级
            setDaemon(boolean on)标记为守护线程
            join(long mill)     等待该线程终止的时间
            interrupt()         中断线程
            boolean isAlive()   是否处于活动状态
        静态方法：
            yield()                     暂停当前线程，执行其他线程
            sleep(long mill)            让当前正在执行的线程休眠执行时间
            boolean holdsLock(Object x) 仅当当前线程在指定的对象上保持监视所，返回true
            Thread currentThread()      返回当前正在执行的线程的引用            
            dumpStack()                 将当前线程的堆栈跟踪打印至标准错误流
    Runnable接口：
        对象实现Runnable接口，实现run方法，调用start方法
    Callable和Future:
        创建Callable接口的实现类，并实现call方法，该方法将作为线程执行体，并有返回值
        创建Callable实现类的实例，使用FutureTask类来包装Callable对象，封装了call()方法的返回值
        使用FutureTask对象作为THread对象的Target创建并启动新线程
        调用FutureTask对象的get方法来获取子线程执行结束后的返回值
    
反射：
    程序可以访问、检测和修改本身状态或行为的一种能力
    动态获取类的内容以及动态调用对象的方法和行为为反射机制
    Class类：
        代表类的实体，在运行的Java应用程序中表示类和接口
        方法：
            getClassLoader()        获取类加载器
            getClasses()            返回一个数组包含类中所有公共类和接口的对象
            getDeclaredClasses()    返回一个数组包含类中所有类和接口的对象
            forName(String className)根据类名返回类对象
            String getName()        获取类的完整路径名
            newInstance()           创建类的实例
            getPackage()            活得类的包
            String getSimpleName()  获得类名
            getSuperclass()         获取当前类的父类
            getInterfaces()         获取当前类实现的接口或类
            getField(String name)   获取共有属性对象
            getFields()             获取所有公有属性对象
            getDelaredFileds()      获取所有属性
            getConstructors()       获取所有公有构造器
            getDeclaredConstructors()获取所有构造器
            getMethods()            获取锁有公共方法
            getDelaredMethods()     获取所有方法
    Field类：
        代表类的成员变量
    Method类：
        代表类的方法
    Construtor类：
        代表类的构造方法
    
    反射的三种创建方式：
        Class c = 类名.class;
        或
        Class c = 对象引用.getClass();
        或
        Class c = Class.forName(类的全路径名);
    访问类的属性：getXxx()、setXxx()
    访问类的方法：getMethod()、invoke()  
    
设计模式：
    创建型模式 对象的创建
    结构型模式 对象的组成(结构)
    行为型模式 对象的行为
    创建型模式：简单工厂模式、工厂方法模式、抽象工厂模式、建造者模式、原型模式、单例模式（6个）
    结构型模式：外观模式、适配器模式、代理模式、装饰模式、桥接模式、组合模式、享元模式（7个）
    行为型模式：模板方法模式、观察者模式、状态模式、职责链模式、命令模式、访问者模式、策略模式、备忘录模式、迭代器模式、解释器模式（10个）
    