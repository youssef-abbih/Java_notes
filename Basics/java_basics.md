# Java Basics

## Variables

Variables are containers for storing data values. In Java, each variable must be declared with a data type before it can be used.

### Data Types

- **Primitive Data Types**: `byte`, `short`, `int`, `long`, `float`, `double`, `char`, `boolean`.
- **Non-Primitive Data Types**: `String`, `Arrays`, `Classes`, `Interfaces`.

### Variable Declaration

**Example:**

```java
int age = 25;
double price = 19.99;
char grade = 'A';
boolean isJavaFun = true;
String greeting = "Hello, World!";
```

## Methods

Methods are blocks of code that perform a specific task. Methods are defined within a class and can be called to execute their code.

### Method Declaration

**Syntax:**

```java
returnType methodName(parameters) {
    // code
}
```

**Example:**

```java
public class MyClass {
    public static void main(String[] args) {
        sayHello();
        int sum = add(5, 3);
        System.out.println("Sum: " + sum);
    }

    public static void sayHello() {
        System.out.println("Hello!");
    }

    public static int add(int a, int b) {
        return a + b;
    }
}
```

## Conditional Statements

Conditional statements allow you to perform different actions based on different conditions.

### if Statement

**Syntax:**

```java
if (condition) {
    // code to be executed if condition is true
}
```

**Example:**

```java
int age = 18;
if (age >= 18) {
    System.out.println("You are an adult.");
}
```

### if-else Statement

**Syntax:**

```java
if (condition) {
    // code to be executed if condition is true
} else {
    // code to be executed if condition is false
}
```

**Example:**

```java
int age = 16;
if (age >= 18) {
    System.out.println("You are an adult.");
} else {
    System.out.println("You are a minor.");
}
```

### else-if Statement

**Syntax:**

```java
if (condition1) {
    // code to be executed if condition1 is true
} else if (condition2) {
    // code to be executed if condition2 is true
} else {
    // code to be executed if all conditions are false
}
```

**Example:**

```java
int score = 85;
if (score >= 90) {
    System.out.println("Grade: A");
} else if (score >= 80) {
    System.out.println("Grade: B");
} else if (score >= 70) {
    System.out.println("Grade: C");
} else {
    System.out.println("Grade: D");
}
```

### switch Statement

**Syntax:**

```java
switch (expression) {
    case value1:
        // code to be executed if expression == value1
        break;
    case value2:
        // code to be executed if expression == value2
        break;
    // you can have any number of case statements
    default:
        // code to be executed if expression doesn't match any case
}
```

**Example:**

```java
int day = 3;
switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    default:
        System.out.println("Weekend");
        break;
}
```

## Loops

Loops are used to execute a block of code repeatedly.

### for Loop

**Syntax:**

```java
for (initialization; condition; update) {
    // code to be executed
}
```

**Example:**

```java
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

### while Loop

**Syntax:**

```java
while (condition) {
    // code to be executed
}
```

**Example:**

```java
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}
```

### do-while Loop

**Syntax:**

```java
do {
    // code to be executed
} while (condition);
```

**Example:**

```java
int i = 0;
do {
    System.out.println(i);
    i++;
} while (i < 5);
```

### for-each Loop

The `for-each` loop is used to iterate through elements of arrays or collections.

**Syntax:**

```java
for (dataType item : array) {
    // code to be executed
}
```

**Example:**

```java
int[] numbers = {10, 20, 30, 40, 50};
for (int num : numbers) {
    System.out.println(num);
}
```

## Arrays

Arrays are used to store multiple values in a single variable.

### Array Declaration

**Syntax:**

```java
dataType[] arrayName = new dataType[arraySize];
```

**Example:**

```java
int[] numbers = new int[5];
numbers[0] = 10;
numbers[1] = 20;
numbers[2] = 30;
numbers[3] = 40;
numbers[4] = 50;
```

### Array Initialization

**Example:**

```java
int[] numbers = {10, 20, 30, 40, 50};
```

### Accessing Array Elements

**Example:**

```java
int firstNumber = numbers[0];
System.out.println("First number: " + firstNumber);
```

### Looping Through an Array

**Example:**

```java
for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}
```

### Looping Through an Array with for-each

**Example:**

```java
int[] numbers = {10, 20, 30, 40, 50};
for (int num : numbers) {
    System.out.println(num);
}
```

## Strings

Strings are used for storing text.

### Creating a String

**Example:**

```java
String greeting = "Hello, World!";
```

### String Methods

Some common string methods:

- `length()`: Returns the length of the string.
- `toUpperCase()`: Converts the string to uppercase.
- `toLowerCase()`: Converts the string to lowercase.
- `charAt(int index)`: Returns the character at the specified index.

**Example:**

```java
String message = "Hello, World!";
System.out.println("Length: " + message.length());
System.out.println("Uppercase: " + message.toUpperCase());
System.out.println("Lowercase: " + message.toLowerCase());
System.out.println("Character at index 1: " + message.charAt(1));
```

## Input and Output

Java provides various classes to handle input and output.

### Using Scanner for Input

**Example:**

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter your name: ");
        String name = scanner.nextLine();

        System.out.print("Enter your age: ");
        int age = scanner.nextInt();

        System.out.println("Name: " + name);
        System.out.println("Age: " + age);

        scanner.close();
    }
}
```

### Printing Output

**Example:**

```java
System.out.println("Hello, World!");
System.out.print("Hello, ");
System.out.print("World!");
```

## Conclusion

These are the basic concepts of Java programming. Understanding these concepts is essential for anyone starting with Java. With a solid foundation in these basics, you can explore more advanced topics and features in Java.
