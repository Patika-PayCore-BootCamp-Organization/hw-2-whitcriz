
### ANSWERS TO WEEK-2 HOMEWORK QUESTIONS

---

#### Q1 - IOC and DI means ?

---

**Inversion of Control (IoC)** is a programming technique in which object coupling is bound at run time by an assembler object and is typically not known at compile time using static analysis. While the flow of the business logic is determined by objects that are statically assigned to one another without inversion of control, with inversion of control, the flow depends on the object graph that is instantiated by the assembler and is made possible by object interactions being defined through abstractions.  

We have several purposes and advantages with inversion control as a design guideline:
 *  We can decouple of the execution of a task from implementation.
 *  Every module can focus on what it is designed for.
 *  Modules make no assumptions about what other systems do but still rely on their contracts.
 * Replacing modules has no side effect on other modules.

We have several design principles to implement inversion of control. These are factory pattern, service locator pattern and dependency injection.

**Dependency injection (DI)** is a design pattern used to create instances of objects that other objects rely on without knowing at compile time which class will be used to provide that functionality. With DI, connecting objects with other objects, or “injecting” objects into other objects, is done by an assembler rather than by the objects themselves. In other words, dependency Injection pattern will change binding on Objects at Compile time to Run time. Hence we can reusable the class more than before. In Case of change in business requirement no code change required. Unit testing also easy to perform with dependency injection. For example, class A is dependent on B. So rather than creating object of B within the class “A”, we can inject the dependencies via a constructor or setter injection.

We can implement DI in three different ways:

• *Constructor Injection :* Constructor Injection means to Inject or Pass dependent objects as a Constructor argument.

• *Setter Injection :* Dependent objects will get created from assembler and pass it to the setter method to initialize at runtime.

• *Interface Injection :* We implement an interface from the IOC framework. IOC framework will use the interface method to inject the object in the main class. It is much more appropriate to use this approach when you need to have some logic that is not applicable to place in a property. Such as logging support.


--- 

#### Q2 - Spring Bean Scopes ?

---

The Spring Framework creates beans for us, after we start a Spring application. These can be application beans that we have defined or beans that are part of the framework.  The Spring Bean scope defines the lifecycle and visibility of that bean and  answers to how long does the bean live, how many instances are created, how is the bean shared questions in the context which we use the bean instance. 

Spring provides `@Scope` annotation to mark a bean scope. The Spring Framework needs to associate a scope with the bean. So, if we do not clearly define a scope, the Spring Framework will create the bean with the Singleton scope. In this condition, `@Scope` annotation is unnecessary. 

While a bean's default scope is  Singleton scope, we can use some other scopes in Spring too. A Spring Bean can be associated with the following scopes:

- Singleton
- Prototype
- Request
- Session
- Global session
- WebSocket
- Application

Request, Session, and Global session are only available for beans using a web-aware Spring ApplicationContext implementation (such as XmlWebApplicationContext). If we try using these scopes with regular Spring IoC containers such as the XmlBeanFactory or ClassPathXmlApplicationContext, we will get an IllegalStateException complaining about an unknown bean scope.

In order to support the web-scoped beans, some minor initial configuration is necessary before you can set about defining your bean definitions.


| Spring Bean Scope Types | Usage and Definitions |
|-------------------------|-----------------------|
| **Singleton Scope** | We call the scope `Singleton` because the spring container will create a single instance of the bean only once. This single instance will be cached of such singleton beans in memory stored and the framework returns this cached instance,  each time the bean with id or ids matching this bean definition is requested or referenced by the application.  Any modifications to the object will be reflected in all references to the bean. The scopes.xml file should contain the xml definitions of the beans used.The singleton scope should be used for stateless beans. |
| **Prototype Scope** | A bean with the prototype scope will return a different bean instance every time a request for that specific bean is made (it means that it is injected into another bean or requested via a programmatic getBean() method call on the container). It is defined by setting the value prototype to the `@Scope` annotation in the bean definition. We should use this scope for all beans which are stateful. Two objects requesting the same bean name with the prototype scope will have different states as they are no longer referring to the same bean instance. The scopes.xml file should contain the xml definition for the bean with the prototype scope. |
| **Request Scope** | The request scope is a web-scoped bean and creates a bean instance for a single HTTP request. We can change or dirty the internal state of the instance that is created as much as we want, safe in the knowledge that other requests that are also using instances created off the back of the same bean definition will not be seeing these changes in state since they are particular to an individual request. When the request is finished processing, the bean in this scope will be discarded. We can define the bean with the request scope using the `@Scope` annotation and also  use a `@RequestScope` composed annotation that acts as a shortcut while defining a request scope for the bean. |
| **Session Scope** | The session scope is a web-scoped bean and creates a bean instance for an HTTP Session. Just like *request-scoped* beans, we can change the internal state of the instance that is created as much as you want, safe in the knowledge that other HTTP `Session` instances that are also using instances created off the back of the same bean definition will not be seeing these changes in state since they are particular to an individual HTTP `Session`. When the HTTP `Session` is eventually discarded, the bean that is scoped to that particular HTTP `Session` will also be discarded. We can define the bean with the session scope using the `@Scope` annotation and also  use a `@SessionScope` composed annotation that acts as a shortcut while defining a session scope for the bean.  |
| **Global Session Scope** | The global session scope is a web-scoped bean and it is for portlets.It is similar to the standard HTTP Session scope, and just only makes sense in the context of portlet-based web applications. The portlet specification defines the notion of a global Session that is shared amongst all of the various portlets that make up a single portlet web application. Beans defined at the global session scope are scoped (or bound) to the lifetime of the global portlet Session. |
| **WebSocket Scope** | When first accessed, WebSocket scoped beans are stored in the WebSocket session attributes. The same instance of the bean is then returned each time that bean is accessed during the entire WebSocket session. We can also say that it shows singleton behavior, however limited to a WebSocket session only. |
| **Application Scope** | The application scope creates the bean instance for the lifecycle of a ServletContext, and the websocket scope creates it for a particular WebSocket session. This is similar to the singleton scope, but there is an important difference with regards to the scope of the bean. When beans are application scoped, the same instance of the bean is shared across multiple servlet-based applications running in the same ServletContext, while singleton scoped beans are scoped to a single application context only. We can define the bean with the application scope using the `@Scope` annotation and also  use a `@ApplicationScope` composed annotation that acts as a shortcut while defining an application scope for the bean. |



---

#### Q3 - What does @SpringBootApplication do ?

---

The `@SpringBootApplication` annotation is often placed on your main class, and it implicitly defines a base “search package” for certain items. For example, if you are writing a JPA application, the package of the `@SpringBootApplication` annotated class is used to search for `@Entity` items. Using a root package also allows component scan to apply only on your project.

 Many Spring Boot developers like their apps to use auto-configuration, component scan and be able to define extra configuration on their "application class". A single `@SpringBootApplication` annotation combines  `@SpringBootConfiguration` `@ComponentScan` and `@EnableAutoConfiguration`. It implicitly scan application classpath and auto configuration based on jars exist in classpath like if we have spring boot starter jpa jar in classpath. It can also provides aliases to customize the attributes of `@EnableAutoConfiguration` and `@ComponentScan`. 

A detailed examining of these combining annotations:

**`@EnableAutoConfiguration :`** 
It enables Spring Boot's auto-configuration mechanism, means that it attempts to automatically configure our Spring application based on the jar dependencies that has been added. For instance, if `HSQLDB` is on our classpath, and we have not manually configured any database connection beans, then Spring Boot auto-configures an in-memory database.

Auto-configuration is non-invasive. At any point, we can define our own configuration to replace specific parts of the auto-configuration. For example, if we add our own `DataSource` bean, the default embedded database support backs away.
f we find that specific auto-configuration classes that we do not want are being applied, we can use the exclude attribute of `@SpringBootApplication` to disable them. We can also control the list of auto-configuration classes to exclude by using the `spring.autoconfigure.exclude` property.

**`@ComponentScan :`**: 
This enables `@Component` scan on the package where the application is located. The underlying component scan configuration of `@SpringBootApplication` defines exclude filters that are used to make sure slicing works as expected. If you are using an explicit `@ComponentScan` directive on your `@SpringBootApplication`-annotated class, be aware that those filters will be disabled. If you are using slicing, you should define them again.

 **`@SpringBootConfiguration :`** 
It enables registration of extra beans in the context or the import of additional configuration classes. An alternative to Spring’s standard `@Configuration` that aids configuration detection in your integration tests.


None of these features are mandatory and we may choose to replace this single annotation by any of the features that it enables. For example, we may not want to use component scan or configuration properties scan in our application.


---

#### Q4 - What is Spring AOP ? Where and How to use it ?

---

Spring Aspect Oriented Programming (AOP) helps in breaking down the logic of the program into distinct parts called as concerns. Cross-cutting concerns is the functions which span multiple points of an application. The cross-cutting concerns help in increasing the modularity and are conceptually separate from the program's business logic. Besides, a cross-cutting is a concern that affects the whole application and it should be centralized in one location in code as possible such as authentication, transaction management, logging,security.

While the key unit of modularity in OOP is the class, the unit of modularity in AOP is the aspect. It is used to increase modularity by cross-cutting concerns. There are various common good examples of aspects like logging, auditing, declarative transactions, security, caching.

Dependency Injection helps you decouple your application objects from each other and AOP helps you decouple cross-cutting concerns from the objects that they affect. 

We don't have to call methods from the method with AOP. Now we can define the additional concern in the method of a class. Its entry is given in the xml file. In the future, if client wants a change, we need to change only in the xml file. So, maintenance is easy in AOP.

Spring AOP module provides interceptors to intercept an application, means dynamically adding the additional concern before, after or around the actual logic. For example, when a method is executed, you can add extra functionality before or after the method execution.

**Where use AOP :**
AOP is mostly used in following cases:
- to provide declarative enterprise services such as declarative transaction management.
- It allows users to implement custom aspects.

We can implement Spring Framework AOP in pure Java, it doesn’t require to the special compilation process. It is the best choice for use in a J2EE web container or application server because it doesn’t require to control the class loader hierarchy.

**How to use Spring AOP :**
Even if the widely used approach is *Spring AspectJ Annotation Style*, the three ways to use Spring AOP are given below:
1. Old Style (dtd based)
2. Spring AspectJ Annotation Style
3. Spring XML Configuration-Style (schema based)


---

#### Q5 - What is Singleton and where to use it ?

---

The **Singleton** pattern will ensure that there is only one instance of a class is created in the JVM. After first time, if we try to instantiate the Singleton class, the new variable also points to the first instance created. So whatever modifications we do to any variable inside the class through any instance, it affects the variable of the single instance created and is visible if we access that variable through any variable of that class type defined. It is used to provide global point of access to the object. In terms of practical use Singleton patterns are used in logging, caches, thread pools, configuration settings, device driver objects, database connections.

The key points while designing a singleton class:

- Make constructor private.
- Write a static method that has return type object of this singleton class. The concept of Lazy initialization is used to write this static method.

 The difference between singleton and the normal class in Java is in terms of instantiation as for normal class we use constructor, whereas for singleton class we use `getInstance()` method. In general, in order to avoid confusion, we may also use the class name as method name while defining this method. 



---

#### Q6 - What is Spring Boot Actuator and Where to use it ?

---

Spring Boot Actuator is mainly used to expose operational information about the running application — health, metrics, info, dump, env. and provides secured endpoints for monitoring and managing our Spring Boot application. By default, all actuator endpoints are secured. Monitoring our app, gathering metrics, understanding traffic, or the state of our database become trivial with this dependency. The main advantage is that we can get production-grade tools without having to actually implement these features ourselves. If we want to get production-ready features in our application, we should use the Spring Boot actuator.

Spring Boot includes a number of built-in endpoints and lets you add your own. Each individual endpoint can be enabled or disabled and exposed (made remotely accessible) over HTTP endpoints or JMX beans. An endpoint is considered to be available when it is both enabled and exposed. To enable Spring Boot actuator endpoints to our application, we need to add the Spring Boot Starter actuator dependency in our build configuration file. The built-in endpoints will only be auto-configured when they are available. Most applications choose exposure via HTTP, where the ID of the endpoint along with a prefix of `/actuator` is mapped to a URL. For instance, by default, the health endpoint is mapped to `/actuator/health`.

Spring Boot Actuator provides dimensional metrics by integrating with the *micrometer*. The micrometer is integrated into Spring Boot. It is the instrumentation library powering the delivery of application metrics from Spring. It provides vendor-neutral interfaces for *timers, gauges, counters, distribution summaries,* and *long task timers* with a dimensional data model.

Spring Boot provides a flexible audit framework that publishes events to an *AuditEventRepository.* It automatically publishes the authentication events if spring-security is in execution.


---

#### Q7 - What is the primary difference between Spring and Spring Boot ?

---

Spring Boot is built on top of the conventional spring framework, widely used to develop REST APIs. It is a microservice-based framework and making a production-ready application in very less time. 
So, the primary difference between Spring and Spring Boot is  *Autoconfiguration in Spring Boot.*  

Other important differences between Spring and Spring Boot:

| SPRING | SPRING BOOT |
|--------|-------------|
| To run the Spring application, needed to set the server explicitly. | Spring Boot provides embedded servers such as Tomcat and Jetty etc. |
| To run the Spring application, a deployment descriptor is needed. | There is no requirement for a deployment descriptor. |
| To create a Spring application, needed to write boilerplate code. | It eliminates most of the boilerplate code. |
| It doesn’t provide support for the in-memory database. | It provides support for the in-memory database, such as H2. |
| It creates a loosely coupled application. | It creates a stand-alone application. |


---

#### Q8 - Why to use VCS ?

---

Version Control is used to track and control changes to source code. Complex code development is almost impossible without a Version Control System (VCS). There are several advantages of using a VCS for our projects:  
- Collaboration with team
- Tracked Changes with answers to Who, What, When, Why 
- Storing Versions properly
- Restoring previous versions easily
- Understanding what happened before with short descriptions and even with text files in it
- Backup
- Concurrent Development
- Automation


---

#### Q9 - What are SOLID Principles ? Give sample usages in Java ?

---

`*SOLID Principles* are five design principles of Object-Oriented class design and best practices to follow while designing a class structure. They encourage us to create understandable, readable, and testable code by helping in reducing tight coupling so that many developers can collaboratively work on.

They are:

**Single Responsibility Principle (SRP) :** A class should do one thing and therefore it should have only a single reason to change. In more technical words, only one potential change (database logic, logging logic, and so on.) in the software’s specification should be able to affect the specification of the class. 
Everything in the class should be related to that single purpose. It does not mean that your classes should only contain one method or property. There can be a lot of members as long as they relate to the single responsibility. It may be that when the one reason to change occurs, multiple members of the class may need modification. It may also be that multiple classes will require updates. Use layers in your application and break great classes into smaller classes or modules.

```
 public class Book{ 
     private String name; 
     private String author; 
     private String text; 
     
     //constructor, getters and setters 
     
     // methods that directly relate to the book properties 
     
     public String replaceWordInText(String word){ 
         return text.replaceAll(word, text); 
     } 
     public boolean isWordInText(String word){ 
         return text.contains(word); 
     } 
  }

```

```
 
 class Book {
     String name;
 	 String authorName;
 	 int year;
 	 int price;
 	 String isbn;
     
     public Book(String name, String authorName, int year, int price, String isbn) {
 	     this.name = name;
 		 this.authorName = authorName;
 		 this.year = year;
         this.price = price;
 		 this.isbn = isbn;
 	 }
 }
 
 
 public class Invoice {
     private Book book;
 	 private int quantity;
 	 private double discountRate;
 	 private double taxRate;
 	 private double total;
      
     public Invoice(Book book, int quantity, double discountRate, double taxRate){
 	     this.book = book;
 	 	 this.quantity = quantity;
 	 	 this.discountRate = discountRate;
 	 	 this.taxRate = taxRate;
 	 	 this.total = this.calculateTotal();
 	 }
 
     public double calculateTotal(){
 	     double price = ((book.price - book.price * discountRate) * this.quantity);
         double priceWithTaxes = price * (1 + taxRate);
         return priceWithTaxes;
 	 }
 }

```

**Open-Closed Principle :** Classes should be open for extension but closed for modification. *“Open to extension”* means that you should design your classes so that new functionality can be added as new requirements are generated. *“Closed for modification”* means that once you have developed a class you should never modify it, except to correct bugs. 

Generally you achieve this by referring to abstractions for dependencies, such as interfaces or abstract classes, rather than using concrete classes. Functionality can be added by creating new classes that implement the interfaces.
Applying OCP to your projects limits the need to change source code once it has been written, tested, and debugged. This reduces the risk of introducing new bugs to existing code, leading to more robust software.

```
 void checkOut(Receipt receipt) { 
     Money total = Money.zero; 
     for (item : items) { 
           total += item.getPrice();
           receipt.addItem(item); 
      } 
     Payment p = acceptCash(total); 
     receipt.addPayment(p); 
  }
```
In order to  add credit card support with OCP Principle;
```
public interface PaymentMethod {void acceptPayment(Money total);} 

void checkOut(Receipt receipt, PaymentMethod pm) { 
    Money total = Money.zero; 
    for (item : items) { 
        total += item.getPrice(); 
        receipt.addItem(item); 
     } 
    Payment p = pm.acceptPayment(total); 
    receipt.addPayment(p); 
}

```

**Liskov Substitution Principle (LSP) :** Subclasses should be substitutable for their base classes. This is the expected behavior, because when we use inheritance we assume that the child class inherits everything that the superclass has. The child class extends the behavior but never narrows it down.
Therefore, when a class does not obey this principle, it leads to some nasty bugs that are hard to detect.
Liskov's principle is easy to understand but hard to detect in code.

 ```
 public class MotorCar implements Car{ 
     private Engine engine; 
     
     //Constructors, getters + setters 

     public void turnOnEngine(){ 
         //turn on the engine!
         engine.on(); 
     } 
     
     public void accelerate(){
         //move forward! 
         engine.powerOn(1000); 
     } 
 }

 
 Public class ElectricCar implements Car{
     public void turnOnEngine(){
         throw new AssertionError("I don't have an engine!");
     }
     
     publicvoidaccelerate(){
         //this acceleration is crazy!
     }
 }

```

By throwing a car without an engine into the mix, we are inherently changing the behavior of our program. This is a  violation of Liskov substitution. One possible solution would be to rework our model into interfaces that take into account the engine-less state of our Car.

**Interface Segregation Principle (ISP) :** Many client-specific interfaces are better than one general-purpose interface. Clients should not be forced to implement a function they do not need. Using this principle helps in reducing the side effects and frequency of required changes.

An example about different ATM functionality depend on separate Messengers:

```
public interface LoginMessenger{ 
    askForCard(); 
    tellInvalidCard(); 
    askForPin(); 
    tellInvalidPin(); 
}
 
public interface WithdrawalMessenger{ 
     tellNotEnoughMoneyInAccount(); 
     askForFeeConfirmation();
}
 
public class EnglishMessenger implements LoginMessenger, WithdrawalMessenger{ ... }

```

**Dependency Inversion Principle (DIP) :** Our classes should depend upon interfaces or abstract classes instead of concrete classes and functions. Two key points are here to keep in mind about this principle :
-  High-level modules/classes should not depend on low-level modules/classes. Both should depend upon abstractions.
-  Abstractions should not depend upon details. Details should depend upon abstractions.

```
publicinterfaceKeyboard{ }

publicclassWindows98Machine{
    private final Keyboard keyboard;
    private final Monitor monitor;
    
    public Windows98Machine(Keyboard keyboard, Monitor monitor){
        this.keyboard = keyboard;
        this.monitor = monitor;
    }
}

public class StandardKeyboard implements Keyboard{  }

```
Our classes in this example are decoupled and communicate through the `Keyboard` abstraction. If we want, we can easily switch out the type of keyboard in our machine with a different implementation of the interface. 



---

#### Q10 - What is RAD model ?

---

**Rapid Application Development (RAD) model** is a Software Development Life Cycle Model based on prototyping and iterative development with no specific planning involved. A prototype is a working model that is functionally equivalent to a component of the product. RAD model uses minimal planning in favor of rapid prototyping, so there is less attention paid to the planning and more priority is given to the development tasks. The process of writing the software itself involves the planning required for developing the product. The model targets at developing software in a short span of time. In other words, in the RAD model, the functional modules are developed in parallel as prototypes and are integrated to make the complete product for faster product delivery. Since there is no detailed preplanning, it makes it easier to incorporate the changes within the development process.

 We can say that any software project that is divisible into smaller modules, which are capable to be assigned independently to different teams like developers, domain experts, customer representatives and other IT teams can be developed using RAD Model which is iterative and incremental. All these various modules are ultimately combined to get the final product.

RAD focuses on gathering customer requirements through workshops or focus groups, early testing of the prototypes by the customer using iterative concept, reuse of the existing prototypes (components), continuous integration and rapid delivery.

The most important aspect for this model to be successful is to make sure that the prototypes developed are reusable.This model allows rapid change and development of the components or product, encourages active customer feedback by providing the early visibility of the product to a customer.

Despite all the advantages of the RAD Model, we can not use this model for some cases like small team, low-budget projects.

RAD model distributes the analysis, design, build and test phases into a series of short, iterative development cycles. It has the following phases:

- **Business Modeling :** The information flow among business channels is defined by answering questions like what data drives the business process, what data is generated, who generates it, where does the information go, who process it, what are the factors driving successful flow of information. 
	
- **Data Modeling :** The information from the previous, Business Modeling, phase is analyzed to form sets of data objects vital for the business. The attributes of all data sets is identified and defined. The relation between these data objects are established and defined in detail in relevance to the business model.
	
- **Process Modeling :** The data object sets defined from the previous phase are converted to establish the business information flow needed to achieve specific business objectives as per the business model. Then, the process model for any changes or enhancements to the data object sets is defined. Process descriptions for adding, deleting, retrieving or modifying a data object are given.
	
- **Application Generation :** The actual system is built and coding is done by using automation tools to convert process and data models into actual prototypes.

- **Testing and Turnover :**  Even though the prototypes are independently tested during every iteration and hence the whole testing time is reduced in this model, the data flow and the interfaces between all components need to be completely tested with whole test coverage. 

---

#### Q11 - What is Spring Boot starter ? How is it useful ?

---

Spring Boot starters were built to reduce dependency management time for developers. Spring Boot Starter is a  dependency descriptor and Starter POMs are a set of convenient dependency descriptors that we can include in our application. We have more than 30 Spring Boot built-in starters that allow us to add jars in the classpath. Spring Boot built-in starters make development easier and rapid. In the Spring Boot Framework, all the starters follow a similar naming pattern: `spring-boot-starter-#,` where `#` denotes a particular type of application. For example, if we want to use Spring and JPA for database access, we need to include the `spring-boot-starter-data-jpa` dependency in our `pom.xml` file of the project.

Some of built-in starters are:
	
- **Core Starter - `spring-boot-starter`** is for including auto-configuration support, logging, and YAML. 
	
- **Web Starter - `spring-boot-starter-web`**  is for building the web application, including RESTful applications using Spring MVC. It uses Tomcat as the default embedded container.
	
- **Test Starter - `spring-boot-starter-test`** is for testing Spring Boot applications with libraries, including JUnit, Hamcrest, and Mockito.
	
- **Data JPA Starter - `spring-boot-starter-data-jpa`** is for Spring Data JPA with Hibernate, helps with specifying the database vendor, URL connection, and credentials. 
	
- **Mail Starter - `spring-boot-starter-mail`** is for supporting Java Mail and Spring Framework's email sending.
	
- **Security Starter - `spring-boot-starter-security`** is for Spring Security.

- 	**Cache Starter - `spring-boot-starter-cache`** is for enabling Spring Boot cache mechanism.

There are several advantages of using Starters like:
- Increasing overall productivity by reducing dependency management time for developers
- Easier POM management because of adding less required dependencies
- Tested, production-ready and supported dependency configurations.


---

#### Q12 - What is Caching ? How can we achive caching in Spring Boot ?

---

A cache is a high-speed data storage layer which stores a subset of data, typically transient in nature, so that future requests for that data are served up faster than is possible by accessing the data’s primary storage location. Caching is the process of storing and accessing copies of files or simply data in a cache, or temporary storage location in order to access them more quickly. Normally, the data required for any process resides in the main memory. However, it is transferred to the cache memory, that is a part of temporary memory, RAM, temporarily if it is used frequently enough.  It lies between the application and persistence database. It stores the recently used data that reduces the number of database hits as much as possible. In other words, caching is storing data for future reference.
A cache's primary purpose is to increase data retrieval performance by reducing the need to access the underlying slower storage layer.

 We have four types of caching:
- **In-memory Caching** increases the performance of the application. Memcached and Redis are examples of in-memory caching. It stores key-value between application and database. Redis is an in-memory, distributed, and advanced caching tool that allows backup and restore facility. We can manage cache in distributed clusters, also.
	
- **Database Caching** is a mechanism that generates web pages on-demand (dynamically) by fetching the data from the database. It is used in a multi-tier environment that involved clients, web-application server, and database. This caching improves scalability and performance by distributing a query workload. The most popular database caching is the first level cache of Hibernate.
	
- **Web server Caching** is a mechanism that stores data for reuse. For example, a copy of a web page served by a web server. It is cached for the first time when a user visits the page. If the user requests the same next time, the cache serves a copy of the page. It avoids server form getting overloaded. Web server caching enhances the page delivery speed and reduces the work to be done by the backend server.
	
- 	**CDN Caching**  reduces the load on an application origin and improves the user experience by delivering a local copy of the content from a nearby  *cache edge* (a cache server that is closer to the end-user), or a  *Point of Presence (PoP)*  with the  *Content Delivery Network (CDN)*  component that is used in modern web applications and improves the delivery of the content by replicating commonly requested files (such as HTML Pages, stylesheet, JavaScript, images, videos, etc.) across a globally distributed set of caching servers.

Spring Framework provides caching transparently with cache abstraction. The cache abstraction mechanism allows consistent use of several caching methods with minimal impact on the code. This mechanism applies to Java methods and the main purpose of it is reducing the number of executions based on the information present in the cache. It applies to expensive methods such as CPU or IO bound.

When a method invokes, each time the abstraction applies a cache behavior to the method. It controls if the method has already been executed for the given argument and if executed, the cached result is returned without executing the actual method. Otherwise, firstly, the method executes, and the result is cached and returned to the user. This approach works only for the methods that are guaranteed to return the same output for a given input. It does not matter how many times the method executes. 

The developers take care of two things while working with cache abstractions:
1. *Cache Declaration :* identifies the methods that need to be cached.
2. *Cache Configuration :* is the backing cache where the data is stored and read from.

We can enable caching in the Spring Boot by using the **`@EnableCaching`** . This annotation  is a class-level annotation and defined in `org.springframework.cache.annotation` package. It is used together with `@Configuration` class. The auto-configuration enables caching and starts a `CacheManager`, if there is no already defined instance of `CacheManager`. It triggers a post-processor that analyzes every Spring bean for the presence of caching annotations on public methods. When such an annotation is found, a proxy is automatically created to intercept the method call and handle the caching behavior accordingly. The post-processor handles the `@Cacheable`, `@CachePut` and `@CacheEvict` annotations.  Besides, `@EnableCaching` creates an in-memory cache using `ConcurrentHashMap`  for the absence of such caching annotations. 

The caching abstraction mechanism has several Java annotations for caching declaration like:
- **`@CacheConfig`** is a class-level annotation that provides a common cache-related setting. It tells the Spring where to store cache for the class. 

- **`@Caching`** is used when we need both annotations `@CachePut` or `@CacheEvict` at the same time on the same method. Because Java does not allow multiple annotations of the same type to be declared for a given method, we use `@Caching` annotation.

- **`@Cacheable`** is a method level annotation. It defines a cache for a method's return value. The Spring Framework manages the requests and responses of the method to the cache that is specified in the annotation attribute. The `@Cacheable` annotation contains more options. For example, we can provide a cache name by using the value or cacheNames attribute. We can also specify the key attribute of the annotation that uniquely identifies each entry in the cache. If we do not specify the key, Spring uses the default mechanism to create the key. 
We can also apply a condition in the annotation by using the condition attribute. When we apply the condition in the annotation, it is called *conditional caching*.

- **`@CacheEvict`** is a method level annotation. It is used when we want to remove stale or unused data from the cache. It requires one or multiple caches that are affected by the action. We can also specify a key or condition into it. If we want wide cache eviction, the `@CacheEvict` annotation provides a parameter called `allEntries`. It evicts all entries rather than one entry based on the key. One important point about `@CacheEvict` annotation is that it can be used with void methods because the method acts as a trigger. It avoids return values. On the other hand, the annotation `@Cacheable` requires a return value that adds/updates data in the cache. 

- **`@CachePut`** is a method level annotation and used when we want to update the cache without interfering the method execution. In other words, the method will always execute, and its result will be placed into the cache. It supports the attributes of `@Cacheable` annotation, however the annotations `@Cacheable` and `@CachePut` have different behavior. There is a slight difference between them is that the `@Cacheable` annotation skips the method execution while the `@CachePut` annotation runs the method and put the result into the cache.


---

#### Q13 - What & How & Where & Why to logging ?

---

Logging is the process of creating and capturing log messages and files. Logging requires frameworks and APIs in Java and Java has a built-in logging framework in the java.util.logging package. Besides, it is possible to use third-party frameworks like Log4j, Logback, and many more for logging purposes.

Logging in Spring Boot provides tracing out of information along with a recording of any critical failure that might occur in the application during its run. Spring Boot uses Commons Logging for all internal logging but leaves the underlying log implementation open and default configurations provides a support for the use of Java Util Logging, Log4j2, and Logback. The loggers are configured the console output and also the optional file output with these default configurations. Logback comes with Spring Boot Starters by default and also supports  Java Util Logging, Commons Logging, Log4J, and SLF4J.
 
A default spring boot log file contains the following items:

- **Date and Time** provides the occurrence date and time of the log item.
- **Log Level** provides the information on what level of information the log is of. It will be one out of the 7 options , the following order of severity from low to high:
  - *TRACE*
  - *DEBUG*
  - *INFO*
  - *WARN*
  - *ERROR* 
  - *FATAL* (Logback does not have a *FATAL* level. It is mapped to *ERROR*)
  - *OFF*
- **Process ID** provides the information of the process ID on which the spring boot application is running on.
- **Separator ---**  signifies the start of actual log messages.
- **Thread Name** is enclosed within a square [] brackets and mostly contains the thread within which the logging thread or element is present.
- **Logger Name** is the penultimate element that contains the source class name.
- **Log Message** explains the methods followed in the application and helps us tracing back to the root cause if an error pops up in the application.
	
The log level here shows the importance of log messages and it can be very time-efficient for developers. For instance, when the level shows   *ERROR*,  the application should actually have encountered some serious failure. Every time looking at logs that mention some information about the process can be disturbing and consumer of time in an unefficient way. Sometimes this information may be classified as  *ERROR*  due to improper architecture and so, the logs should be carefully set up while developing the architecture of the application in order to make tracing back to the root point easier. 

When a code in the application executes with each of the classified options available, the corresponding options are validated against the level declared for the application. It is put in the log message if the severity of the level declared for application is lower than the point of code execution. The level can be declared by using the code 

`logging.level.com.<application name>=<logging level>` . 

As an example, when the code breaks and fails due to some corner cases we have not considered during code execution, the location of the code is put into the log message with the appropriate level. However, if the code execution yields a less severe level than the declared level of application, then the logging is skipped.  

Once it is determined of what to put, the application looks for the pattern declared in either the xml or in the java code and corresponding elements are extracted and noted. 

The default log configuration writes messages to the console as they are written. By default, *ERROR-level*, *WARN-level*, and *INFO-level*  messages are logged. 
We can also enable a *DEBUG* mode  by starting your application with a `--debug` flag :

`$ java -jar myapp.jar --debug`

We can also specify `debug=true` in our `application.properties`.

When the *DEBUG* mode is enabled, a selection of core loggers which are embedded container, Hibernate, and Spring Boot, are configured to output more information. However, enabling the *DEBUG* mode does not configure our application to log all messages with *DEBUG-level*.

Alternatively, we can enable a *TRACE* mode by starting our application with a `--trace` flag or specifying `trace=true` in our `application.properties`. This also enables *TRACE*  logging for a selection of core loggers  which are embedded container, Hibernate schema generation, and the whole Spring portfolio.

In case the terminal supports ANSI, color-coded output is used to aid readability. We can set `spring.output.ansi.enabled` to a supported value to override the auto-detection.
Color coding is configured by using the `%clr` conversion word. In its simplest form, the converter colors the output according to the log level:

`%clr(%5p)`

We can map of log levels to colors:

| Log Level | Color |
|------------- |--------|
| OFF | Red |
| FATAL | Red |
| ERROR | Red |
| WARN | Yellow |
| INFO | Green |
| DEBUG | Green |
| TRACE | Green |

Moreover, the color or style can be specified by providing it as an option to the conversion.

Spring Boot logs only to the console by default and does not write log files. If we want to write log files in addition to the console output, we need to set a `logging.file` or `logging.path` property (for instance, in our `application.properties`).


---

#### Q14 - What is Swagger? Have you implemented it using Spring Boot?

---

Swagger is the standard way of documenting the Standard APIs. Swagger is helpful when deploying APIs in azure. Swagger is primarily used for documenting API. For the other developers to be able to use our API, the API must be properly documented and they need to know that what the endpoints  are exposed by the API and what the operations are supported on those endpoints, what parameters they should pass, and what they will get back, what authentication methods to use. . If we want APIs to be consumed and properly used, it is very important to document the APIs.  Swagger and Open API specification are the ways to document an API specifying that what exactly APIs can do.

We can implement *Swagger* using *Spring Boot* by first adding a dependency related to Swagger to generate *Swagger Documentation*. We also need *Swagger UI* to have a visual representation of the Documentation and execute Test Requests.

We start by adding this dependency to `pom.xml` file.

```
<dependency>
 <groupId>io.springfox</groupId>
 <artifactId>springfox-boot-starter</artifactId>
 <version>3.0.0</version>
</dependency>
```

Dependency `springfox-swagger-ui` adds APIs documentation endpoint at root `url /swagger-ui.html`. So we have to make sure our other resource (entity) APIs are not present at root url. We can achieve this by adding following lines over each `ResourceController` class, like `StudentController` class.

```
@RestController
@RequestMapping("/api")
public class StudentController{

// your code

}
```

---

