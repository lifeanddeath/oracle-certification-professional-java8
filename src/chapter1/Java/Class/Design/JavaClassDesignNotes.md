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
