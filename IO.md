# Console

`import java.util.Scanner`

```java
System.out.println("type your name and press Enter");
Scanner scanner = new Scanner(System.in);
String name = scanner.nextLine();
System.out.println("Hello, " + name + "!");

scanner.next(); // returns text up until the first space
scanner.nextLine(); // returns all text that the user inputted until pressing enter
scanner.nextByte();
scanner.nextShort();
scanner.nextInt();
scanner.nextLong();
scanner.nextFloat();
scanner.nextDouble();
scanner.nextBigInteger();
scanner.nextBigDecimal();
```

Prefixing any of these methods with `has` returns true if the stream has any more of the request type

```java
Scanner scanner = new Scanner(System.in);
scanner.useLocale(Locale.US); //Set number format excepted
System.out.println("Input a float");
// the decimal separator is .

if (scanner.hasNextFloat()) { //Check if it is a float
	float fValue = scanner.nextFloat();
	//retrive the value directly as float
	System.out.println(fValue + " is a float");
} else {
	String sValue = scanner.next();
	// We can not retrive as float
	System.out.println(sValue + " is not a float");
}
```

# Files

## paths

```java
Path p1 = Paths.get("/home/");
Path p2 = Paths.get("arthur/files");
Path joined = p1.resolve(p2);
joined.normalize().toString() // "/home/arthur/files"
Path path = p1.resolve("ford/files");

path.getFileName();  // files
path.getNameCount(); // 3
path.getName(1);     // ford
path.getParent();    // /home/ford
path.getRoot();      // /
```

## file-system

```java
// checking existance
Files.exists(Path path);
Files.notExists(Path path);

Files.isDirectory(p1);
Files.isRegularFile(p1);

// copy, move, creation

// getting properties
Files.isReadable(Path path)
Files.isWritable(Path path)
Files.isExecutable(Path path)
Files.isHidden(Path path)
Files.isSymbolicLink(Path path)

// Getting MIME type
Files.probeContentType(Path path)
```

## reading files

```java
Path p2 = Paths.get(URI.create("file:///home/testuser/File.txt"));
byte[] content = Files.readAllBytes(p2);
List<String> linesOfContent = Files.readAllLines(p2);
```

## writing files

```java
Path p2 = Paths.get("/home/testuser/File.txt");
List<String> lines = Arrays.asList(
new String[]{"First line", "Second line", "Third line"});
Files.write(p2, lines);
Files.write(Path path, byte[] bytes)
```

Existing files wile be overridden, non-existing files will be created.

## Serialization

Serialization is the process of converting an object's state (including its references) to a sequence of bytes, as well as the process of rebuilding those bytes into a live object at some future time.

NOTE: non-access modifiers -> transient ( for attributes )

Every class ( and the classes of it's attributes ) has to implement the `Serializable` interface 

```java
import java.io.Serializable;
public class SerialClass implements Serializable {
	AnotherClass data;
	// implementation
}
public class AnotherClass implements Serializable {
	// implementation
}
```

### serialization (write)

```java
import java.io.FileOutputStream;
import java.io.ObjectOutputStream;
import java.io.IOException;

public class PersistSerialClass {
public static void main(String [] args) {
	String filename = "sc.bin";
	SerialClass sc = new SerialClass();
	//We will write this object to file system.
	try {
		ObjectOutputStream out = new ObjectOutputStream (
			new FileOutputStream(filename)
		);
		out.writeObject( sc );
		//Write byte stream to file system.
		out.close();
	} catch(IOException ex){
		ex.printStackTrace();
	}
}}
```

### de-serialization (read)

```java
import java.io.FileInputStream;
import java.io.ObjectInputStream;
import java.io.IOException;
import java.io.java.lang.ClassNotFoundException;

public class ReadSerialClass {
public static void main(String [] args) {
	String filename = "sc.bin";
	SerialClass sc = null;
	try {
		ObjectInputStream in = new ObjectInputStream(
			new FileInputStream(filename)
		);
		sc = (SerialClass)in.readObject();
		in.close();
	} catch(IOException ex){
		ex.printStackTrace();
	} catch(ClassNotFoundException cnfe){
		cnfe.printStackTrace();
	}
}}
```