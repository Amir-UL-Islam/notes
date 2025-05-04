> Problem:

1. Split Brain
2. Network Partitioning


> Why Distributed System is HARD

1. Performance lead to Shading
2. Faults lead to Tolerance 
3. Replica lead to Inconsistency\
4. Consistency lead to lack of Performance [And our main goal was Improve Performance]



>  Failover 

**Failover** is the ability to seamlessly and automatically switch to a reliable backup system. Either redundancy or moving into a standby operational mode when a primary system component fails should achieve failover and reduce or eliminate negative user impact.
![[Screenshot 2024-11-28 at 1.59.31 PM.png]]
Service Discovery Pattern
Service Oriented Architecture => You build a service for reusability but you don't know where to user.![[Screenshot 2024-11-28 at 5.54.55 PM.png]]NoSuchBeanException[When i try to autowaire a class that is not annotated with @Component or thers]


NoUnincBeanExceptoin[When 2 class is implemented same Interface] Use Qualifer, or make it primary


BeanCreationExctpoin @Lazy
BeanInstantiationExceptoion

## 1. Constructor Throws an Exception

```
import org.springframework.stereotype.Service;

@Service
public class MyService {
    public MyService() {
        throw new RuntimeException("Constructor failed!");
    }
}
```

Running the above Spring Boot application will result in a BeanInstantiationException due to the exception thrown in the constructor.

```
Caused by: org.springframework.beans.BeanInstantiationException: Failed to instantiate [com.example.springboot.MyService]: Constructor threw exception
```

## 2. Abstract Class or Interface 

If you mistakenly annotate an abstract class or an interface with [@Component](https://www.javaguides.net/2018/11/spring-component-annotation-example.html) or [@Service](https://www.javaguides.net/2018/11/spring-service-annotation.html), Spring will fail to create a bean instance.

```
import org.springframework.stereotype.Service;

@Service
public abstract class AbstractService {
    // some methods...
}
```

## 3. No Default Constructor 

A class without a default constructor, where Spring doesn't have any way to provide the required arguments, can also cause this issue.

```
package com.example.demo;

import org.springframework.stereotype.Component;

@Component
public class MyComponent {
    private final String name;

    public MyComponent(String name) {
        this.name = name;
    }
}
```



Repository>Curd> PagingAndSorting>JpaRepository


Under some circumstances, a bug in the JVM can cause the JVM to crash in attach mode. To avoid this problem, start the JVM with the VM parameter "-Xshare:off".