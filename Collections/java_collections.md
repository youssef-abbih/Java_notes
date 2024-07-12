# Java Collections Framework

The Java Collections Framework provides a set of classes and interfaces for storing and manipulating groups of data as a single unit. It includes various data structures like lists, sets, maps, and queues.

## Why Use Collections?

- **Efficiency**: Collections provide optimized implementations for common data structures and algorithms.
- **Reusability**: You can use pre-built data structures rather than implementing your own.
- **Interoperability**: Collections work seamlessly with Java's standard APIs and libraries.
- **Flexibility**: Collections provide a wide range of interfaces and implementations to suit different needs.

## Collection Interfaces

### Collection Interface

The `Collection` interface is the root of the collections hierarchy. It defines methods for basic operations like adding, removing, and checking the size of the collection.

### List Interface

The `List` interface extends `Collection` and represents an ordered collection that allows duplicate elements.

- **ArrayList**: Resizable-array implementation of the `List` interface. It allows random access and is not synchronized.
- **LinkedList**: Doubly-linked list implementation of the `List` interface. It allows sequential access and can be used as a list, stack, or queue.

**Example:**

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<String> arrayList = new ArrayList<>();
        arrayList.add("Apple");
        arrayList.add("Banana");
        arrayList.add("Cherry");

        List<String> linkedList = new LinkedList<>();
        linkedList.add("Dog");
        linkedList.add("Elephant");
        linkedList.add("Frog");

        System.out.println("ArrayList: " + arrayList);
        System.out.println("LinkedList: " + linkedList);
    }
}
```

### Set Interface

The `Set` interface extends `Collection` and represents a collection that does not allow duplicate elements.

- **HashSet**: Hash table-based implementation of the `Set` interface. It does not guarantee the order of elements.
- **LinkedHashSet**: Hash table and linked list implementation of the `Set` interface. It maintains the insertion order.
- **TreeSet**: Tree-based implementation of the `Set` interface. It stores elements in a sorted order.

**Example:**

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Set<String> hashSet = new HashSet<>();
        hashSet.add("Apple");
        hashSet.add("Banana");
        hashSet.add("Cherry");

        Set<String> linkedHashSet = new LinkedHashSet<>();
        linkedHashSet.add("Dog");
        linkedHashSet.add("Elephant");
        linkedHashSet.add("Frog");

        Set<String> treeSet = new TreeSet<>();
        treeSet.add("Grape");
        treeSet.add("Honeydew");
        treeSet.add("Kiwi");

        System.out.println("HashSet: " + hashSet);
        System.out.println("LinkedHashSet: " + linkedHashSet);
        System.out.println("TreeSet: " + treeSet);
    }
}
```

### Map Interface

The `Map` interface represents a collection of key-value pairs. It does not extend the `Collection` interface.

- **HashMap**: Hash table-based implementation of the `Map` interface. It does not guarantee the order of elements.
- **LinkedHashMap**: Hash table and linked list implementation of the `Map` interface. It maintains the insertion order.
- **TreeMap**: Tree-based implementation of the `Map` interface. It stores key-value pairs in a sorted order.

**Example:**

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Map<String, Integer> hashMap = new HashMap<>();
        hashMap.put("Apple", 1);
        hashMap.put("Banana", 2);
        hashMap.put("Cherry", 3);

        Map<String, Integer> linkedHashMap = new LinkedHashMap<>();
        linkedHashMap.put("Dog", 4);
        linkedHashMap.put("Elephant", 5);
        linkedHashMap.put("Frog", 6);

        Map<String, Integer> treeMap = new TreeMap<>();
        treeMap.put("Grape", 7);
        treeMap.put("Honeydew", 8);
        treeMap.put("Kiwi", 9);

        System.out.println("HashMap: " + hashMap);
        System.out.println("LinkedHashMap: " + linkedHashMap);
        System.out.println("TreeMap: " + treeMap);
    }
}
```

### Queue Interface

The `Queue` interface extends `Collection` and represents a collection designed for holding elements prior to processing. It typically orders elements in a FIFO (first-in, first-out) manner.

- **PriorityQueue**: Priority heap-based implementation of the `Queue` interface. It orders elements according to their natural order or a specified comparator.
- **LinkedList**: Doubly-linked list implementation of the `Queue` interface. It can be used as a queue, stack, or list.

**Example:**

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Queue<String> priorityQueue = new PriorityQueue<>();
        priorityQueue.add("Apple");
        priorityQueue.add("Banana");
        priorityQueue.add("Cherry");

        Queue<String> linkedListQueue = new LinkedList<>();
        linkedListQueue.add("Dog");
        linkedListQueue.add("Elephant");
        linkedListQueue.add("Frog");

        System.out.println("PriorityQueue: " + priorityQueue);
        System.out.println("LinkedListQueue: " + linkedListQueue);
    }
}
```

### Deque Interface

The `Deque` interface extends `Queue` and represents a double-ended queue that allows elements to be added or removed from both ends.

- **ArrayDeque**: Resizable-array implementation of the `Deque` interface.
- **LinkedList**: Doubly-linked list implementation of the `Deque` interface.

**Example:**

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Deque<String> arrayDeque = new ArrayDeque<>();
        arrayDeque.addFirst("Apple");
        arrayDeque.addLast("Banana");
        arrayDeque.addFirst("Cherry");

        Deque<String> linkedListDeque = new LinkedList<>();
        linkedListDeque.addFirst("Dog");
        linkedListDeque.addLast("Elephant");
        linkedListDeque.addFirst("Frog");

        System.out.println("ArrayDeque: " + arrayDeque);
        System.out.println("LinkedListDeque: " + linkedListDeque);
    }
}
```

## Generics in Collections

Generics provide type safety by allowing you to specify the type of objects that a collection can hold.

**Example:**

```java
List<String> stringList = new ArrayList<>();
stringList.add("Apple");
stringList.add("Banana");

for (String s : stringList) {
    System.out.println(s);
}
```

## Why Use `List arr = new ArrayList<>()`?

Using `List arr = new ArrayList<>()` instead of `ArrayList arr = new ArrayList<>()` allows you to:

1. **Programming to an Interface**: This promotes flexibility, as you can easily change the implementation to another class that implements the `List` interface (e.g., `LinkedList`) without changing much code.
2. **Code Readability**: It makes it clear that you're working with a `List` rather than a specific implementation, which can make the code easier to understand.

**Example:**

```java
List<String> list = new ArrayList<>();
list.add("Apple");
list.add("Banana");
list.add("Cherry");

for (String s : list) {
    System.out.println(s);
}
```

## Conclusion

The Java Collections Framework provides a comprehensive set of interfaces and classes for managing groups of data. By understanding and utilizing these collections, you can write more efficient, reusable, and flexible code.
