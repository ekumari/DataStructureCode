# Bean Scope

Control the scope of the objects created from a particular bean definition.
Spring Framework supports 6 scopes, four of which available with web-aware "ApplicationContext".

> Also, Create a custom scope.

## 1.1. The Singleton Scope

**Defining a bean with singleton scope means the container creates a single instance of that bean, and all requests for that bean name will return the same object, which is cached. Any modifications to the object will be reflected in all references to the bean. This scope is the default value if no other scope is specified**

Only one shared instance of a singleton bean is managed, and all requests for beans with an ID or IDs that match that bean definition result in that one specific bean instance being returned by the Spring container.

![Image of Yaktocat](..\images\singleton.png)

This spring singleton scope is different from Singleton Pattern. As, Singleton pattern is having single object per class and Spring Singleton Scope is having single instance/object per-bean and per-container. This means, if you define single bean for a particular class, Spring container will create one and only one instance of the class defined by bean definition.

> Singleton Scope is the default scope in Spring.

```
<bean id="accountService" class="com.something.DefaultAccountService"/>

<!-- the following is equivalent, though redundant (singleton scope is the default) -->
<bean id="accountService" class="com.something.DefaultAccountService" scope="singleton"/>
```
```
    DefaultAccountService objA = (DefaultAccountService) context.getBean("accountService");

      objA.setMessage("I'm object A");
      objA.getMessage();

      DefaultAccountService objB = (DefaultAccountService) context.getBean("accountService");
      objB.getMessage()
```

> Object A sets the message and since, the object is shared and single. So it is available to object B.

Output:
```
Your Message : I'm object A
Your Message : I'm object A
```

## 1.2. The Prototype Scope

Creates new bean each a new request for specific bean is made. That is, the bean is injected into another bean or you request it through a getBean() method call on the container. As a rule, you should use the prototype scope for all stateful beans and the singleton scope for stateless beans.

![Image of Yaktocat](..\images\prototype.png)

Example of Prototype: 

```
<bean id="accountService" class="com.something.DefaultAccountService" scope="prototype"/>
```
```
    DefaultAccountService objA = (DefaultAccountService) context.getBean("accountService");

      objA.setMessage("I'm object A");
      objA.getMessage();

      DefaultAccountService objB = (DefaultAccountService) context.getBean("accountService");
      objB.getMessage()
```

Output:  Creates a new object per request to bean and value is not shared.

```
Your Message : I'm object A
Your Message : null
```

---
# Web Aware Scopes

## 1.1. Request Scope

The request scope creates a bean instance for a single HTTP request (per HTTP request).

## 1.2. Session Scope

Session scope creates for an HTTP Session (per session).

## 1.3. Application Scope

Creates the bean instance for the lifecycle of a ServletContext 

## 1.4. Websocket Scope

Creates it for a particular WebSocket session.