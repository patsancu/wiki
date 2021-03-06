### Maven

Test speficic method from specific classes, ignoring failure if there are no tests
```
mvn test -Dtest=ZoneDaoTest#findZoneByCityIdExistingCityId -DfailIfNoTests=false
```

### Find dependency version updates

#### Display version updates
```
mvn -DskipTests -Dmaven.test.skip=true -Pgrpc -Panalysis -Pdisplay-updates versions:display-dependency-updates
```

### Update dependencies in place
```
mvn -DskipTests -Dmaven.test.skip=true -Pgrpc -Panalysis -Pdisplay-updates versions:update-properties
```


### Find duplicated dependencies
```
mvn dependency:analyze-duplicate
```

### Create executable jar
* In pom.xml
```
<build>
    <pluginManagement>
      [...]
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <configuration>
                    <archive>
                        <manifest>
                            <mainClass>s3.trying.TimeZoneStuff</mainClass>
                        </manifest>
                    </archive>
                </configuration>
            </plugin>
            <plugin>
                <artifactId>maven-assembly-plugin</artifactId>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>single</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <archive>
                        <manifest>
                            <addClasspath>true</addClasspath>
                            <mainClass>s3.trying.TimeZoneStuff</mainClass>
                        </manifest>
                        </archive>
                        <descriptorRefs>
                            <descriptorRef>jar-with-dependencies</descriptorRef>
                    </descriptorRefs>
                </configuration>
            </plugin>
      [...]
        </plugins>
    </pluginManagement>
</build>
```
```
mvn clean compile assembly:single -Dmaven.test.skip=true
```
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


### Get project version
```
MVN_VERSION=$(mvn -q \
    -Dexec.executable=echo \
    -Dexec.args='${project.version}' \
    --non-recursive \
    exec:exec)
```
