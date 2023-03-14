[sintax](https://en.wikipedia.org/wiki/Java_syntax)

# datatypes

|Data Type|Size|Description|
|-|-|-|
|byte|1 byte|Stores whole numbers from -128 to 127|
|short|2 bytes|Stores whole numbers from -32,768 to 32,767|
|int|4 bytes|Stores whole numbers from -2,147,483,648 to 2,147,483,647|
|long|8 bytes|Stores whole numbers from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807|
|float|4 bytes|Stores fractional numbers. Sufficient for storing 6 to 7 decimal digits|
|double|8 bytes|Stores fractional numbers. Sufficient for storing 15 decimal digits|
|boolean|1 bit|Stores true or false values|
|char|2 bytes|Stores a single character/letter or ASCII values|

# standard datatypes

## string
[link](https://www.geeksforgeeks.org/strings-in-java/)
## collections
[link](https://www.geeksforgeeks.org/collections-in-java-2/)
- arraylist
- hashmap
- hashset
- tries
## big_integer
[link](https://www.geeksforgeeks.org/biginteger-class-in-java/)
## big_decimal
[link](https://www.geeksforgeeks.org/bigdecimal-class-java/)
## date
[link](https://www.geeksforgeeks.org/new-date-time-api-java8/)

# standard interfaces

## clonable

```java
class Foo implements Cloneable {
	int w;
	String x;
	float[] y;
	Date z;
	public Foo clone() {
		try {
			Foo result = new Foo();
			// copy primitives by value
			result.w = this.w;
			// copy immutable objects by reference
			result.x = this.x;
			// clone mutable objects recursively
			if (this.y != null) {
				result.y = this.y.clone();
			}
			if (this.z != null) {
				result.z = this.z.clone();
			}
			return result;
		} catch (CloneNotSupportedException e) {
			throw new AssertionError(e);
		}
	}
}
```

## comparable

necessario per funzionalità come l'ordinamento

```java
public class Person implements Comparable<Person> {
	String lastName;
	String firstName;
	public Person(String firstName, String lastName) {
	this.firstName = firstName != null ? firstName : "";
	this.lastName = lastName != null ? lastName : "";
	}
	@Override
	public boolean equals(Object o) {
		if (! (o instanceof Person)) return false;
		Person p = (Person)o;
		return firstName.equals(p.firstName) &&
		lastName.equals(p.lastName);
	}
	@Override
	public int hashCode() {
		return Objects.hash(firstName, lastName);
	}
	@Override
	public int compareTo(Person other) {
	int LNCompare = lastName.compareTo(other.lastName);
	if ( LNCompare != 0 ) {
		return lastNameCompare;
	} else {
		return firstName.compareTo(other.firstName);
	}
}
```

# Asserting

```java
TBD
```

# Generics

Generics are a facility of generic programming that extend Java's type system to allow a type or method to operate on objects of various types while providing compile-time type safety.

Code that uses generics has many benefits over non-generic code
- Stronger type checks at compile time
- Elimination of casts
- Enabling programmers to implement generic algorithms

Generics enable classes, interfaces, and methods to take other classes and interfaces as type parameters.

```java
public class Param<T> {
	private T value;
	public T getValue() {
		return value;
	}
	public void setValue(T value) {
		this.value = value;
	}
}
```

To instantiate this class, provide a type argument in place of T:
```java
Param<Integer> integerParam = new Param<Integer>();

// The type argument can be any reference type, including arrays and other generic types:

Param<String[]> stringArrayParam;
Param<int[][]> int2dArrayParam;
Param<Param<Object>> objectNestedParam;
```

**naming conventions:**
- T for "type"
- E for "element"
- K/V for "key"/"value"

```java
public abstract class AbstractParam<T> {
	public T value;
}
public class Email extends AbstractParam<String> {
	// ...
}
public class MultiParam<T, E> extends AbstractParam<E> {
	// ...
}
```

## wildcards

`? extends T` represents an upper bounded wildcard. The unknown type represents a type that must be a subtype of T, or type T itself.
`? super T` represents a lower bounded wildcard. The unknown type represents a type that must be a supertype of T, or type T itself.
As a rule of thumb, you should use
- `? extends T` if you only need "read" access ("input")
- `? super T` if you need "write" access ("output")
- `T` if you need both ("modify")

If it is not easy to understand, please remember **PECS** rule:
Producer uses "Extends" and Consumer uses "Super"

```java
interface Fruit {}
class Apple implements Fruit {}
class Banana implements Fruit {}
class GrannySmith extends Apple {}
public class FruitHelper {
public void eatAll(Collection<? extends Fruit> fruits) {}
public void addApple(Collection<? super Apple> apples) {}
}

public static void main(String[] args) {
	List<Fruit> fruits = new ArrayList<Fruit>();
	fruits.add(new Apple());
	fruits.add(new Banana());
	
	FruitHelper fruitHelper = new FruitHelper() ;
	fruitHelper.addApple(fruits);
	fruitHelper.eatAll(fruits);
	
}
```

## methods

```java
public class Example {
	public <T> List<T> makeList(T t1, T t2) {
		List<T> result = new ArrayList<T>();
		result.add(t1);
		result.add(t2);
		return result;
	}
	public void usage() {
		List<String> listString = makeList(
			"Jeff", "Atwood"
		);
		List<Integer> listInteger = makeList(1, 2);
	}
}
```

## instantiating

Due to type erasure the following will not work:
```java
public <T> void genericMethod() {
	T t = new T(); // Can not instantiate the type T
}
```
The type T is erased. Since, at runtime, the JVM does not know what T originally was, it does not know which constructor to call.

Workarounds

```java
// Passing T's class when calling genericMethod

public <T> void genericMethod(Class<T> cls) {
	try {
		T t = cls.newInstance();
	} catch (Exception e) {
		System.err.println(e);
	}
}
genericMethod(String.class);

// Passing a reference to T's constructor

public <T> void genericMethod(Supplier<T> cons) {
	T t = cons.get();
}
genericMethod(String::new);
```

# Unit testing

Unit testing is an integral part of test-driven development, and an important feature for building any robust application.
Unit testing is ensuring that a given module behaves as expected. In large-scale applications, ensuring the appropriate execution of modules in a vacuum is an integral part of ensuring application fidelity.

in intellij lo strumento di testing si trova in: navigate->test

i test saranno definiti come tante funzioni senza valore di ritorni e preceduti dall'annotazione `@Test`
ogni test possiederà i dati necessari all'esecuzione e terminerà chiamando la funzione `assertEquals` che prende in input il risultato aspettato ed il dato di ritorno della funzione in esame.

```java
import org.junit.jupiter.api.Test;  
import static org.junit.jupiter.api.Assertions.*;

class MainTest {
	@Test  
	void test1() {
	    assertEquals( 1 , metodo( 57, "hello" ));
	}
	@Test  
	void test2() {
	    assertEquals(1,0); // fail
	}
}
```

Note: test-driven development ([TDD](https://www.codingdojo.com/blog/test-driven-development))
