# Java Multithreading

## What is a Thread?

A thread is a lightweight subprocess, the smallest unit of processing. It is a separate path of execution in a program. Java allows concurrent execution of two or more threads for maximum utilization of CPU.

## Creating a Thread in Java

There are two main ways to create a thread in Java:

1. By extending the `Thread` class.
2. By implementing the `Runnable` interface.

### Example: Extending the `Thread` class

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running...");
    }

    public static void main(String args[]) {
        MyThread t1 = new MyThread();
        t1.start();
    }
}
```

### Example: Implementing the `Runnable` interface

```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Thread is running...");
    }

    public static void main(String args[]) {
        MyRunnable myRunnable = new MyRunnable();
        Thread t1 = new Thread(myRunnable);
        t1.start();
    }
}
```

## Synchronization in Java

Synchronization is the capability to control the access of multiple threads to any shared resource. It is mainly used to:

1. Prevent thread interferences.
2. Prevent consistency problems.

### Mutual Exclusive

Mutual Exclusive, a thread synchronization, helps keep threads from interfering with one another while sharing data. This can be done in Java in three ways:

1. By synchronized methods.
2. By synchronized blocks.
3. By static synchronization.

#### Synchronized Methods

When a thread invokes a synchronized method, it automatically acquires the lock for that method and releases it when the thread completes its task.

**Example:**

```java
public synchronized String getData(File f) {
    String s = "";
    try {
        Scanner sc = new Scanner(f);
        while (sc.hasNextLine()) {
            s += sc.nextLine() + "\n";
        }
    } catch (FileNotFoundException e) {
        e.printStackTrace();
    }
    return s;
}
```

#### Synchronized Block

A synchronized block can be used to perform synchronization on any specific resource of the method. It is used to lock an object for any shared resource. The scope of a synchronized block is smaller than a method.

**Example:**
```java
public String getData(File f) {
    File file = new File("file1.txt");
    String s = "";
    synchronized(file) {
        try {
            Scanner sc = new Scanner(file);
            while (sc.hasNextLine()) {
                s += sc.nextLine() + "\n";
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
    }
    return s;
}
```

#### Static Synchronization

When a static method is synchronized, the lock will be on the class, not on the object.

**Example:**
```java
public class FileUtil {
    public static synchronized String getDataStatic(File f) {
        String s = "";
        try {
            Scanner sc = new Scanner(f);
            while (sc.hasNextLine()) {
                s += sc.nextLine() + "\n";
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
        return s;
    }
}
```

#### Synchronization Types pros and cons

| Synchronization Type   | Pros                                                                                               | Cons                                                                      |
|-------------------------|----------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| Synchronized Methods    | - Automatically manages locking and unlocking of resources.<br>- Ensures thread safety for methods. | - May lead to contention if multiple methods use the same lock.<br>- Can impact performance due to lock acquisition.                    |
| Synchronized Blocks     | - Provides finer control over synchronization.<br>- Allows locking on specific sections of code.    | - Requires explicit handling of locks.<br>- Risk of deadlock if not carefully managed.                                                 |
| Static Synchronization | - Synchronizes access to static methods and variables across all instances and threads.             | - May lead to contention on the class level.<br>- Global lock can affect scalability and performance in high-concurrency environments.   |

## Thread Pool

A thread pool is an instance of the `ExecutorService` class. With an `ExecutorService`, you can submit tasks that will be completed in the future.

### Types of Thread Pools

There are five types of thread pools which can be created with the `Executors` class:

1. **Single Thread Executor**: A thread pool with only one thread. All the submitted tasks will be executed sequentially.

    ```java
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;

    public class SingleThreadExecutorExample {
        public static void main(String[] args) {
            ExecutorService executor = Executors.newSingleThreadExecutor();
            for (int i = 1; i <= 5; i++) {
                final int taskId = i;
                executor.submit(() -> {
                    System.out.println("Task " + taskId + " executed by " + Thread.currentThread().getName());
                });
            }
            executor.shutdown();
        }
    }
    ```

2. **Cached Thread Pool**: A thread pool that creates as many threads as it needs to execute tasks in parallel. The old available threads will be reused for new tasks. If a thread is not used for 60 seconds, it will be terminated and removed from the pool.

    ```java
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;

    public class CachedThreadPoolExample {
        public static void main(String[] args) {
            ExecutorService executor = Executors.newCachedThreadPool();
            for (int i = 1; i <= 5; i++) {
                final int taskId = i;
                executor.submit(() -> {
                    System.out.println("Task " + taskId + " executed by " + Thread.currentThread().getName());
                });
            }
            executor.shutdown();
        }
    }

    ```

3. **Fixed Thread Pool**: A thread pool with a fixed number of threads. If a thread is not available for a task, the task is put in a queue waiting for another task to end.

    ```java
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;

    public class FixedThreadPoolExample {
        public static void main(String[] args) {
            ExecutorService executor = Executors.newFixedThreadPool(3); // Creates a thread pool with 3 threads
            for (int i = 1; i <= 5; i++) {
                final int taskId = i;
                executor.submit(() -> {
                    System.out.println("Task " + taskId + " executed by " + Thread.currentThread().getName());
                });
            }
            executor.shutdown();
        }
    }

    ```

4. **Scheduled Thread Pool**: A thread pool made to schedule future tasks.

    ```java
    import java.util.concurrent.Executors;
    import java.util.concurrent.ScheduledExecutorService;
    import java.util.concurrent.TimeUnit;

    public class ScheduledThreadPoolExample {
        public static void main(String[] args) {
            ScheduledExecutorService executor = Executors.newScheduledThreadPool(1);
            executor.scheduleAtFixedRate(() -> {
                System.out.println("Executing task at " + System.currentTimeMillis() / 1000);
            }, 0, 1, TimeUnit.SECONDS); // executes the task every 1 second

            // Shutdown after 5 seconds
            try {
                Thread.sleep(5000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            executor.shutdown();
        }
    }

    ```

5. **Single Thread Scheduled Pool**: A thread pool with only one thread to schedule future tasks.

    ```java
    import java.util.concurrent.Executors;
    import java.util.concurrent.ScheduledExecutorService;
    import java.util.concurrent.TimeUnit;

    public class SingleThreadScheduledPoolExample {
        public static void main(String[] args) {
            ScheduledExecutorService executor = Executors.newSingleThreadScheduledExecutor();
            executor.scheduleWithFixedDelay(() -> {
                System.out.println("Executing task at " + System.currentTimeMillis() / 1000);
            }, 0, 2, TimeUnit.SECONDS); // executes the task every 2 seconds with an initial delay of 0

            // Shutdown after 10 seconds
            try {
                Thread.sleep(10000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            executor.shutdown();
        }
    }
    ```

### Pro and cons of each thread pool

| Thread Pool Type            | Pros                                                                                     | Cons                                                                 |
|-----------------------------|------------------------------------------------------------------------------------------|----------------------------------------------------------------------|
| Single Thread Executor      | - Ensures tasks are executed sequentially.<br>- Guarantees no more than one thread.<br> | - Limited concurrency.<br>- Task execution order may vary.           |
| Cached Thread Pool          | - Dynamically adjusts pool size.<br>- Reuses idle threads.<br>                            | - No limit on the number of threads (may lead to resource exhaustion). |
| Fixed Thread Pool           | - Maintains a fixed number of threads.<br>- Guarantees task execution order.<br>          | - Limited flexibility in managing peak loads.<br>- Potential resource wastage. |
| Scheduled Thread Pool       | - Allows tasks to be scheduled for future execution.<br>- Supports periodic tasks.        | - May lead to thread starvation under heavy loads.<br>- Complexity in scheduling tasks. |
| Single Thread Scheduled Pool| - Guarantees single-threaded execution for scheduled tasks.<br>- Simple to use.<br>       | - Limited to sequential execution.<br>- Potential bottleneck for concurrent tasks. |

## Callable and Future

* The Java `Callable` interface uses Generics to define the return type of the object.
* The `Executors` class provides useful methods to execute `Callable` tasks in a thread pool.
  * Since `Callable` tasks run in parallel, we have to wait for the returned object.
* Java `Callable` tasks return a `Future` object.
* Use the `Future` object to find out the status of the `Callable` task and get the returned object.
  * It provides the `get()` method that can wait for the `Callable` to finish and then return the result.

### Example: Using Callable and Future

```java
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class CallableExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newSingleThreadExecutor();
        
        Callable<Integer> task = () -> {
            // Simulate long running task
            Thread.sleep(2000);
            return 123;
        };
        
        Future<Integer> future = executor.submit(task);
        
        try {
            // Wait for the result
            Integer result = future.get();
            System.out.println("Result: " + result);
        } catch (Exception e) {
            e.printStackTrace();
        }
        
        executor.shutdown();
    }
}
```
