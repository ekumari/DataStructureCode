# Spring Session

## Example:

```
public interface sim{
    void calling();
    void data();
}
```

* Airtel implements Sim and override all the method of sim interface.

```
public class Airtel implements sim{
    @override
    public void calling(){
        System.out.println("Calling using airtel sim");
    }
    @public void data(){
        System.out.println("Browsing internet using airtel sim");
    }
}
```
* Vodafone implements Sim and override all the method of sim interface.

```
public class Vodafone implements sim{
    @override
    public void calling(){
        System.out.println("Calling using vodafone sim");
    }
    @public void data(){
        System.out.println("Browsing internet using vodafone sim");
    }
}
```
* Main Class - Mobile

```
public class Mobile{
    public static void main(String args[]){
        Airtel airtel = new Airtel(); - Tight coupling, bad code, hard-coding
        airtel.calling();
        airtel.data();
    }
}
```
* Tomorrow I don't want to use airtel sim, vodafone is providing unlimitted data. I want to use vodafone feature. So I have to make changes to source code without that I can't have vodafone. right.

```
public class Mobile{
    public static void main(String args[]){
        Vodafone vodafone = new Vodafone();
        vodafone.calling();
        vodafone.data();
    }
}
```
* Use Interface reference
```
public class Mobile{
    public static void main(String args[]){
        Sim sim = new Vodafone();
        sim.calling();
        sim.data();

        <!-- Sim sim = new Airtel();
        sim.calling();
        sim.data(); -->
    }
}
```
## Problem

Don't touch the source code, rather make it configurable.

Solution: Spring framework

* Spring Framework 

    * Create object
    * Manage Object
    * Help our application to make configurable
    * Manage dependencies (Powerful feature)

How Spring is going to create object and manage objects ?

* Create config file: mention all the class for which you want to create object.
* Spring has IoC container and doesn't depend on anything.
* IoC container read your config file and create objects for them and manage them inside IoC container.
* Objects which spring creates - called a Bean.

### How To use created object/Beans ?

* Use getBean('class id');

### How to use IoC Container ?

* 2 Types of IOC Container

    * BeanFactory (Interface)
    * ApplicationContext (Interface)

* Use IoC container using BeanFactory or ApplicationContext.
* ApplicationContext extends from BeanFactory so it can do all the things which BeanFactory does, and provide some additional features.

* ClassPathXMLApplicationContext is the implementations of ApplicationContext.

Spring Code
```
public static void main(){
    ApplicationContext context = new ClassPathXMLApplicationContext("beans.xml");
    Sim sim = context.getBean("sim", Sim.class); // return sim interface reference
    sim.calling();
    sim.data();

}

beans.xml

<bean id="sim" class="com.demo.Airtel">
</bean>
```
Spring Inversion Of Control 

* Framework is creating object, injecting dependency and managing object for us, that's why it is called inversion of control
