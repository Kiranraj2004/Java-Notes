
### 🔒 **Synchronization and Locks in Java**

Synchronization and locks are crucial for managing access to shared resources in a multithreaded environment.

---

### 📔 **Key Concepts**

1. **Intrinsic Locks**: Built-in locks that every Java object has. Used automatically with the `synchronized` keyword.
2. **Explicit Locks**: Manual locks using the `Lock` interface, providing more control over locking behavior.
3. **Reentrant Locks**: A type of explicit lock that allows a thread to enter a locked section multiple times without deadlocking.

---

### 📝 **Example: Shared Notebook**

**Scenario**: Three children want to write in a shared notebook. Without synchronization, they might write over each other's text, leading to jumbled content.

**Solution**: Use synchronization to ensure only one child can write in the notebook at a time.

---

### 🔐 **Intrinsic Locks with `synchronized`**

**Example**: Using `synchronized` to ensure only one thread can access a method at a time.

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
- The `synchronized` keyword ensures that only one thread can access the `increment` method at a time.
- This prevents race conditions and ensures the final count is correct.

---

### 🔓 **Explicit Locks with `ReentrantLock


``` java

import java.util.concurrent.TimeUnit;  
import java.util.concurrent.locks.Lock;  
import java.util.concurrent.locks.ReentrantLock;  
  
class Counter{  
     private int count;  
     private static  final Lock lock=new ReentrantLock();  
  
    public Counter() {  
        this.count =0;  
    }  
    public void increment() throws InterruptedException {  
        if(lock.tryLock(1, TimeUnit.SECONDS)) {  
            try{  
                count++;  
            }  
            catch (Exception e){  
  
            }  
           finally {  
                lock.unlock();  
            }  
        }  
    }  
    public  int getcount(){  
        return this.count;  
    }  
}  
class MyThread extends Thread {  
    private Counter c;  
    MyThread(Counter c){  
        this.c=c;  
    }  
    @Override  
    public  void run() {  
        for(int i=1;i<=10000;i++){  
            try {  
                c.increment();  
            } catch (InterruptedException e) {  
                throw new RuntimeException(e);  
            }  
        }  
  
    }  
}  
  
public class ThreadPractice {  
    public static void main(String[] args) throws InterruptedException {  
        Counter obj=new Counter();  
        MyThread t1 = new MyThread(obj);  
        MyThread t2 = new MyThread(obj);  
  
        t1.start();  
        t2.start();  
  
        t1.join();  
        t2.join();  
  
        System.out.println(obj.getcount());  
    }  
}
```

**Example**: Using `ReentrantLock` to manually control locking behavior.

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

class BankAccount {
    private int balance = 1;
    private final Lock lock = new ReentrantLock();

    public void withdraw(int amount) {
        try {
            if (lock.tryLock(1, java.util.concurrent.TimeUnit.SECONDS)) {
                try {
                    if (balance >= amount) {
                        System.out.println(Thread.currentThread().getName() + " proceeding with withdrawal");
                        Thread.sleep(3000); // Simulate transaction processing
                        balance -= amount;
                        System.out.println(Thread.currentThread().getName() + " completed withdrawal. Remaining balance: " + balance);
                    } else {
                        System.out.println(Thread.currentThread().getName() + " insufficient balance");
                    }
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt(); // Restore interrupted status
                } finally {
                    lock.unlock();
                }
            } else {
                System.out.println(Thread.currentThread().getName() + " could not acquire the lock. Will try again later.");
            }
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt(); // Restore interrupted status
        }
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount();

        Runnable task = () -> account.withdraw(50);

        Thread t1 = new Thread(task, "Thread 1");
        Thread t2 = new Thread(task, "Thread 2");

        t1.start();
        t2.start();
    }
}
```

**Explanation**:
- `ReentrantLock` provides more control over locking behavior.
- `tryLock(long timeout, TimeUnit unit)` attempts to acquire the lock within a specified time, preventing indefinite waiting.
- The lock must be explicitly unlocked in a `finally` block to ensure it is released even if an exception occurs.

---

### 🔄 **Reentrant Lock Example**

**Example**: Demonstrating reentrancy with `ReentrantLock`.

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

class ReentrantExample {
    private final Lock lock = new ReentrantLock();

    public void outerMethod() {
        lock.lock();
        try {
            System.out.println("Outer method");
            innerMethod();
        } finally {
            lock.unlock();
        }
    }

    public void innerMethod() {
        lock.lock();
        try {
            System.out.println("Inner method");
        } finally {
            lock.unlock();
        }
    }

    public static void main(String[] args) {
        ReentrantExample example = new ReentrantExample();
        example.outerMethod();
    }
}
```

**Explanation**:
- The same thread can acquire the lock multiple times without deadlocking.
- The lock maintains a count of acquisitions and releases, ensuring proper unlocking.

---

### 🔍 **Key Points**

1. **Intrinsic Locks**: Automatic locks used with the `synchronized` keyword.
2. **Explicit Locks**: Manual locks using the `Lock` interface, providing more control.
3. **Reentrant Locks**: Allow a thread to enter a locked section multiple times without deadlocking.
4. **Lock Methods**:
   - `lock()`: Acquires the lock, waiting indefinitely if necessary.
   - `tryLock()`: Attempts to acquire the lock immediately, returning `false` if not available.
   - `tryLock(long timeout, TimeUnit unit)`: Attempts to acquire the lock within a specified time.
   - `unlock()`: Releases the lock.
   - `lockInterruptibly()`: Acquires the lock unless the thread is interrupted.

---
