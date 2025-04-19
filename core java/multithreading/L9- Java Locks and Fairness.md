


### 🧵 **Concept: Threads and Locks**

- Multiple threads may want to access a shared resource.
    
- To avoid conflicts and ensure data integrity, we use **locks** to provide exclusive access.
    
- Java provides different mechanisms:
    
    - `synchronized` keyword
        
    - `ReentrantLock` class from `java.util.concurrent.locks`
        

---

### ⚖️ **Fair vs Unfair Locks**

#### 🔓 **Unfair Lock (Default Behavior)**

- **No guaranteed order** in which threads acquire the lock.
    
- Thread scheduling is **arbitrary** and managed by the **OS scheduler**.
    
- This can lead to **starvation** – some threads may **never** acquire the lock if others are constantly getting it.
    

#### 🔒 **Fair Lock**

- Uses **First-Come, First-Served (FCFS)** approach.
    
- Implemented by `ReentrantLock` with fairness flag:
    
    ```java
    Lock lock = new ReentrantLock(true); // fair lock
    ```
    
- Threads acquire the lock **in the order they requested** it.
    
- Prevents starvation.
    

---

### 💡 **Code Structure Example**

```java
Lock lock = new ReentrantLock(true); // true for fairness

public void accessResource() {
    lock.lock();
    try {
        System.out.println(Thread.currentThread().getName() + " acquired the lock");
        Thread.sleep(1000); // simulate work
    } catch (InterruptedException e) {
        Thread.currentThread().interrupt();
    } finally {
        lock.unlock();
        System.out.println(Thread.currentThread().getName() + " released the lock");
    }
}




import java.util.concurrent.locks.ReentrantLock;

public class FairnessExample {
    private final ReentrantLock lock = new ReentrantLock(true); // Fair lock

    public void accessResource() {
        lock.lock();
        try {
            System.out.println("Acquired the lock and doing some work...");
            Thread.sleep(1000); // Simulate work
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
            System.out.println("Thread interrupted");
        } finally {
            System.out.println("Releasing the lock");
            lock.unlock();
        }
    }

    public static void main(String[] args) throws InterruptedException {
        FairnessExample example = new FairnessExample();

        Runnable task = example::accessResource; // anonymous  class with run methos 

        Thread thread1 = new Thread(task);
        Thread thread2 = new Thread(task);
        Thread thread3 = new Thread(task);

        thread1.start();
        thread2.start();
        thread3.start();

        thread1.join();
        thread2.join();
        thread3.join();
    }
}

```

---

### 🎯 **Thread Scheduling and Execution Order**

- Threads are started using `thread.start()`.
    
- **Thread scheduling is non-deterministic**.
    
- Even if threads are started in order, execution order may vary due to OS scheduler.
    

#### ✅ To enforce order:

- Introduce delay between starting threads:
    
    ```java
    thread1.start();
    Thread.sleep(50);
    thread2.start();
    Thread.sleep(50);
    thread3.start();
    ```
    

---

### ❗ **Disadvantages of `synchronized` Keyword**

1. **No fairness guarantee**
    
2. **Thread blocking is automatic** and cannot be customized
    
3. **Not interruptible** – threads can't be interrupted while waiting for a lock
    
4. **No read/write distinction** – even reading threads are blocked if one write is happening
    

---

### ✅ **Advantages of Using `ReentrantLock`**

- Can specify **fairness**
    
- **Interruptible** lock acquisition (`lock.lockInterruptibly()`)
    
- Allows **manual control** over locking/unlocking
    
- Can be used to implement **read-write locks** (via `ReadWriteLock`)
    

---

### 🍬 **Analogy for Fairness**

- Distributing toffees to children:
    
    - **Unfair lock**: random kids get toffees, some may not get at all
        
    - **Fair lock**: kids stand in a line; toffees are distributed in the same order – no one is left out
        

---

### 🧠 **Interview Pointers**

- Explain the difference between `synchronized` and `ReentrantLock`
    
- Highlight the **fairness** issue and **starvation** risk in unfair locks
    
- Know how to **manually control locks**
    
- Discuss **interruptibility** and **read-write access** as advanced lock concepts
    

---

Would you like this in a downloadable PDF or formatted for slides or flashcards?