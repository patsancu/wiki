### Sleep
```java
//Pause for 4 seconds
Thread.sleep(4000);
```

### Write file
```java
public void writeFile() {
	try(FileOutputStream fos = newFileOutputStream("movies.txt");
		DataOutputStream dos = newDataOutputStream(fos)) {

		dos.writeUTF("Java 7 Block Buster");

	} catch(IOException e) {

		// log the exception

	}
}

```
### Read file
#### Java 7
##### Read all contents at once
```java
String content = new String(Files.readAllBytes(Paths.get(fileName)));
```
##### Line by line
```
package com.mkyong;

import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.io.IOException;

public class ReadTextFile {

    public static void main(String[] args) throws IOException {

        try {

            File f = new File("src/com/mkyong/data.txt");

            BufferedReader b = new BufferedReader(new FileReader(f));

            String readLine = "";

            System.out.println("Reading file using Buffered Reader");

            while ((readLine = b.readLine()) != null) {
                System.out.println(readLine);
            }

        } catch (IOException e) {
            e.printStackTrace();
        }

    }

}
```

#### Java 8
```java
Stream<String> lines = Files.lines(path);
lines.forEach(line -> data.append(line).append("\n"));
lines.close();
```

```java
@Test
public void givenFilePath_whenUsingFilesLines_thenFileData() {
   String expectedData = "Hello World from fileTest.txt!!!";

   Path path = Paths.get(getClass().getClassLoader()
           .getResource("fileTest.txt").toURI());

   StringBuilder data = new StringBuilder();
   Stream<String> lines = Files.lines(path);
   lines.forEach(line -> data.append(line).append("\n"));
   lines.close();

   Assert.assertEquals(expectedData, data.toString().trim());
}
```

### Read file extension
http://commons.apache.org/proper/commons-io/javadocs/api-2.5/org/apache/commons/io/FilenameUtils.html#getExtension

```java
String ext1 = FilenameUtils.getExtension("/path/to/file/foo.txt"); // returns "txt"
String ext2 = FilenameUtils.getExtension("bar.exe"); // returns "exe"
```
```
// https://mvnrepository.com/artifact/commons-io/commons-io
compile group: 'commons-io', name: 'commons-io', version: '2.4'
```


### Get file last updated date

```java
import java.io.File;
import java.text.SimpleDateFormat;

public class GetFileLastModifiedExample
{
    public static void main(String[] args)
    {
	File file = new File("c:\\logfile.log");

	System.out.println("Before Format : " + file.lastModified());

	SimpleDateFormat sdf = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");

	System.out.println("After Format : " + sdf.format(file.lastModified()));
    }
}
```

### Empty stack trace
From [here](https://www.atlassian.com/blog/archives/if_you_use_exceptions_for_path_control_dont_fill_in_the_stac). Useful for custom exceptions, or when a quicker *error handling* is required.
```
/**
* efficient exception that has no stacktrace; we use this for flow-control.
*/
@Immutable
static final class ResourceNotFound extends Exception
{
ResourceNotFound()
{}
@Override
public Throwable fillInStackTrace()
{
return this;
}
}
```

### Create temp file/folder

```java
import java.nio.file.Files;

tempCheckpointFolder = Files.createTempDirectory("checkpoints");
//the directory must be empty in order to be deleted.
tempCheckpointFolder.toFile().deleteOnExit();
```

### Compute time difference
```java
LocalDateTime now = LocalDateTime.now();
boolean olderThanAday = ChronoUnit.DAYS.between(startSessionDate, now ) >= 1;
if (olderThanAday){
    System.out.println("The stored timestamp is older than a day")
    startSessionDate = now;
}
```

### Random alphanumeric string
```<!-- https://mvnrepository.com/artifact/org.apache.commons/commons-lang3 -->
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-lang3</artifactId>
    <version>3.8</version>
</dependency>
```

```
RandomStringUtils.randomAlphanumeric(10);
```


### Difference between two dates
```
LocalDateTime now = LocalDateTime.now();
boolean olderThanAday = ChronoUnit.DAYS.between(startSessionDate, now ) >= 1;
if (startSessionDate == null || olderThanAday){
    AuthLoginResponseType response = this.serviceV12.startSession(this.username, this.password, this.locale);
    this.sessionId = response.getResult().getValue().getSessionId();
    startSessionDate = now;
}```
