## Basic CLI
### Compile and run

`javac p.java; java p`

### Create jar from class

`jar -cvfe TheJavaFile.jar <MainClass> TheJavaFile.class`

### Run jar

`java -jar TheJavaFile.jar`

### Run a class from Jar which is not the Main-Class in its Manifest file

`java -cp MyJar.jar com.mycomp.myproj.dir2.MainClass2 /home/myhome/datasource.properties /home/myhome/input.txt`

### Find out what is loading some specific class
```
java -verbose:class project-televisa-reports-db-extractor-spring-boot.jar | grep javax.servlet.ServletContext
```
More info [here](http://www.oracle.com/technetwork/java/javase/clopts-139448.html)

### JMX debug jconsole
execute 
```bash
$JAVA_HOME/bin/jconsole server:port
## Example:
$JAVA_HOME/bin/jconsole localhost:8048
```


### Freemarker

#### Ouptut integers without commas (separating the thousands)
Add **?c** to the number variable
```
report.total_households?c
```

### Eclipse
#### Remote debug
```
java -jar -Xdebug -Xrunjdwp:transport=dt_socket,server=y,address="8765" project.jar --server.port=7080 
```
* From Eclipse, Run -> Debug configurations... -> Remote Java Application
* In *Connection Type*: 
```
Standard (Socket Attach)
Connection Properties:
Host: localhost
Port: 8765
```

More info [here](http://www.ibm.com/developerworks/library/os-eclipse-javadebug/)


### Useful libraries
[com.google.common.base.Strings](https://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Strings.html)

`static String commonPrefix(CharSequence a, CharSequence b)`

`static String commonSuffix(CharSequence a, CharSequence b)`

`static String emptyToNull(String string)`

`static boolean isNullOrEmpty(String string)`

`static String nullToEmpty(String string)`

`static String padEnd(String string, int minLength, char padChar)`

`static String padStart(String string, int minLength, char padChar)`

`static String repeat(String string, int count)`
