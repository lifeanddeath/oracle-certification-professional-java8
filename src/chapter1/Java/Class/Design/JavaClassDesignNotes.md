#Chapter 1: Java Class Design

##Encapsulation

The term encapsulation refers to combining data and associated functions as a single
unit. In other words, the class encapsulates its fields and methods together.

##Access Modifiers

Access modifiers determine the level of visibility for a Java entity (a class, method, or field). Access
modifiers enable you to enforce effective encapsulation.

Java supports four types of access modifiers:


* Public

* Private

* Protected

* Default (no access modifier specified)

##Protected and Default Access Modifiers

Protected and default access modifiers are quite similar to each other. If a member method or field is
declared as protected or default, then the method or field can be accessed within the package. Note that
there is no explicit keyword to provide default access; in fact, when no access modifier is specified, the
member has default access. Also, note that default access is also known as package-protected access.
Protected and default accesses are comparable to the situation in an office where a conference room is
accessible only to one department.


What is the difference between protected and default access? One significant difference between these
two access modifiers arises when we talk about a subclass belonging to another package than its superclass.
In this case, protected members are accessible in the subclass, whereas default members are not.

##Inheritance

Inheritance is a reusability mechanism in object-oriented programming. With inheritance, the common
properties of various objects are exploited to form relationships with each other. The abstract and common
properties are provided in the superclass, which is available to the more specialized subclasses. For example,
a color printer and a black-and-white printer are kinds of a printer (single inheritance); an all-in-one printer
is a printer, scanner, and photocopier (multiple inheritance).

Consider a simple example used in earlier sections: class Shape is a base class and Circle is a
derived class. In other words, a Circle is a Shape; similarly, a Square is a Shape. Therefore, an inheritance
relationship can be referred to as an IS-A relationship. A super class hence stays on the right hand side of the "is-a" equation.

Example: In java NUMBER class contitues a base for several classes in java.lang package for Byte, Integer, Float, Double classes.

##Polymorphism

Polymorphism can be of two forms: dynamic and static.
* When different forms of a single entity are resolved during runtime (late binding),
such polymorphism is called dynamic polymorphism. In the previous section
on inheritance, we discussed overriding. Overriding is an example of runtime
polymorphism.

* When different forms of a single entity are resolved at compile time (early binding),
such polymorphism is called static polymorphism. Function overloading is an
example of static polymorphism, and let us explore it now.

###Runtime Polymorphism

```
class Shape {
	public double area() {
		return 0;
	} // default implementation
// other members
}

class Circle extends Shape {
	private int radius;

	public Circle(int r) {
		radius = r;
	}

// other constructors
	public double area() {
		return Math.PI * radius * radius;
	}
// other declarations
}

class Square extends Shape {
	private int side;

	public Square(int a) {
		side = a;
	}

	public double area() {
		return side * side;
	}
// other declarations
}

public class TestShape {
	public static void main(String[] args) {
		Shape shape1 = new Circle(10);
		System.out.println(shape1.area());
		Shape shape2 = new Square(10);
		System.out.println(shape2.area());
	}
}

```

This program prints

314.1592653589793

100.0

## Method Overloading

In Java, you can define multiple
methods with the same name, provided the argument lists differ from each other.

```
class Circle {
	// other members
	public void fillColor(int red, int green, int blue) {
		/* color the circle using RGB color values – actual code elided */
	}

	public void fillColor(float hue, float saturation, float brightness) {
		/* color the circle using HSB values – actual code elided */
	}
}
```

## Constructor Overloading

A default constructor is useful for creating objects with a default initialization value. When you want to
initialize the objects with different values in different instantiations, you can pass them as the arguments to
constructors. And yes, you can have multiple constructors in a class, which is constructor overloading. In a
class, the default constructor can initialize the object with default initial values, while another constructor
can accept arguments that need to be used for object instantiation.

```
public class Circle {
	private int xPos;
	private int yPos;
	private int radius;

// three overloaded constructors for Circle
	public Circle(int x, int y, int r) {
		xPos = x;
		yPos = y;
		radius = r;
	}

	public Circle(int x, int y) {
		xPos = x;
		yPos = y;
		radius = 10; // default radius
	}

	public Circle() {
		xPos = 20; // assume some default values for xPos and yPos
		yPos = 20;
		radius = 10; // default radius
	}

	public String toString() {
		return "center = (" + xPos + "," + yPos + ") and radius = " + radius;
	}

	public static void main(String[] s) {
		System.out.println(new Circle());
		System.out.println(new Circle(50, 100));
		System.out.println(new Circle(25, 50, 5));
	}
}
```

This program prints

center = (20,20) and radius = 10

center = (50,100) and radius = 10

center = (25,50) and radius = 5

## Overload Resolution

```
class Overloaded {
	public static void aMethod(int val) {
		System.out.println("int");
	}

	public static void aMethod(short val) {
		System.out.println("short");
	}

	public static void aMethod(Object val) {
		System.out.println("object");
	}

	public static void aMethod(String val) {
		System.out.println("String");
	}

	public static void main(String[] args) {
		byte b = 9;
		aMethod(b); // first call
		aMethod(9); // second call
		Integer i = 9;
		aMethod(i); // third call
		aMethod("9"); // fourth call
	}
}
```

It prints

short

int

object

String

Here is how the compiler resolved these calls:

1. In the first method call, the statement is aMethod(b) where the variable b is of
type byte. There is no aMethod definition that takes byte as an argument. The
closest type (in size) is short type and not int, so the compiler resolves the call
aMethod(b) to aMethod(short val) definition.
2. In the second method call, the statement is aMethod(9). The constant value 9 is
of type int. The closest match is aMethod(int), so the compiler resolves the call
aMethod(9) to aMethod(int val) definition.
3. The third method call is aMethod(i), where the variable i is of type Integer.
There is no aMethod definition that takes Integer as an argument. The closest
match is aMethod(Object val), so it is called. Why not aMethod(int val)? For
finding the closest match, the compiler allows implicit upcasts, not downcasts, so
aMethod(int val) is not considered.
4. The last method call is aMethod("9"). The argument is a String type. Since there
is an exact match, aMethod(String val) is called.

```
class OverloadingError {
	public static void aMethod(byte val) {
		System.out.println("byte");
	}

	public static void aMethod(short val) {
		System.out.println("short");
	}

	public static void main(String[] args) {
		aMethod(9);
	}
}
```

This would give compiler error, as compiler would do upcasting but the downcasting is not possible!

```
class AmbiguousOverload {
	public static void aMethod(long val1, int val2) {
		System.out.println("long, int");
	}

	public static void aMethod(int val1, long val2) {
		System.out.println("int, long");
	}

	public static void main(String[] args) {
		aMethod(9, 10);
	}
}
```

Above shown code would also fail and not compile, as int value would be upcasted for long as well, so it is sort of like compiler confusion for the types of int and long!

###Points to remember 
* Overload resolution takes place entirely at compile time
* You cannot overload methods with the methods differing in return types alone
* You cannot overload methods with the methods differing in exception specifications
* For overload resolution to succeed, you need to define methods such that the
compiler finds one exact match. If the compiler finds no matches for your call or
if the matching is ambiguous, the overload resolution fails and the compiler issues
an error.
