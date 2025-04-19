

**Problem without communication:**

- In multithreading, if threads don't communicate, they enter **busy waiting** (constantly checking conditions).
    
- This wastes CPU and can lead to **deadlock**.
    

**Solution:**

- Java provides three methods for **inter-thread communication**:
    
    - `wait()` → Releases lock and waits.
        
    - `notify()` → Wakes up **one** waiting thread.
        
    - `notifyAll()` → Wakes up **all** waiting threads.
        
- These must be called **within a synchronized block or method**.
    

---

### 💡 Example: Producer-Consumer Problem

**Goal:**  
One thread (producer) generates data.  
Another thread (consumer) uses that data.  
They should communicate so:

- Producer waits if buffer is full.
    
- Consumer waits if buffer is empty.
    

---

### ✅ Final Java Code

```java
// Shared Resource
class SharedResource {
    private int data;
    private boolean hasData = false;

    // Synchronized produce method
    public synchronized void produce(int value) {
        while (hasData) {
            try {
                wait(); // Wait if data is already available
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }
        data = value;
        hasData = true;
        System.out.println("Produced: " + data);
        notify(); // Notify consumer
    }

    // Synchronized consume method
    public synchronized int consume() {
        while (!hasData) {
            try {
                wait(); // Wait if data is not available
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }
        hasData = false;
        System.out.println("Consumed: " + data);
        notify(); // Notify producer
        return data;
    }
}
```

```java
// Producer thread
class Producer implements Runnable {
    private final SharedResource resource;

    public Producer(SharedResource resource) {
        this.resource = resource;
    }

    public void run() {
        for (int i = 0; i < 10; i++) {
            resource.produce(i);
        }
    }
}

// Consumer thread
class Consumer implements Runnable {
    private final SharedResource resource;

    public Consumer(SharedResource resource) {
        this.resource = resource;
    }

    public void run() {
        for (int i = 0; i < 10; i++) {
            resource.consume();
        }
    }
}
```

```java
// Main class to run both threads
public class ThreadCommunicationExample {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();

        Thread producerThread = new Thread(new Producer(resource));
        Thread consumerThread = new Thread(new Consumer(resource));

        producerThread.start();
        consumerThread.start();
    }
}
```

---

### 🔁 Flow Summary

|Step|Producer|Consumer|
|---|---|---|
|Buffer empty|Produces value → sets `hasData = true`|Waits (`wait()` until data is available)|
|Buffer full|Waits (`wait()` if `hasData = true`)|Consumes value → sets `hasData = false`|

---

### 🔔 Notes on `notify` vs `notifyAll`

- `notify()` → Use when only **one thread** should be woken.
    
- `notifyAll()` → Use when **multiple threads** may be waiting, e.g., many consumers.
    

---

Want me to generate a PDF of these notes and code for easy reference?