### Mapstruct abstract mapper injected in JUnit test
Mockito can inject it.
Just define the mapper as a Mockito spy, by getting the real mapper
```java
@Spy
private XMapper xMapper = Mappers.getMapper(XMapper.class);

@InjectMocks
private Service service;

```
