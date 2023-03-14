# The Liskov Substitution Principle

Una variabile di tipo riferimento T può riferirsi ad un qualsiasi oggetto il cui tipo sia T o un suo sottotipo

Analogamente, un parametro formale di tipo riferimento T può riferirsi a parametri attuali il cui tipo sia T o un suo sottotipo

```java
class A {...}
class B extends A {...}
public void method(A obj) {...}
A a = new B(); // Assignment OK
method(new B()); // Passing as parameter OK
```

This also applies when the type is an interface, where there doesn't need to any hierarchical relationship between
the objects:

```java
interface Foo {
	void bar();
}
class A implements Foo {
	void bar() {...}
}
class B implements Foo {
	void bar() {...}
}
List<Foo> foos = new ArrayList<>();
foos.add(new A()); // OK
foos.add(new B()); // OK
```

# encapsulation

Encapsulation allows developers to present a consistent and usable interface which is independent of how a system is implemented internally.
Hiding the state ( **information hiding** ) of an object and providing
all interaction through an objects methods allows the class to make assumptions about its internal state.
