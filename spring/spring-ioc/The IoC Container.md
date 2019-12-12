#### [1. The IoC Container-IOC容器](https://docs.spring.io/spring/docs/5.2.1.RELEASE/spring-framework-reference/core.html)
This chapter covers Spring’s Inversion of Control (IoC) container.  
[本章节讨论了控制反转（IOC）容器].  
#### [1.1. Introduction to the Spring IoC Container and Beans-介绍spring的IOC容器和Bean](https://docs.spring.io/spring/docs/5.2.1.RELEASE/spring-framework-reference/core.html#beans-introduction)
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