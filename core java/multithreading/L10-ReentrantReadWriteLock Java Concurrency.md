
# 🔐

## 🧠 **Why Use ReentrantReadWriteLock?**

- The traditional `synchronized` block or `ReentrantLock` doesn't distinguish between **read** and **write** operations.
    
- This can cause **unnecessary blocking**, even when multiple threads only want to **read** shared data.
    

## 🧱 **ReentrantReadWriteLock Overview**

- **Interface**: `ReadWriteLock`
    
- **Implementation**: `ReentrantReadWriteLock`
    
- This lock provides:
    
    - `readLock()`: Shared lock for **reading**
        
    - `writeLock()`: Exclusive lock for **writing**
        

## ✅ **Advantages**

- **Multiple threads** can hold the **read lock** **concurrently**, **if no thread holds the write lock**.
    
- Ensures **exclusive access** for **write operations**.
    
- Reduces contention and improves performance in **read-heavy** scenarios.
    

---

## 💡 **Concept Summary**

- ✅ **Read Lock**: Many threads can acquire simultaneously.
    
- ❌ If a thread holds the **write lock**, no thread (not even readers) can acquire the lock.
    
- ✅ **Write Lock**: Only one thread can hold it at a time. Blocks **all other readers and writers**.
    

---

## 📘 **Example Code Logic**

### 👨‍💻 Class: `ReadWriteCounter`

- A shared `count` variable.
    
- Two methods:
    
    - `getCount()` → uses `readLock`
        
    - `increment()` → uses `writeLock`
        

### 🔁 Tasks

- **ReadTask** (Runnable): Reads and prints the counter value in a loop.
    
- **WriteTask** (Runnable): Increments the counter in a loop.
    

### 🧵 Threads

- 1 Writer thread → updates the counter.
    
- 2 Reader threads → read and print the counter.
    

---

## ⚙️ **Locks Used**

```java
ReentrantReadWriteLock lock = new ReentrantReadWriteLock();
Lock readLock = lock.readLock();
Lock writeLock = lock.writeLock();
```

### ✅ In `getCount()`

```java
readLock.lock();
try {
    return count;
} finally {
    readLock.unlock();
}
```

### ✅ In `increment()`

```java
writeLock.lock();
try {
    count++;
} finally {
    writeLock.unlock();


### final code 



import java.util.concurrent.locks.ReadWriteLock;
import java.util.concurrent.locks.ReentrantReadWriteLock;

public class ReadWriteCounter {
    private int count = 0;
    private final ReadWriteLock lock = new ReentrantReadWriteLock();

    public int getCount() {
        lock.readLock().lock();
        try {
            return count;
        } finally {
            lock.readLock().unlock();
        }
    }

    public void increment() {
        lock.writeLock().lock();
        try {
            count++;
        } finally {
            lock.writeLock().unlock();
        }
    }

    public static void main(String[] args) throws InterruptedException {
        ReadWriteCounter counter = new ReadWriteCounter();

        Runnable readTask = () -> {
            for (int i = 0; i < 10; i++) {
                System.out.println(Thread.currentThread().getName() + " reads count: " + counter.getCount());
            }
        };

        Runnable writeTask = () -> {
            for (int i = 0; i < 10; i++) {
                counter.increment();
                System.out.println(Thread.currentThread().getName() + " increments count to: " + counter.getCount());
            }
        };
    // below obj is same as above one's anonymous class
        /* Runnable writeTask = new Runnable(){
        @Override
        public void run(){
        for (int i = 0; i < 10; i++) {
                counter.increment();
                System.out.println(Thread.currentThread().getName() + " increments count to: " + counter.getCount());
            }
        }
        }; */

        Thread writerThread = new Thread(writeTask, "WriterThread");
        Thread readerThread1 = new Thread(readTask, "ReaderThread1");
        Thread readerThread2 = new Thread(readTask, "ReaderThread2");

        writerThread.start();
        readerThread1.start();
        readerThread2.start();

        writerThread.join();
        readerThread1.join();
        readerThread2.join();

        System.out.println("Final count: " + counter.getCount());
    }
}

```

---


## 🧪 **Thread Sleep Observation**

- Adding `Thread.sleep(50)` in the writer helps the CPU **context switch**, allowing readers to run in between writes.
    
- This demonstrates how **read/write coordination** improves concurrency.
    

---

## 🔍 **Behavior Without ReentrantReadWriteLock**

- If a normal lock was used:
    
    - All threads (even readers) would wait for the lock.
        
    - **Unnecessary blocking** would occur even when only reading.
        
    - Performance degrades in read-dominant scenarios.
        

---

## 📝 **Takeaway**

- Use `ReentrantReadWriteLock` when:
    
    - You have **frequent reads** and **infrequent writes**.
        
    - You want to allow **concurrent reads** without locking out all other threads.
        
- Avoid unnecessary resource locking and improve performance with smarter synchronization.
    
