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
```java
public static String readFirstLineFromFile(String path) throws IOException {
    try (BufferedReader br =
                   new BufferedReader(new FileReader(path))) {
        return br.readLine();
    }
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