
---

## 🧵 **Executor Framework in Java – Simplified Notes**

### 🚀 Introduction

- The **Executor Framework** was introduced in **Java 5**.
    
- It **simplifies multithreading** by abstracting the complexity of thread creation and management.
    
- Prior to this, developers had to **manually create, start, and manage threads**.
    

---

### 😓 Problems with Manual Thread Management

1. **Manual Thread Creation**:
    
    - Tedious and error-prone (e.g., using `new Thread()` everywhere).
        
2. **No Reuse of Threads**:
    
    - Threads were not reused, leading to performance overhead.
        
3. **Lack of Scalability**:
    
    - No proper resource management.
        
    - System may crash if too many threads are created.
        
4. **Error Handling**:
    
    - More complex when managing threads manually.
        

---

### 🤖 What is the Executor Framework?

- **Executor** is an **abstraction** that handles thread management for you.
    
- Developers focus only on **business logic**.
    
- Internally, Executor manages thread lifecycle efficiently.
    

---

### 🧱 Core Components of Executor Framework:

1. **Executor** – base interface.
    
2. **ExecutorService** – extends Executor, adds advanced methods.
    
3. **ScheduledExecutorService** – supports scheduling tasks (delayed or periodic execution).
    

---

### ✅ Advantages of Executor Framework

- Reuses a **fixed set of threads** (like reliable friends in a lemonade stand).
    
- Improves **performance** and **resource management**.
    
- Supports **scaling**, **task queuing**, and **scheduling**.
    

---

### 🧪 Manual Threading Example – With Issues

```java
public class ManualFactorial {
    public static long factorial(int n) {
        long result = 1;
        for (int i = 1; i <= n; i++) {
            result *= i;
        }
        return result;
    }

    public static void main(String[] args) throws InterruptedException {
        long startTime = System.currentTimeMillis();

        Thread[] threads = new Thread[10];

        for (int i = 1; i <= 10; i++) {
            final int num = i;
            threads[i - 1] = new Thread(() -> {
                long result = factorial(num);
                System.out.println("Factorial of " + num + " is " + result);
            });
            threads[i - 1].start();
        }

        // Wait for all threads to complete
        for (Thread t : threads) {
            t.join();
        }

        long endTime = System.currentTimeMillis();
        System.out.println("Total Time Taken: " + (endTime - startTime) + " ms");
    }
}
```

> ❌ **Downside**: Threads are manually created and not reused.

---

### ✅ With Executor Framework – Clean & Efficient

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ExecutorFactorial {
    public static long factorial(int n) {
        long result = 1;
        for (int i = 1; i <= n; i++) {
            result *= i;
        }
        return result;
    }

    public static void main(String[] args) {
        long startTime = System.currentTimeMillis();

        ExecutorService executor = Executors.newFixedThreadPool(3); // 3 Threads in the pool

        for (int i = 1; i <= 10; i++) {
            final int num = i;
            executor.submit(() -> {
                long result = factorial(num);
                System.out.println("Factorial of " + num + " is " + result);
            });
        }

        executor.shutdown(); // Shut down the executor after task submission

        while (!executor.isTerminated()) {
            // wait until all tasks are finished
        }

        long endTime = System.currentTimeMillis();
        System.out.println("Total Time Taken: " + (endTime - startTime) + " ms");
    }
}
```

> ✅ **Benefits**:

- Threads are reused.
    
- Clean code.
    
- No need to manage thread lifecycle manually.
    

---

### 🧠 Additional Utility Methods in `Executors`:

|Method|Description|
|---|---|
|`Executors.newFixedThreadPool(n)`|Fixed number of threads|
|`Executors.newSingleThreadExecutor()`|Only one thread|
|`Executors.newCachedThreadPool()`|Creates new threads as needed, reuses if possible|
|`Executors.newScheduledThreadPool(n)`|For scheduled or delayed task execution|

---

### 🔚 Final Thoughts:

- Executor Framework is like hiring a **task manager** who handles thread labor.
    
- It helps you **focus on the logic**, not the thread plumbing.
    
- Great for building **scalable, robust** concurrent applications.
    








### Executor Framework in Java

1. **Introduction**:
   - Introduced in Java 5.
   - Simplifies the development of concurrent applications by abstracting away the complexities involved in creating and managing threads.
   - Provides a high-level API for managing thread pools and executing asynchronous tasks.

2. **Problems with Manual Thread Management**:
   - **Resource Management**: No pre-defined resource management, leading to inefficient use of resources.
   - **Scalability**: Difficult to scale as the number of requests increases.
   - **Overhead**: Creating and destroying threads repeatedly leads to overhead in terms of memory and CPU usage.
   - **Error Handling**: Manual thread management can lead to complex error handling.

3. **Executor Framework Components**:
   - **Executor**: A simple interface with a single `execute` method for running `Runnable` tasks.
   - **ExecutorService**: An extended interface that provides methods for managing the lifecycle of threads, submitting tasks, and shutting down the executor.
   - **ScheduledExecutorService**: An extended interface that allows scheduling tasks to run after a given delay or periodically.

### Example: Factorial Calculation using Executor Framework

#### Without Executor Framework

```java
public class FactorialExample {
    public static void main(String[] args) {
        long startTime = System.currentTimeMillis();

        for (int i = 1; i <= 10; i++) {
            long result = factorial(i);
            System.out.println("Factorial of " + i + " is " + result);
        }

        long endTime = System.currentTimeMillis();
        System.out.println("Total time: " + (endTime - startTime) + " ms");
    }

    public static long factorial(long n) {
        long result = 1;
        for (long i = 1; i <= n; i++) {
            result *= i;
        }
        return result;
    }
}
```

#### With Executor Framework

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;

public class FactorialExecutorExample {
    public static void main(String[] args) {
        ExecutorService executorService = Executors.newFixedThreadPool(3);
        long startTime = System.currentTimeMillis();

        for (int i = 1; i <= 10; i++) {
            final int number = i;
            executorService.submit(() -> {
                long result = factorial(number);
                System.out.println("Factorial of " + number + " is " + result);
            });
        }

        executorService.shutdown();
        try {
            if (!executorService.awaitTermination(60, TimeUnit.SECONDS)) {
                executorService.shutdownNow();
            }
        } catch (InterruptedException e) {
            executorService.shutdownNow();
        }

        long endTime = System.currentTimeMillis();
        System.out.println("Total time: " + (endTime - startTime) + " ms");
    }

    public static long factorial(long n) {
        long result = 1;
        for (long i = 1; i <= n; i++) {
            result *= i;
        }
        return result;
    }
}
```

### Explanation

1. **Without Executor Framework**:
   - The factorial calculation is done synchronously in the main thread.
   - The total time taken is printed at the end.

2. **With Executor Framework**:
   - An `ExecutorService` is created with a fixed thread pool of 3 threads.
   - Tasks are submitted to the executor service to calculate the factorial of numbers from 1 to 10.
   - The `shutdown` method is called to initiate an orderly shutdown of the executor service.
   - The `awaitTermination` method is used to wait for all tasks to complete within a specified timeout.
   - The total time taken is printed at the end.

### Key Points

- **Executor Framework**: Simplifies thread management and improves the performance of concurrent applications.
- **Thread Pooling**: Reuses threads to reduce the overhead of creating and destroying threads.
- **Shutdown Procedures**: Use `shutdown` for orderly shutdown and `shutdownNow` for immediate shutdown.
- **awaitTermination**: Blocks until all tasks are completed or the timeout occurs.
- **Future Object**: Represents the result of an asynchronous computation (not shown in this example but mentioned in the transcript).

### Advantages of Executor Framework

- **Resource Management**: Efficient use of resources with thread pooling.
- **Scalability**: Easier to scale as the number of requests increases.
- **Error Handling**: Simplified error handling with built-in mechanisms.
- **Reusability**: Threads are reused, reducing the overhead of creating and destroying threads.

### Summary

- **Executor Framework**: Provides a high-level API for managing thread pools and executing asynchronous tasks.
- **Thread Pooling**: Improves performance and resource management.
- **Shutdown Procedures**: Ensures orderly shutdown of the executor service.
- **Future Object**: Allows retrieving the result of asynchronous computations.

---

