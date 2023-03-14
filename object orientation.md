# packages

package in java is used to group class and interfaces. This helps developer to avoid conflict when there are huge numbers of classes. If we use this package the classes we can create a class/interface with same name in different packages.
By using packages we can import the piece of again in another class.

Packages can be used to create classes with the same name

# classes

Objects have states and behaviors.
può essere vista come il collegamento tra una `struct` ed alcune funzioni che operano su di essa

# constructors

Constructors are used to initialize objects.

se non viene definito alcun costruttore, il compilatore genera automaticamente un costruttore senza parametri che inizializza tutte le variabile al loro valore di default, eccetto quelle nello heap che non vengono inizializzate, puntando a `null`

I costruttori non vengono ereditati

example ( that doesn't compile )
```java
public class Name {
	// must be names the same as the class name
	// do not have a return type
	public Name () {
		this ( 5 );
		// refers to another constructor in the current
		// class with different signatures
	}
	// they can take input parameters
	public Name ( int n ) { }

	// Constructors also can be called through 
	// inheritance using the keyword super
	public Name () {
		super(); // must be the first instruction
	}
}
```

## singleton
A singleton is a class that only ever has one single instance

```java
public class Singleton {
	private static final 
		Singleton INSTANCE = new Singleton();
	private Singleton() {}
	public static Singleton getInstance() {
		return INSTANCE;
	}
}

```

# object

every class depends directly or transitively on the `Object` class and therefore inherit some methods

## `hashCode()`
is used in hash implementations such as `HashMap`, `HashTable`, and `HashSet`
If two objects are equal according to the equals(Object) method, then calling the `hashCode` method on each of the two objects must produce the same integer result

## `toString()`
is used to create a String representation of an object by using the object ́s content
this method should be overridden when writing your class
is called implicitly when an object is concatenated to a string

```java
public class User {
	private String firstName;
	private String lastName;
	public User(String firstName, String lastName) {
		this.firstName = firstName;
		this.lastName = lastName;
	}
	@Override
	public String toString() {
		return firstName + " " + lastName;
	}
	public static void main(String[] args) {
		User user = new User("John", "Doe");
		System.out.println(user.toString());
		// Prints "John Doe"
	}
}
```

## `equals()`
tests for value equality (whether they are logically "equal")
To compare the contents of an object for equality, equals() has to be overridden

```java
public class Foo {
	int field1, field2;
	public Foo( int i, int j ) {
		field1 = i;
		field2 = j;
	}
	@Override
	public boolean equals(Object obj) {
		if (this == obj) return true;
		if (obj == null || getClass() != obj.getClass()) {
			return false;
		}
		Foo f = (Foo) obj;
		return  field1 == f.field1 && field2 == f.field2;
	}
	@Override
	public int hashCode() {
		int hash = 1;
		hash = 31 * hash + this.field1;
		hash = 31 * hash + this.field2;
		return hash;
	}
	public static void main(String[] args) {
		Foo foo1 = new Foo(0, 0, "bar");
		Foo foo2 = new Foo(0, 0, "bar");
		System.out.println(foo1.equals(foo2));
		// prints true
	}
}
```

`==` test for physic equality
Even though `foo1` and `foo2` are created with the same fields, they are pointing to two different objects in memory
if `equals()` is not overridden it will have the same behavior as `==`

```java
public static void main(String[] args) {
	Foo foo1 = new Foo(0, 0);
	Foo foo2 = new Foo(0, 0);
	System.out.println( foo1 == foo2 );
	// prints false
	System.out.println(foo1.equals(foo2));
	// prints false
}
```

# enum

Java enums are shorthand syntax for sizable quantities of constants of a single class.

```java
// Enums implicitly implement Serializable and Comparable
public enum Direction {
	NORTH, SOUTH, EAST, WEST;
	// An enum can contain a method, just like any class
	public Direction getOpposite () {
		switch ( this ) {
			case NORTH:
				return SOUTH;
			case SOUTH:
				return NORTH;
			case WEST:
				return EAST;
			case EAST:
				return WEST;
			default: //This will never happen
				return null;
		}
	}
}
// You can also compare enum constants using `==`
Season.FALL == Season.WINTER   // false
Season.SPRING == Season.SPRING // true
```

```java
public enum Coin {
	PENNY(1), NICKEL(5), DIME(10), QUARTER(25);
	private int value;
	
	// An enum cannot have a public constructor
	Coin ( int value ) { this.value = value; }
	
	public int getValue() { return value; }
	public boolean isGreaterThan ( Coin other ) {
		return this.value > other.value;
	}
}
int p = Coin.NICKEL.getValue(); // 5
```

An enum is compiled with a built-in static `valueOf()` method which can be used to lookup a constant by its name

```java
String dayName = DayOfWeek.SUNDAY.name();
assert dayName.equals("SUNDAY");

DayOfWeek day = DayOfWeek.valueOf(dayName);
assert day == DayOfWeek.SUNDAY;

// This is also possible using a dynamic enum type:
Class<DayOfWeek> enumType = DayOfWeek.class;
DayOfWeek day = Enum.valueOf(enumType, "SUNDAY");
assert day == DayOfWeek.SUNDAY;
```
