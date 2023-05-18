La estensioni possono essere:
strutturali
(aggiunta di variabili di istanza)
e/o
comportamentali
(aggiunta di nuovi metodi e/o modifica di metodi esistenti)

# extends
With the use of the extends keyword among classes, all the properties of the superclass (also known as the Parent
Class ) are present in the subclass

```java
public class BaseClass {
	protected int n; // fields are also inherited
	public void baseMethod(){
		System.out.println("Doing base class stuff");
	}
}
public class SubClass extends BaseClass { }
```

Instances of SubClass have inherited the method `baseMethod()`

```java
SubClass s = new SubClass();
s.baseMethod(); 
```

Additional content can be added to a subclass. Doing so allows for additional functionality in the subclass without any change to the base class or any other subclasses from that same base class

```java
public class Subclass2 extends BaseClass {
	public void anotherMethod() {
		System.out.println("Doing subclass2 stuff");
	}
}
```

```java
Subclass2 s2 = new Subclass2();
s2.baseMethod();
s2.anotherMethod();
```

In Java, each class may extend at most one other class.
Java does not permit multiple inheritance with classes.

# abstract classes & interfaces

An abstract class is a class marked with the abstract keyword.
It, contrary to non-abstract class, may contain abstract (implementation-less) methods.
```java
public abstract class Component {
	private int x, y;
	public setPosition(int x, int y) {
		this.x = x;
		this.y = y;
	}
	public abstract void render();
}
```

All variables declared in an interface are public static final
All methods declared in an interface methods are public abstract
Interfaces cannot be declared as final

An abstract class cannot be instantiated. It can be sub-classed (extended) as long as the sub-class is either also abstract, or implements all methods marked as abstract by super classes

```java
public class Button extends Component {
	@Override
	public void render() {
		//render a button
	}
}
```

**anonymous subclasses of abstract classes**
```java
Component myAnonymousComponent = new Component() {
	@Override
	public void render() {
		// render a quick 1-time use component
	}
}
```
There are two key differences between abstract classes and interfaces:
- A class may only extend a single class, but may implement many interfaces.
- An abstract class can contain instance (non-static) fields, but interfaces may only contain static fields.

Abstract classes create "is a" relations while interfaces provide "has a" capability

```java
abstract class Animal {
	String name;
	int age;
}
class Dog extends Animal implements Learn { ... }
class Cat extends Animal implements Climb { ... }
interface Climb { void climb(); }
interface Think { void think(); }
interface Learn { void learn(); }
interface Apply { void apply(); }
class Man implements Think, Learn, Apply, Climb { ... }
```

Consider using abstract classes if...
1. You want to share code among several closely related classes.
2. You expect that classes that extend your abstract class have many common methods or fields, or require access modifiers other than public (such as protected and private).
3. You want to declare non-static or non-final fields.

Consider using interfaces if...
1. You expect that unrelated classes would implement your interface. For example, many unrelated objects can implement the Serializable interface.
2. You want to specify the behaviour of a particular data type but are not concerned about who implements its behaviour.
3. You want to take advantage of multiple inheritance of type.

# keyword `super`

TBD
