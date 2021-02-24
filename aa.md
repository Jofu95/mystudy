Spring MVC获取参数
通过实体Bean接受请求参数
适用于get和post提交请求方式，Bean的属性名称必须和请求参数名称相同
springmvc如何访问静态资源：
    web.xml中配置
    <servlet-mapping>
        <servlet-name>default</servlet-name>
        <url-pattern>*.css</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>default</servlet-name>
        <url-pattern>*.js</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>default</servlet-name>
        <url-pattern>*.jpg</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>default</servlet-name>
        <url-pattern>*.png</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>default</servlet-name>
        <url-pattern>*.html</url-pattern>
    </servlet-mapping>
    springmvc-servlet.xml中配置
    <!-- 允许css目录下文件可见 -->
	<mvc:resources location="/css/" mapping="/css/**" />
	<!-- 允许css目录下文件可见 -->
	<mvc:resources location="/html/" mapping="/html/**" />
	<!-- 允许css目录下文件可见 -->
	<mvc:resources location="/images/" mapping="/images/**" />

@RequestMapping是用来映射请求的，比如get、post、REST风格与非REST风格
    用在类上表示该类中所有方法的父路径
@PathVariable用来映射请求URL中绑定的占位符，可将URL中占位符的参数绑定到controller处理方法的入参中 
    <a href="springmvc/testRequestMapping/1">testRequestMapping2</a>
    @RequestMapping("/testRequestMapping/{id}")
    public String testRequestMapping2(@PathVariable(value="id") Integer id) {
        System.out.println("testRequestMapping"+ id);
        return "success";
    }
@RequestParam用来获取请求参数
    <a href="springmvc/testRequestMapping3?username=joker&age=26">testRequestMapping3</a>
    @RequestMapping("/testRequestMapping3")
    public String testRequestMapping3(@RequestParam("username") String username, @RequestParam("age") Integer age) {
        System.out.println("testRequestMapping3 "+ username +"--"+age);
        return "success";
    }
@CookieValue映射一个Cookie值
    @RequestMapping("/testCookieValue")
    public String testCookieValue(@CookieValue("JSESSIONID")String cookieValue) {
        System.out.println("testCookieValue: "+cookieValue );
        return "success";
    }

REST风格：
    在web.xml中添加过滤器
    <!-- 配置HiddenHttpMethodFilter:可把POST请求转为DELETE或POST请求 -->
    <filter>
        <filter-name>hiddenHttpMethodFilter</filter-name>
        <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>hiddenHttpMethodFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

    <form action="springmvc/testRest/1" method="post">
        <input type="hidden" name="_method" value="PUT">
        <input type="submit" value="testRestPut">
    </form>
    @RequestMapping(value="/testRest/{id}", method = RequestMethod.PUT)
    public String testRestPut(@PathVariable("id")Integer id) {
        System.out.println("test put: "+id);
        return "success";
    }

SpringMVC的妆发与重定向
    重定向是将用户从当前处理请求定向到另一个视图或处理请求，以前的请求中存放的信息全部失效，并进入一个新的request作用域，重定向是客户端行为，至少做了两次请求
    转发是将用户对当前处理的请求转发给另一个视图或处理请求，以前的request中存放的信息不会失效，转发是服务器行为，只做一次请求
    SpringMVC框架中，控制器类中处理方法的return语句默认为转发实现，只不过是转发到视图
    return "forword:/xx/xxx";
    return "redirect:/xx/xxx"
    如果不需要前端控制器拦截配置如下：
    <mvc:resources location="/html/" mapping="/html/**">

SpringMVC应用@Autowired和@Service进行依赖注入
    使用@Autowired注解类型将依赖注入到一个属性或方法，例如：
    @Autowired
    public UserService userService;
    类必须使用Service注解类型标明为@Service,另外需在配置文件中使用<context:component-scan base-package="">扫描依赖包

SpringMVC Converter(类型转换器)：
    Converter<S,T>是一个可将一种数据类型转换为另一种数据类型的接口，S表示原类型，T表示目标类型
    内置类型转换器：
    1、标量转换器
     StringToBooleanConverter           String到boolean的转换
     ObjectToStringConverter            Object到String的转换
     StringToNumberConverterFactory     String到数字的转换
     NumberToNumberConverterFactory     基本类型到包装类型的转换
     ...
    2、集合、数组相关转换器
     ArrayToCollectionConverter         任意数组到任意集合的转换
     ...发生的
    类型转换是在视图和控制器相互传递数据时
    自定义类型转换器：
     创建自定义类型转换器、注册类型转换器
     实现Converter接口，实现convert方法，配置文件注册：
     <bean id="conversionService" class="org.springframework.context.support.ConversionServiceFactoryBean">
		<property name="converters">
			<list>
				<bean class="converter.GoodsConverter"/>
			</list>
		</property>
	 </bean>
    开启类型转换服务
     <mvc:annotation-driven conversion-service="conversionService"/>

SpringMVC Formatter(数据格式化)：
    内置格式化转换器：
    NumberFormatter     实现Number与String之间的解析与格式化
    CurrencyFormatter   实现Number与String之间的解析与格式化(带货币符号)
    PercentFormatter    实现Number与String之间的解析与格式化(带百分数符号)
    DateFormatter       实现Date与String之间的解析与格式化
    自定义格式化转换器：
     实现Formatter接口，并实现两个方法parse和print
     <bean id="conversionService" class="org.springframework.format.support.FormattingConversionServiceFactoryBean">
		<property name="formatters">
			<list>
				<bean class="formatter.GoodsFormatter"/>
			</list>
		</property>
	 </bean>
	开启类型转换服务
	 <mvc:annotation-driven conversion-service="conversionService"/>

SpringMVC的表单标签
    在JSP页面使用Spring表单标签库时，必须在JSP页面开头声明taglib指令
    <%@taglib prefix="form" uri="http://www.springframework.org/tags/form"%>
    表单标签库中有form、input、password、hidden、textarea、checkbox、checkboxes、radiobutton、radiobuttons、select、options、options、errors等
    表单标签语法：
    <form:>
    b表单标签除html表单属性外还有其他属性：
    1、acceptCharset    定义服务器接收的字符编码列表
    2、commandName      暴露表单对象的模型属性名称
    3、cssClass         定义应用到form元素的Css类
    4、cssStyle         定义应用到form元素的Css样式
    5、htmlEscape       true或false,表示是否进行html转义
    6、modelAttribute   

SpringMVCJSON数据交互
    JSON是一种轻量级数据交换格式，基于纯文本的数据格式，有对象和数组两种数据结构
    1、对象结构
     对象结构以"{"开始"}"结束，中间部分由0或多个以英文","分隔的key/value对构成，key和value用":"分隔
     {
         key1:value1,
         key2:value2,
         ...
     }
     key必须是String类型，value可以是String、Number、Object、Array等数据类型
    2、数组结构
     数组结构以"["开始，以"]"结束，中间部分由0个或多个以英文","分隔的值的列表组成
     [
         value1,value2,...
     ]
    JSON数据转换
    
SpringMVC拦截器（Interceptor）
    主要用于拦截用户的请求并作相应的处理，通常应用在权限验证、记录请求信息的日志、判断用户是否登录等
    使用拦截器需要对拦截器进行定义和配置，定义一个拦截器可通过两种方式：
    1、实现HandlerInterceptor接口或继承HandlerInterceptor接口的实现类来定义
     三个实现方法：
     preHandler方法：在控制器的处理请求方法之前执行，返回值表示是否中断后续操作，true表示继续向下执行，false表示中断
     postHandler方法：在控制器的处理请求方法之后，解析视图之前执行
     afterComletion方法：在控制器的处理请求完成后执行面积视图渲染结束后执行，可通过此方法实现资源清理、记录日志等
    2、实现WebRequestInterceptor接口或继承WebRequestInterceptor接口的实现类来定义
    拦截器的配置：
     <!-- 配置拦截器 -->
	<mvc:interceptors>
		<!-- 配置全局拦截器，拦截所有请求 -->
		<bean class="interceptor.TestInterceptor"/>
		<mvc:interceptor>
			<!-- 配置拦截器作用路径 -->
			<mvc:mapping path="/**"/>
			<!-- 配置不需要拦截作用的路径 -->
			<mvc:exclude-mapping path=""/>
			<!--  -->
			<bean class=""/>
		</mvc:interceptor>
		<mvc:interceptor>
			<!-- 拦截作用路径 -->
			<mvc:mapping path="/gotoTest"/>
			<bean class=""/>			
		</mvc:interceptor>
	</mvc:interceptors>
    <mvc:interceptors>元素用于配置一组拦截器，子元素<bean>定义全局拦截器，即拦截所有请求
    <mvc:interceptor>元素定义的是指定路径的拦截器，子元素<mvc:mapping>用户配置拦截器作用路径
    <mvc:exclude-mapping>元素配置不需要拦截的作用路径
    <mvc:interceptor>元素的子元素必须按照：<mvc:mapping>、<mvc:exclude-mapping>、<bean>顺序配置

SpringMVC数据验证
    SpringMVC框架中有两种验证输入数据的方法：利用Spring自带的验证框架、利用JSR303实现
    数据验证分为客户端验证和服务器端验证，客户端通过js正常用户的误操作，服务器端阻止非法数据
    验证器Validator接口和ValidationUtils类
     创建自定义Spring验证器需要实现Validator接口，并实现support和validate方法，当support方法返回true时，验证器可以处理指定的Class,
     validate方法的功能是验证目标对象，并验证错误信息存入Errors对象
     ValidationUtils类是一个工具类，可帮助用户判定值为空

SpringMVC JSR-303验证框架
    JSR 303验证，目前有两个实现，一个是Hibernate Validator(与Hibernate无关),一个是Apache BVal
    <!-- 配置消息属性文件 -->
	<bean id="messageSource" class="org.springframework.context.support.ReloadableResourceBundleMessageSource">
		<!-- 资源文件名 -->
		<property name="basenames">
			<list>
				<value>/WEB-INF/resource/errorMessages</value>
			</list>
		</property>
		<!-- 配置编码格式 -->
		<property name="fileEncodings" value="UTF-8"></property>
		<!-- 对资源文件缓存的时间单位为秒 -->
		<property name="cacheSeconds" value="120"></property>
	</bean>
	<!-- 注册校验器 -->
	<bean id="validator" class="org.springframework.validation.beanvalidation.LocalValidatorFactoryBean">
		<!-- hibernate校验器 -->
		<property name="providerClass" value="org.hibernate.validator.HibernateValidator" />
		<!-- 指定校验使用的资源文件 -->
		<property name="validationMessageSource" ref="messageSource"/>
	</bean>
	<!-- 开启spring的valid功能 -->
	<mvc:annotation-driven conversion-service="conversionService" validator="validator"/>
    标注类型：
     JSR 303不需要编写验证器，但需要利用他的标注类型在领域模型的属性上嵌入约束
     1、空检查
       @Null 验证对象是否为null
       @NotNull 验证对象是否不为Null，无法检查长度为0的字符串
       @NotBlank 检查约束字符串是否为null，以及被trim后的长度是否大于0，只针对字符串，且会去掉前后空格
       @NotEmpty 检查约束元素是否为null或者是empty
     2、boolean检查
       @AssertTrue 验证boolean属性是否为true
       @AssertFalse 验证boolean属性是否为false
     3、长度检查
       @Size (min=,max=) 验证对象(Array、Collection、Map、String)长度是否在给定的范围内
       @Length (min=,max=) 验证字符串长度是否在给定范围内
     4、日期检查
       @Past 验证Date和Callendar对象是否在当前时间之前
       @Future 验证Date和Calendar对向是否在当前时间之后
       @Pattern 验证String对象是否符合正则表达式
     5、数值检查
       @Max、@Min、@DecimalMax、@DecimalMin、@Digits、@Range(min=,max=)、@Valid、@CreditCardNUmber、@Email  

Java国际化
    java国际化思想是将程序中的信息放在资源文件中，程序根据支持的国家及语言环境读取相应的资源文件
    Java程序的国际化主要通过两个类来完成
    1、java.util.Locale
      用于提供本地信息(语言环境),不同语言、国家和地区采用不同Locale对象表示
    2、java.util.ResourceBundle
      资源包，包含了特定语言环境的资源对象
    资源文件的命名可以有3种形式：
     1）baseName.properties
     2）baseName_language.properties
     3）baseName_language_country.properties
     baseName是由用户自定义，language和country必须为Java所支持的语言和国家/地区代码
     如：中国大陆，baseName_zh_CN.properties, 美国，baseName_en_US.properties
     Java中的资源文件支支持ISO-8859-1编码格式字符

SpringMVC国际化
    加载资源属性文件
    <bean id="" class="org.springframework.context.support.ReloadableResourceBundleMessageSource">
        <property name="basenames">
            <list>
                <value>/WEB-INF/resource/messages</value>
                <value>/WEB-INF/resource/labels</value>
            </list>
        </property>
    </bean>
    使用区域解析器bean选择语言区域，该bean有3个常见实现，即AcceptHandlerLocaleResolver、SesssionLocaleResolver、CookieLocaleResolver
    1、AcceptHandlerLocaleResolver
      跟据浏览器Http Header中的accept-language域设定
    2、SessionLocaleResolver
      根据本次会话过程中的语言设定决定语言区域
      <bean id="localeResolver" class="org.springframework.web.servlet.i18n.SessionLocaleResolver">
        <property name="defaultLocale" value="zh_CN"/>
      </bean>
    3、CookieLocaleResolver
      跟据Cookie判定用户语言设定
    如果基于SessionLocaleResolver和CookieLocaleResolver的国际化实现，必须配置LocaleChangeInterceptor拦截器
    <mvc:interceptors>
		<bean class="org.springframework.web.servlet.i18n.LocaleChangeInterceptor"/>
	</mvc:interceptors>
    message标签显示国际化
    taglib指令声明spring标签
    <%@taglib uri="http://www.springframework.org/tags" prefix="spring"%>
    message标签常用属性：
     code 获取国际化消息的key
     arguments 代表该标签的参数
     argumentSeparator 用来分隔该标签参数的字符，默认为逗号
     text code属性不存在或指定的key无法获取消息时所显示的默认文本信息
    <!-- 国际化操作拦截器 -->
	<mvc:interceptors>
		<bean class="org.springframework.web.servlet.i18n.LocaleChangeInterceptor"/>
	</mvc:interceptors>
	<!-- 存储区域设置 -->
	<bean id="localeResolver" class="org.springframework.web.servlet.i18n.SessionLocaleResolver">
		<property name="defaultLocale" value="zh_CN"/>
	</bean>
	<!-- 加载国际化资源文件 -->
	<bean id="messageSource" class="org.springframework.context.support.ReloadableResourceBundleMessageSource">
		<property name="basename" value="/WEB-INF/resource/messages"/>
		<property name="cacheSeconds" value="0"/>
		<!-- 解决乱码 -->
		<property name="defaultEncoding" value="UTF-8"/>
	</bean>

常用注解：
    1、@Controller
    负责处理由DispacherServlet分发的请求，它把用户请求的数据经过业务层处理之后封装成一个Model,
    然后再把该Model返回给对应的View进行展示
    @Controller用于标记在一个类上，使用该标记的类就是SpringMVC Controller对象，@Controller只是定义了一个控制器类，
    而使用@RequestMapping注解的方法才是真正处理请求的处理器
    仅仅使用@Controller注解Spring无法识别为控制器类，还需配置（两种方式）
        1）在springmvc配置文件中定义控制器类的bean对象
        <bean class="com.joker.handler.MyController"></bean>
        2）在springmvc配置文件中开启注解扫描
        <context:component-scan base-package="com.joker.*"></context:component-scan>
    2、@RequestMapping
    用来处理请求地址映射的注解，可用于方法或类上，用于类上表示类中的所有响应请求的方法都是以该地址作为父路径
    @RequestMapping注解有六个属性(三类)：
        1）value , method
        value 指定请求的实际地址
        method 指定请求的method类型，GET、POST、DELETE、PUT
        2）consumes , produces
        consumes 指定处理请求的提交内容类型（Content-Type）,例如：application/json、text/html
        produces 指定返回的内容类型，仅当request请求头中的Accept类型中包含该指定类型才返回
        3）params , headers
        params 指定request中必须包含某些参数值，才让该方法处理
        headers 指定request中必须包含某些指定的header值，才能让该方法处理请求
    3、@Resource 和 @Autowired
    bean的注入时使用，@Resource注解并不是Spring的注解，但Spring支持该注解的注入
    共同点，可在字段和setter方法上，如果都写在字段上就不用再写setter方法
        @Autowired  //方式一
        private UserDao userDao;
        
        @Autowired  //方式二
        public void setUserDao(UserDao userDao) {
            this.userDao = userDao;
        }
    不同点，
        1）@Autowired为Spring提供的注解，按照类型（byType）装配依赖对象
        按照名称（byName）装配对象，结合@Qualifier注解
        @Autowired 
        @Qualifier("userDao")
        private UserDao userDao;
        2）@Resource默认按照byName自动注入，有两个属性：name和type,Spring将@Resource注解的name属性解析为bean的名字(id)，
        而type属性解析为bean的类型，使用name属性，则使用byName自动注入策略，使用type属性，则使用byType自动注入策略
        如果不指定name和type，则通过反射机制使用byName自动注入策略
    4、@ModelAttribute 和 @SessionAttributes
    用于将多个请求参数封装到一个实体对象,和model.addAttribute("",xx)功能一样
    注解一个非请求处理方法，被该注解的方法将在每次调用该控制器类的请求处理方法前被调用，这种特性可用于控制登录权限
    5、@PathVariable将请求URL中的模板变量映射到功能处理方法的参数上，即取出uri模板中的变量作为参数
    6、@RequestParam用于在SpringMVC后台控制层获取参数
    三个常用参数：defaultValue="0",required=false,value="isApp"
    defaultValue 表示设置默认值
    required 设置是否必须传入的参数
    value 表示接收的传入参数类型
    7、@ResponseBody用于将Controller的方法返回的对象，通过适当的HttpMessageConverter转换为指定格式后，写入到Response对象的body数据区
    返回的数据不是html标签页面，而是其他某种格式（json、xml等）的数据时使用
    8、@Component相当于通用注解，
    9、Respository用于注解dao层，在daoimpl类上面注解

SpringMVC统一异常处理
    如果对每个过程出现的异常单独处理，那么系统的代码耦合的高，工作量大不好统一，维护就很困难
    SpringMVC框架支持将所有异常处理从各层中解耦出来，保证相关处理过程的功能单一，又实现了异常信息的统一处理和维护
    统一异常处理有三种方式：
    1、使用SpringMVC提供的简单异常处理器SimpleMappingExceptionResolver
    2、实现String的异常处理接口HanlderExceptionResolver自定义异常处理器
    3、使用@ExceptionHanlder注解实现异常处理

SpringMVC文件上传
    SpringMVC框架的文件上传是基于commons-fileupload组件的文件上传
    <form>元素的属性enctype指定表单的编码方式，有三个属性值：
    1、application/x-www-form-urlencoded,默认编码方式，只处理表单域里的value属性值
    2、multipart/form-data,该编码方式是以二进制流的方式来处理表单数据，并将文件域指定文件的内容封装到请求参数中
    3、text/plain,该编码方式只有当表单的action属性为"mailto:url"形式时才使用，主要适用直接通过表单发送邮件
    MultipartFile接口：
    SpringMVC框架中文件上传时文件相关信息及操作都封装到该对象中
    byte[] getBytes()               以字节数组形式返回文件内容
    String getContentType()         返回文件内容类型
    InputStream getInputStream()    返回一个InputStream，从中读取文件的内容
    String getName()                返回请求参数的名称
    String getOriginalFilename()    返回客户端提交的原始文件名称
    long getSize()                  返回文件大小，单位为字节
    bookean isEmpty()               判断被上传文件是否为空
    void transferTo(File destination)将上传文件保存到目标目标录下
    <!-- 配置MultiparResolver,用于文件上传，使用spring的CommonsMultiparResolver -->
	<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
		<property name="maxUploadSize" value="5000000"></property>
		<property name="defaultEncoding" value="UTF-8"></property>
	</bean>

SpringMVC文件下载
    实现文件下载有两种方式：
    1、通过超链接实现下载
    2、利用程序编码实现下载
      1）web服务器需要告诉浏览器所输出内容的类型不是普通文本文件或html文件，而是需要保存到本地的下载文件，需要设置
        Content-Type的值为application/x-msdownload
      2）web服务器希望浏览器不直接处理相应的实体内容，而是由用户选择相应的实体内容保存到一个文件中，需要设置
        Content-Disposition报头
      response.setHeader("Content-Type","application/x-msdownload");
      response.setHeader("Content-Disposition","attachment;filename="+filename);
    

Mybatis实现映射器的两种方式
    映射器是Mybatis中最重要、最复杂的组件，由一个接口和对应的XML文件(或注解)组成，可配置内容如下：
    1、描述映射规则
    2、提供SQL语句，并可以配置SQL参数类型、返回类型、缓存刷新等信息
    3、配置缓存
    4、提供动态SQL
    映射器的主要作用是将SQL查询到的结果映射为一个POJO，或将POJO的数据插入到数据库中，并定义一些关于缓存的重要内容
    用XML实现映射器：
    分为两部分：接口和XML
    <?xml version="1.0" encoding="UTF-8" ?> 
    <!DOCTYPE mapper 
    PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"  
    "http://mybatis.org/dtd/mybatis-3-mapper.dtd"> 
    <mapper namespace="mapper.RoleMapper">
        <select id="getRole" parameterType="long" resultType="role">
            SELECT id,role_name as roleName,note FROM role id=#{id}
        </select>
    </mapper>
    <mapper>元素中的属性namespace所对应的是一个接口的全限定名
    <select>元素表名这是一条查询语句，而id属性是对应接口中的方法名，parameterType="long"表示输入参数类型，resultType="role"表示输出参数类型
    注解实现映射器：
    只需要一个接口，通过注解注入SQL
    public interface RoleMapper2 {
        @Select("select id,role_name as roleName,note from t_role where id=#{id}")
        Role getRole(Long id);
    }

Mybatis执行SQL的两种方式
    SqlSession发送SQL：
      selectOne(String str, Object obj) 查询并且只返回一个对象
      SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(Resources.getResourceAsStream("mybatis-config.xml"));
	  SqlSession sqlSession = sqlSessionFactory.openSession();
	  Role role = sqlSession.selectOne("mapper.RoleMapper.getRole", 1L);
      当mybatis中只有一个id为getRole的SQL，可简写为Role role = sqlSession.selectOne("getRole", 1L);
    用Mapper接口发送SQL：
      RoleMapper roleMapper = sqlSession.getMapper(RoleMapper.class);
	  Role role2 = roleMapper.getRole(1L);
    推荐使用Mapper接口方式，可消除SqlSession带来的功能性代码，提高可读性，而SqlSession发送SQL，需要跟据sql的id去匹配对应SQL，而Mapper接口完全面向对象

核心组件的作用域和生命周期
    SqlSessionFactoryBuilder
        作用在于创建SqlSessionFactory,创建成功后就失去了作用，所以只能存在于创建SqlSessionFactory的方法中，最佳作用域是方法作用域
    SqlSessionFactory
        SqlSessionFactory可看作是一个数据库连接池，作用就是创建SqlSession接口对象，生命周期存在于整个Mybatis应用之中
        作为单例，在应用中被共享，最佳作用域是应用作用域
    SqlSession
        相当于数据库连接Connection对象，可在一个事务里执行多条SQL，然后通过commit、rollback等方法，提交或回滚事务
        存活在一个业务请求中，处理完整个请求后，应该关闭这条连接，最佳作用域是请求或方法作用域
    Mapper
        mapper是一个接口，由SqlSession所创建，生命周期小于等于SqlSession生命周期，Mapper代表一个请求中的业务处理
    
Mybatis配置文件详解
    