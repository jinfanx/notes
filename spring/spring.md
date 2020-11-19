## spring启动过程
todo
## bean生命周期
启动 $\rightarrow$ 初始化 $\rightarrow$ 注入各种aware对应的组件 $\rightarrow$ BeanPostProcessor.postProcessBeforeInitialization() $\rightarrow$ InitializingBean $\rightarrow$ BeanPostProcessor.postProcessAfterInitialization()

## 生命周期钩子
- 各种aware
   - BeanNameAware
   - BeanClassLoaderAware
   - BeanFactoryAware
   - EnvironmentAware
   - EmbeddedValueResolverAware
   - ResourceLoaderAware
   - ApplicationEventPublisherAware
   - MessageSourceAware
   - ApplicationContextAware
   - ServletContextAware
  
- BeanPostProcessor
有两个方法，分别在InitializingBean之前和之后调用

- InitializingBean
所有aware和属性注入完成后执行，可以结合spring事件机制使用ApplicationEventPublisher发布特定事件

## springboot
### 原理
使用了java的spi机制，在META-INF下注册自动配置类`org.springframework.boot.autoconfigure.EnableAutoConfiguration`，spring启动时会加载所有的自动配置类并执行自动配置。所谓自动配置就是在spring应用启动时扫描配置类，判断是否符合自动配置条件，执行对应的方法，在这些方法中可以返回配置好的对象，如对mybatis做自动配置，可以检测classpath下是否有mybatis相关的类或者配置文件中是否有对应的属性，如果存在就进行自动配置，在相应的方法中创建SqlSessionFactory并注入到spring容器中。

### starter和autoconfigure区别
autoconfigure真正实现了自动配置逻辑，starter包含自动配置功能所有的库以及autoconfigure，通常只有一个pom。如mybatis的自动配置，starter时一个包含mybatis相关库以及autoconfigure的pom，使用时只需要引入starter即可

### 自定义自动配置
- 实现自动配置类autoconfigure
- 在autocongfigure的META-INF目录下注册自动配置类
```
# Auto Configure
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
org.mybatis.spring.boot.autoconfigure.MybatisLanguageDriverAutoConfiguration,\
org.mybatis.spring.boot.autoconfigure.MybatisAutoConfiguration
```
- 封装starter
新建一个工程，只包含pom即可，在pom下引用自动配置功能相关的库以及autoconfigure


## spring mvc
### DispatcherServlet
前端控制器，所有请求都从此经过，能拿到原始请求，可以用来定位问题
### HandlerMapping
请求和具体的处理方法映射器
### ViewResolver
用来处理各种类型的相应，如json、Resource、String等

### HttpMessageConverter
- `org.springframework.http.converter.HttpMessageConverter`  
HttpMessageConverter用来处理返回值，当报返回值无法处理等错误时可去`org.springframework.web.servlet.mvc.method.annotation.AbstractMessageConverterMethodProcessor`
跟代码，确定当前注册的converter里面是否有用来处理指定返回值的converter，若没有，可手动注册，springboot的自动配置会注册常用的converter，如json、resource、byteArray等
ResourceHttpMessageConverter可用来处理Resource类型的返回值，用来做文件下载  
   `注意：HTTPMessageConverter的顺序很重要，它们被放在list里从前到后遍历，找到能处理当前返回值的就不再使用后面的converter`

## 常见问题
### 循环依赖
用`@Resource`或`@Autowire`等注入属性可以正常处理循环依赖，但如果在构造方法中存在循环依赖，则无法创建bean，因为bean会先实例化，然后注入各种属性。

### spring容器中注入bean方法  
- 注解注入
- xml注入
- FactoryBean注入  
可以在FactoryBean的`getObject()`方法中创建需要注入的bean，FactoryBean本身必须先注册到spring
- BeanFactoryPostProcessor  
可实现BeanFactoryPostProcessor接口，获取beanFactory，手动注入Bean