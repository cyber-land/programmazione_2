## overloading

Method overloading ( also known as static polymorphism ) is a way you can have two ( or more ) methods with same name in a single class

```java
public class Name {
	int num = 5;
	
	// based on the number of parameters passed
	public void sum () { num + 5; }
	public void sum ( int n ) { num + n; }
	
	// based on the order of parameters
	public int method ( int i , float f ) { }
	public int method ( float f , int i ) { }
}
```

Methods cannot be overloaded by changing just the return type

## overriding

method overriding ( also known as dynamic polymorphism ) is a substitution of the method body provided by the parent class

```java
public class Shape {
	public Double area () { return 0.0; }
}

public class Circle extends Shape {
	private Double radius = 5.0;
	@Override
	public Double area () {
		return 3.14 * radius * radius;
	}
}

public class Rectangle extends Shape {
	private Double length  = 5.0;
	private Double breadth = 10.0;
	@Override
	public Double area () { return length * breadth; }
}

public static void main(String[] args) {
	Shape circle = new Circle();
	Shape rectangle = new Rectangle();
	System.out.println( circle.area() );    // 78.5
	System.out.println( rectangle.area() ); // 50.0
}
```

# binding

Il tipo statico determina quali metodi possono essere invocati
il tipo dinamico determina quale (ri)definizione eseguire

Si assuma 
C o = ...;
o.m(...);
 
il metodo scelto dipende dal tipo dinamico di `o`, e viene deciso (a runtime) con questa logica:
1. Si cerca all’interno della classe `C` (tipo statico di `o`) il
metodo `m` con la firma più simile all’invocazione
Le firme da considerare sono quelle fissate a compile time,
guardando cioè il tipo statico dei parametri attuali
2. Si guarda al tipo dinamico `D` di `o`; se è un sottotipo di
`C`, si deve verificare se ridefinisce (override) `m`. Se sì,
si usa l’implementazione di `D`, altrimenti quella di `C`

```java
public class Person {
    public void fun( Person p ) {
        System.out.println( "2 persone" );
    }
    public void fun ( Student s ) {
        System.out.println( "1 persona 1 studente" );
    }
}

public class Student extends Person {
    public void fun( Person p ) {
        System.out.println( "1 studente 1 persona" );
    }
    public void fun ( Student s ) {
        System.out.println( "2 studenti " );
    }
}
public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        Student s = new Student();
        Person ps = new Student();
        p.fun(p);
        p.fun(s);
        p.fun((Person) s); // casting
        s.fun(p);
        s.fun(s);
        ps.fun(p);
        ps.fun(s);
        p.fun(ps);
        s.fun(ps);
        // se oggetto valuta il tipo dinamico
        // se parametro valuta il tipo statico
    }
}
```
