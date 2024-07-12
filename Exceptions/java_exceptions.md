# Java Exceptions

## What are Exceptions?

Exceptions are events that occur during the execution of a program that disrupt the normal flow of instructions. In Java, exceptions are objects that represent these events.

### Exception Hierarchy

Java exceptions are part of a hierarchy of classes, with `Throwable` at the top. There are two main subclasses of `Throwable`:

- `Error`: Represents serious problems that a reasonable application should not try to catch.
- `Exception`: Represents conditions that a reasonable application might want to catch.

#### Types of Exceptions

- **Checked Exceptions**: These are exceptions that are checked at compile-time. Examples include `IOException`, `SQLException`.
- **Unchecked Exceptions**: These are exceptions that are not checked at compile-time. Examples include `ArithmeticException`, `NullPointerException`.

## Handling Exceptions

### Try-Catch Block

The `try-catch` block is used to handle exceptions. Code that might throw an exception is placed in the `try` block, and the exception handling code is placed in the `catch` block.

**Syntax:**

```java
try {
    // code that may throw an exception
} catch (ExceptionType e) {
    // code to handle the exception
}
```

**Example:**

```java
try {
    int[] numbers = {1, 2, 3};
    System.out.println(numbers[5]);
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Array index is out of bounds!");
}
```

### Finally Block

The `finally` block is used to execute important code such as closing resources, regardless of whether an exception is thrown or not.

**Example:**

```java
try {
    int[] numbers = {1, 2, 3};
    System.out.println(numbers[5]);
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Array index is out of bounds!");
} finally {
    System.out.println("This block is always executed.");
}
```

### Multiple Catch Blocks

You can have multiple catch blocks to handle different types of exceptions.

**Example:**

```java
try {
    int[] numbers = {1, 2, 3};
    System.out.println(numbers[5]);
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Array index is out of bounds!");
} catch (Exception e) {
    System.out.println("An error occurred.");
}
```

### The throw Keyword

The `throw` keyword is used to explicitly throw an exception.

**Syntax:**

```java
throw new ExceptionType("Error message");
```

**Example:**

```java
public class Main {
    public static void main(String[] args) {
        try {
            checkAge(15);
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }

    static void checkAge(int age) throws Exception {
        if (age < 18) {
            throw new Exception("Age must be at least 18");
        } else {
            System.out.println("Access granted");
        }
    }
}
```

### The throws Keyword

The `throws` keyword is used in the method signature to declare that a method can throw one or more exceptions.

**Syntax:**

```java
returnType methodName(parameters) throws ExceptionType1, ExceptionType2 {
    // method code
}
```

**Example:**

```java
public class Main {
    public static void main(String[] args) {
        try {
            checkAge(15);
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }

    static void checkAge(int age) throws Exception {
        if (age < 18) {
            throw new Exception("Age must be at least 18");
        } else {
            System.out.println("Access granted");
        }
    }
}
```

## User-Defined Exceptions

You can create your own exceptions by extending the `Exception` class.

**Example:**

```java
class AgeException extends Exception {
    public AgeException(String message) {
        super(message);
    }
}

public class Main {
    public static void main(String[] args) {
        try {
            checkAge(15);
        } catch (AgeException e) {
            System.out.println(e.getMessage());
        }
    }

    static void checkAge(int age) throws AgeException {
        if (age < 18) {
            throw new AgeException("Age must be at least 18");
        } else {
            System.out.println("Access granted");
        }
    }
}
```

## Exception Propagation

Exception propagation occurs when an exception is thrown from a method and not caught, causing it to propagate to the caller method. If the caller does not handle it, the exception will propagate to its caller, and so on.

**Example:**

```java
public class Main {
    public static void main(String[] args) {
        try {
            method1();
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }

    static void method1() throws Exception {
        method2();
    }

    static void method2() throws Exception {
        method3();
    }

    static void method3() throws Exception {
        throw new Exception("Exception occurred in method3");
    }
}
```

## Conclusion

Exception handling is a crucial aspect of Java programming, allowing you to manage runtime errors effectively. By understanding and utilizing the various exception handling mechanisms, you can write robust and error-resistant code.
