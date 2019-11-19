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
