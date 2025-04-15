🔒 Synchronization in Java

Synchronization is a crucial concept in multithreading that ensures that only one thread can access a shared resource at a time, preventing data inconsistency.

---

### 🧵 **Key Concepts**

1. **Critical Section**: The part of the code where shared resources are accessed or modified.
2. **Race Condition**: A situation where the outcome depends on the relative timing of threads, leading to unpredictable results.
3. **Mutual Exclusion**: Ensuring that only one thread can access the critical section at a time.

---

### 🛠️ **Example: Counter Class**

Let's create a `Counter` class with a shared resource and demonstrate synchronization.

#### Step 1: Create the Counter Class

```java
class Counter {
    private int count = 0;

    public void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}
```

#### Step 2: Create the MyThread Class

```java
class MyThread extends Thread {
    private Counter counter;

    public MyThread(Counter counter) {
        this.counter = counter;
    }

    @Override
    public void run() {
        for (int i = 0; i < 1000; i++) {
            counter.increment();
        }
    }
}
```

#### Step 3: Test the Counter Class Without Synchronization

```java
public class Main {
    public static void main(String[] args) throws InterruptedException {
        Counter counter = new Counter();
        MyThread t1 = new MyThread(counter);
        MyThread t2 = new MyThread(counter);

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Final Count: " + counter.getCount());
    }
}
```

**Explanation**:
- We create a `Counter` object and two `MyThread` objects that share the same `Counter` instance.
- Each thread increments the counter 1000 times.
- We expect the final count to be 2000, but due to the race condition, the result is unpredictable it can be 1873 or some thing .

---

### 🔒 **Synchronization to Avoid Race Conditions**

To avoid race conditions, we use the `synchronized` keyword.

#### Step 4: Synchronize the Increment Method

```java
class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}
```

**Explanation**:
- By adding the `synchronized` keyword to the `increment` method, we ensure that only one thread can access this method at a time.
- This prevents data inconsistency and ensures the final count is 2000.

#### Step 5: Test the Counter Class With Synchronization

```java
public class Main {
    public static void main(String[] args) throws InterruptedException {
        Counter counter = new Counter();
        MyThread t1 = new MyThread(counter);
        MyThread t2 = new MyThread(counter);

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Final Count: " + counter.getCount());
    }
}
```

**Explanation**:
- With synchronization, the final count will always be 2000, as expected.

---

### 🔍 **Synchronized Block**

If you need to synchronize only a part of the method, you can use a synchronized block.

#### Step 6: Use a Synchronized Block

```java
class Counter {
    private int count = 0;

    public void increment() {
        synchronized (this) {
            count++;
        }
    }

    public int getCount() {
        return count;
    }
}
```

**Explanation**:
- The synchronized block ensures that only one thread can execute the code within the block at a time.
- This is useful when you need to synchronize only a specific part of the method.

---

### 🔑 **Key Points**

1. **Synchronized Method**: Ensures that only one thread can access the method at a time.
2. **Synchronized Block**: Allows synchronization of specific code blocks within a method.
3. **Critical Section**: The part of the code that accesses or modifies shared resources.
4. **Race Condition**: Occurs when the outcome depends on the relative timing of threads.
5. **Mutual Exclusion**: Ensures that only one thread can access the critical section at a time.

---
