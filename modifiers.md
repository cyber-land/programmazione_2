# access modifiers

## classes

**public**: the class is accessible by any other class
**default**: the class is only accessible by classes in the same package

## attributes, methods and constructors

**public**: the code is accessible for all classes
**private**: the code is only accessible within the declared class
**default**: the code is only accessible in the same package
**protected**: the code is accessible in the same package and subclasses

|Access Modifier|Visibility|Inheritance|
|-|-|-|
|Private|Class only|Can't be inherited|
|Package|In package|Available if subclass in package|
|Protected|In package|Available in subclass|
|Public|Everywhere|Available in subclass|

**Private Visibility**
allows a variable to only be accessed by its class
they are often used in conjunction with public getters and setters

```java
class Name {
	private int variable;
	public int getVariable ( ) {
		return variable;
	}
	public void setVariable ( int variable ) {
		this.variable = variable;
	}
	
	public static void main ( String[] args ) {
		Name n = new Name();
		n.setVariable( 5 );
		int var = n.getVariable();
	}
}
```

I metodi private non possono essere ridefiniti (come i final) ma sono completamente «invisibili» alle sottoclassi

**Public visibility**
Visible to the class, package, and subclass.

```java
public class Name {
	public int number;

	public static void main ( String[] args ) {
		Name n = new Name();
		n.number = 5;
		System.out.println( n.number );
	}
}
```

**Package Visibility**
With no modifier, the default is package visibility that indicates
whether classes in the same package as the class (regardless of their parentage) have access to the member.

example from javax.swing

```java
package javax.swing;
public abstract class JComponent extends Container ... {
	...
	static boolean DEBUG_GRAPHICS_LOADED;
	...
}
```

DebugGraphics is in the same package, so DEBUG_GRAPHICS_LOADED is accessible.

```java
package javax.swing;
public class DebugGraphics extends Graphics {
	...
	static {
		JComponent.DEBUG_GRAPHICS_LOADED = true;
	}
	...
}
```

**Protected visibility**
means that this member is visible to its package, along with any of its subclasses.

```java
package com.main;
public class MyClass {
	protected int variable;
	public MyClass () { variable = 2; }
}
```

```java
package some.other.pack;
import com.main.MyClass;
public class SubClass extends MyClass {
	public SubClass(){
		super();
		System.out.println( super.variable );
	}
}
```

You would be also able to access a protected member without extending it if you are accessing it from the same package.

# non-access modifiers

## classes

**final**: the class cannot be inherited by other classes
**abstract**: the class cannot be used to create objects ( To access an abstract class, it must be inherited from another class )

examples:
final -> immutability
```java
final class MyClass {
	/* some code */
}
// Compilation error: cannot inherit from final MyClass
class MySubClass extends MyFinalClass {
	/* more code */
}
```

## attributes and methods

**final**: Attributes and methods cannot be modified/overridden
**static**: Attributes and methods belongs to the class, rather than an object
**abstract**: Can only be used in an abstract class, and can only be used on methods. The method does not have a body
The body is provided by the subclass (inherited from)
**transient**: Attributes and methods are skipped when serializing the object containing them
**synchronized**: Methods can only be accessed by one thread at a time
**volatile**: The value of an attribute is not cached thread-locally, and is always read from the "main memory"

### final
le variabili definite `final` possono venire modificate solo dal costruttore quando vengono definite

```java
public class Name {
	final int num;
	public Name (int num ) {
		this.num = num;
	}
	public int get() { return num; }
}
```

### static
Static variables and methods are not part of an instance, There will always be a single copy of that variable no matter how many objects you create of a particular class.

```java
public class Name {
	public static int var;

	// static initializer
	static { var = 10; }
	
	public Name () { var = 5; };
	
	// All the fields and methods of a class used inside 
	// a static method must be static or local
	public static int getSub ( int num ) {
		return var - num;
	}

	public static void main(String[] args) {
		int res = Name.getSub ( 2 );    // 8
		Name n = new Name();
		System.out.println( n.var );    // 5
		Name.var = 6;
		System.out.println( n.var );    // 6
		n.var = 4;
		System.out.println( Name.var ); // 4
	}
}
```

il binding dei metodi `static` è sempre statico ( non dinamico )

### abstract
TBD
