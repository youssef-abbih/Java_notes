# Object-Oriented Programming (OOP) in Java

## Introduction

Object-Oriented Programming (OOP) is a programming paradigm based on the concept of "objects", which can contain data and methods to manipulate that data. Java is a popular object-oriented programming language that supports various OOP concepts.

## Key OOP Concepts in Java

### Class

A class is a blueprint for creating objects. It defines a datatype by bundling data and methods that work on the data into one single unit.

**Example:**

```java
public class Animal {
    String name;
    int age;

    void eat() {
        System.out.println(name + " is eating.");
    }
}
```

### Object

An object is an instance of a class. When a class is defined, no memory is allocated until an object of that class is created.

**Example:**

```java
public class Main {
    public static void main(String[] args) {
        Animal dog = new Animal();
        dog.name = "Buddy";
        dog.age = 5;
        dog.eat();
    }
}
```

### Inheritance

Inheritance is a mechanism where one class acquires the properties (fields) and behaviors (methods) of another class. The class that inherits is called the subclass (or derived class), and the class from which it inherits is called the superclass (or base class).

**Example:**

```java
public class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

public class Dog extends Animal {
    void bark() {
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();  // Inherited method
        dog.bark();
    }
}
```

### Polymorphism

Polymorphism allows methods to do different things based on the object it is acting upon, even though they share the same name. It can be achieved through method overloading and method overriding.

**Method Overloading Example:**

```java
public class MathUtils {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}
```

**Method Overriding Example:**

```java
public class Animal {
    void sound() {
        System.out.println("This animal makes a sound.");
    }
}

public class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        myDog.sound();  // Calls the overridden method in Dog class
    }
}
```

### Encapsulation

Encapsulation is the technique of wrapping the data (variables) and the code acting on the data (methods) together as a single unit. It restricts direct access to some of the object's components, which can be accessed through methods.

**Example:**

```java
public class Person {
    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

### Abstraction

Abstraction is the concept of hiding the complex implementation details and showing only the essential features of the object. It can be achieved using abstract classes and interfaces.

**Abstract Class Example:**

```java
abstract class Animal {
    abstract void makeSound();

    void eat() {
        System.out.println("This animal eats food.");
    }
}

class Dog extends Animal {
    void makeSound() {
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.makeSound();
        dog.eat();
    }
}
```

### Interface

An interface in Java is a reference type, similar to a class, that can contain only constants, method signatures, default methods, static methods, and nested types. Interfaces cannot contain instance fields. The methods in interfaces are abstract by default.

**Example:**

```java
interface Animal {
    void eat();
    void makeSound();
}

class Dog implements Animal {
    public void eat() {
        System.out.println("The dog eats food.");
    }

    public void makeSound() {
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();
        dog.makeSound();
    }
}
```

### Static Attributes and Methods

Static attributes and methods belong to the class rather than any object instance. They can be accessed without creating an instance of the class.

**Example:**

```java
public class MathUtils {
    public static final double PI = 3.14159;

    public static int add(int a, int b) {
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println("PI: " + MathUtils.PI);
        int sum = MathUtils.add(5, 3);
        System.out.println("Sum: " + sum);
    }
}
```

### Final Attributes and Methods

Final attributes cannot be changed once they are initialized. Final methods cannot be overridden by subclasses. Final classes cannot be subclassed.

**Example of Final Attribute:**

```java
public class Person {
    public final String ssn;

    public Person(String ssn) {
        this.ssn = ssn;
    }
}
```

**Example of Final Method:**

```java
public class Animal {
    public final void eat() {
        System.out.println("This animal eats food.");
    }
}

public class Dog extends Animal {
    // This will cause a compilation error
    // public void eat() {
    //     System.out.println("The dog eats food.");
    // }
}
```

**Example of Final Class:**

```java
public final class Utility {
    public static void printMessage(String message) {
        System.out.println(message);
    }
}

// This will cause a compilation error
// public class ExtendedUtility extends Utility {
// }
```

## Conclusion

Object-Oriented Programming in Java allows for the creation of modular, reusable, and maintainable code. By understanding and utilizing classes, objects, inheritance, polymorphism, encapsulation, abstraction, interfaces, static attributes/methods, and final attributes/methods, developers can build robust Java applications.
