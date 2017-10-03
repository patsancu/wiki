### Maven
#### Run java project from CLI
```
mvn exec:java -Dexec.mainClass="s3.pruebas.pruebas.App"
```
#### Maven error

try-with-resources is not supported in -source 1.6

### Cause
There's no java version listed on the pom for that step/order

### Solution, (from [here](https://stackoverflow.com/a/7034105/2769307) ):
```
<build>

    <pluginManagement>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>2.3.2</version>
          <configuration>
            <source>1.6</source>
            <target>1.6</target>
          </configuration>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
```
