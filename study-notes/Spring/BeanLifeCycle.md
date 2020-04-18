## Bean life cycle

* When container starts – a Spring bean needs to be instantiated, based on Java or XML bean definition. It may also be required to perform some post-initialization steps to get it into a usable state. Same bean life cycle is for spring boot applications as well.

* After that, when the bean is no longer required, it will be removed from the IoC container.

* Spring bean factory is responsible for managing the life cycle of beans created through spring container.

1.1. Life cycle callbacks

Spring bean factory controls the creation and destruction of beans. To execute some custom code, it provides the call back methods which can be categorized broadly in two groups:

    Post-initialization call back methods
    Pre-destruction call back methods

## Life cycle callback methods

Spring framework provides following 4 ways for controlling life cycle events of a bean:

* InitializingBean and DisposableBean callback interfaces
* Aware interfaces for specific behavior
  Custom init() and destroy() methods in bean configuration file
* @PostConstruct and @PreDestroy annotations

### InitializingBean and DisposableBean
* InitializeBean has afterPropertieSet() method.
* DisposableBean has destroy() method.

```
public class DemoBean implements InitializingBean, DisposableBean 
{
    //Other bean attributes and methods 
     
    @Override
    public void afterPropertiesSet() throws Exception
    {
        //Bean initialization code
    }
     
    @Override
    public void destroy() throws Exception 
    {
        //Bean destruction code
    }
}
```
2.3. Custom init() and destroy() methods

The default init and destroy methods in bean configuration file can be defined in two ways:

    Bean local definition applicable to a single bean
    Global definition applicable to all beans defined in beans context

2.3.1. Bean local definition

Local definition is given as below.
beans.xml
```
<beans>
 
    <bean id="demoBean" class="com.howtodoinjava.task.DemoBean"
                    init-method="customInit"
                    destroy-method="customDestroy"></bean>
 
</beans>
```
Java program to show methods configured in bean XML configuration file.
```
DemoBean.java
package com.howtodoinjava.task;
 
public class DemoBean 
{
    public void customInit() 
    {
        System.out.println("Method customInit() invoked...");
    }
 
    public void customDestroy() 
    {
        System.out.println("Method customDestroy() invoked...");
    }
}
```

### @PostConstruct and @PreDestroy

Spring 2.5 onwards, you can use annotations also for specifying life cycle methods using @PostConstruct and @PreDestroy annotations.

* @PostConstruct annotated method will be invoked after the bean has been constructed using default constructor and just before it’s instance is returned to requesting object.

* @PreDestroy annotated method is called just before the bean is about be destroyed inside bean container.

Java program to show usage of annotation configuration to control using annotations.
```
package com.howtodoinjava.task;
 
import javax.annotation.PostConstruct;
import javax.annotation.PreDestroy;
 
public class DemoBean 
{
    @PostConstruct
    public void customInit() 
    {
        System.out.println("Method customInit() invoked...");
    }
     
    @PreDestroy
    public void customDestroy() 
    {
        System.out.println("Method customDestroy() invoked...");
    }
}
```