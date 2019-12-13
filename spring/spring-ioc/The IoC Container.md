## [1. The IoC Container[IOC容器]](https://docs.spring.io/spring/docs/5.2.1.RELEASE/spring-framework-reference/core.html)
This chapter covers Spring’s Inversion of Control (IoC) container.  
[本章节讨论了控制反转（IOC）容器].  
### [1.1. Introduction to the Spring IoC Container and Beans[介绍spring的IOC容器和Bean]](https://docs.spring.io/spring/docs/5.2.1.RELEASE/spring-framework-reference/core.html#beans-introduction)
This chapter covers the Spring Framework implementation of the Inversion of Control (IoC) principle. IoC is also known as dependency injection (DI)  
[本章介绍了Spring框架实现控制反转(IOC)的原理，IOC也称为依赖注入(DI)].  
It is a process whereby objects define their dependencies (that is, the other objects they work with) only through constructor arguments, arguments to a factory method, or properties that are set on the object instance after it is constructed or returned from a factory method.  
[这是一个对象只有通过构造函数参数、工厂方法参数、对象实例化或者通过工厂方法返回实例后在其设置的属性来定义依赖项(即注入其他对象)的过程].  
The container then injects those dependencies when it creates the bean. This process is fundamentally the inverse (hence the name, Inversion of Control) of the bean itself controlling the instantiation or location of its dependencies by using direct construction of classes or a mechanism such as the Service Locator pattern.  
[容器在创建bean时注入bean的依赖项，这个过程完全是bean自身反转的过程（因此称为控制反转），通过使用类直接构造或者类似服务定位模式的原理来控制其依赖项的实例化或位置].  
  
The `org.springframework.beans` and `org.springframework.context` packages are the basis for Spring Framework’s IoC container. The `BeanFactory` interface provides an advanced configuration mechanism capable of managing any type of object. `ApplicationContext` is a sub-interface of `BeanFactory`. It adds:  
[`org.springframework.beans`和`org.springframework.context`这两个包是SpringIOC容器的基础。`BeanFactory`接口提供了能管理任何类型对象的高级配置机制，而`ApplicationContext`是它的子接口，功能如下：]  

- Easier integration with Spring’s AOP features [更容易与Spring的AOP特性集成]  
- Message resource handling (for use in internationalization) [消息资源处理(用于国际化)]
- Event publication [事件发布]
- Application-layer specific contexts such as the `WebApplicationContext` for use in web applications. [特定于应用程序层的上下文，如用于web应用程序的`WebApplicationContext`]  

In short, the `BeanFactory` provides the configuration framework and basic functionality, and the `ApplicationContext` adds more enterprise-specific functionality. The `ApplicationContext` is a complete superset of the `BeanFactory` and is used exclusively in this chapter in descriptions of Spring’s IoC container. For more information on using the `BeanFactory` instead of the `ApplicationContext`, see The `BeanFactory`.  
[简言之，`BeanFactory`接口提供了框架的配置和基础功能，而`ApplicationContext`接口则加入了更多的是企业特性的功能。`ApplicationContext`是`BeanFactory`的一个完整子集，在本章描述SpringIOC容器时专门使用了它。更多使用`BeanFactory`的方法，请看[BeanFactory详细](https://docs.spring.io/spring/docs/5.2.1.RELEASE/spring-framework-reference/core.html#beans-beanfactory)]  
  
In Spring, the objects that form the backbone of your application and that are managed by the Spring IoC container are called beans. A bean is an object that is instantiated, assembled, and otherwise managed by a Spring IoC container. Otherwise, a bean is simply one of many objects in your application. Beans, and the dependencies among them, are reflected in the configuration metadata used by a container.  
[在Spring中，构成应用程序主干并由Spring IoC容器管理的对象称为bean。bean是由Spring Ioc容器负责创建、装配及其他功能的对象。另外，bean只是应用程序中的许多对象之一。bean及其他们之间的依赖关系反映在被容器使用的配置元数据中。]  
  
### [1.2. Container Overview[容器概述]](https://docs.spring.io/spring/docs/5.2.1.RELEASE/spring-framework-reference/core.html#beans-basics)  
The `org.springframework.context.ApplicationContext` interface represents the Spring IoC container and is responsible for instantiating, configuring, and assembling the beans. The container gets its instructions on what objects to instantiate, configure, and assemble by reading configuration metadata. The configuration metadata is represented in XML, Java annotations, or Java code. It lets you express the objects that compose your application and the rich interdependencies between those objects.  
[ `org.springframework.context.ApplicationContext`接口负责Spring IoC容器的实例化、配置、组装bean。IoC容器通过读取配置元数据中哪些对象要被创建实例、要配置、要装配的指令，配置元数据可以由XML文件、Java注解或者Java代码的方式。IoC容器允许你自己定义组成应用程序的对象以及这些对象之间丰富的相互依赖关系。]  
  
Several implementations of the `ApplicationContext` interface are supplied with Spring. In stand-alone applications, it is common to create an instance of `ClassPathXmlApplicationContext` or `FileSystemXmlApplicationContext`. While XML has been the traditional format for defining configuration metadata, you can instruct the container to use Java annotations or code as the metadata format by providing a small amount of XML configuration to declaratively enable support for these additional metadata formats.
[Spring提供了几个`ApplicationContext`接口的实现，在单体应用中，通常会创建`ClassPathXmlApplicationContext`和`FileSystemXmlApplicationContext`的实例。XML一直是传统的定义配置元数据的格式，但你也可以通过提供少量XML配置方式来提供这些额外的元数据格式，然后让容器用Java注解或者代码作为元数据格式。]  
  
In most application scenarios, explicit user code is not required to instantiate one or more instances of a Spring IoC container. For example, in a web application scenario, a simple eight (or so) lines of boilerplate web descriptor XML in the web.xml file of the application typically suffices (see [Convenient ApplicationContext Instantiation for Web Applications](https://docs.spring.io/spring/docs/5.2.1.RELEASE/spring-framework-reference/core.html#context-create)). If you use the [Spring Tool Suite](https://spring.io/tools) (an Eclipse-powered development environment), you can easily create this boilerplate configuration with a few mouse clicks or keystrokes.  
[在大多数应用场景中，不需要显示的用户代码来实例一个或多个Spring的IoC容器。例如，在web应用程序场景中，在应用程序的web.xml文件中使用(大约)8行简单的XML标签样板通常就足够了(请参考[web程序ApplicationContext实例化的简单示例](https://docs.spring.io/spring/docs/5.2.1.RELEASE/spring-framework-reference/core.html#context-create))。如果你使用的[Spring Tool Suite](https://spring.io/tools)(一个Eclipse支持的开发环境)，那你只需要简单的点几下鼠标就可以创建一个模板。]  

The following diagram shows a high-level view of how Spring works. Your application classes are combined with configuration metadata so that, after the `ApplicationContext` is created and initialized, you have a fully configured and executable system or application.  
[下图是Spring如何工作的高级视图，你的应用程序类和Spring的元数据配置文件相结合，然后在`ApplicationContext`创建完并初始化后，你就可以得到一个已经完全配置好并且可以直接运行的程序了。]
![img](https://raw.githubusercontent.com/wirechen/github-readme/master/img/container-magic.png)  
*Figure 1. The Spring IoC container*  

#### [1.2.1. Configuration Metadata[配置元数据]](https://docs.spring.io/spring/docs/5.2.1.RELEASE/spring-framework-reference/core.html#beans-factory-metadata)  
