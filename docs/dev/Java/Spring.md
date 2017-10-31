### [Use events in Spring](http://www.baeldung.com/spring-events)
### [Events listener](https://spring.io/blog/2015/02/11/better-application-events-in-spring-framework-4-2)

### Run something when application is ready (everything is nicely loaded)
```java
@EventListener(ApplicationReadyEvent.class)
public void doSomethingAfterStartup() {
    System.out.println("hello world, I have just started up");
}
```
