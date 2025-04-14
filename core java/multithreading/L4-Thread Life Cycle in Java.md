

A Java thread goes through several **states** from its creation to termination. These are:

#### 1. **NEW**

- The thread is created but not yet started.
    
- Example:
    
    ```java
    MyThread t1 = new MyThread();
    System.out.println(t1.getState()); // NEW
    ```
    

#### 2. **RUNNABLE**

- After calling `t1.start()`, the thread enters the `RUNNABLE` state.
    
- It is now ready to run and waiting for CPU allocation.
    
- Note: **`Runnable`** (interface) ≠ **`RUNNABLE`** (state).
    

#### 3. **RUNNING**

- There's **no explicit `RUNNING` state in Java**, but when a thread from the RUNNABLE pool gets CPU time, it starts executing.
    
- Internally, Java treats RUNNABLE as both ready-to-run and running.
    
- `getState()` will still show `RUNNABLE` even while it's executing.
    

#### 4. **TIMED_WAITING**

- When a thread is paused using `Thread.sleep(time)` or `join(time)`, it goes into this state.
    
- Example:
    
    ```java
    Thread.sleep(2000); // Inside run() method
    System.out.println(Thread.currentThread().getState()); // TIMED_WAITING
    ```
    

#### 5. **WAITING**

- When a thread waits indefinitely for another thread’s action (like using `.join()` without time).
    
- More on this when you explore inter-thread communication.
    

#### 6. **BLOCKED**

- When a thread is waiting to acquire a lock to enter a synchronized block/method.
    
- You’ll encounter this with synchronization.
    

#### 7. **TERMINATED**

- When the thread’s run method completes execution.
    

---

### ✅ Example Summary from the Code:

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Running");
        try {
            Thread.sleep(2000); // moves to TIMED_WAITING
        } catch (InterruptedException e) {
            System.out.println(e);
        }
    }

    public static void main(String[] args) throws InterruptedException {
        MyThread t1 = new MyThread();
        
        System.out.println(t1.getState()); // NEW
        
        t1.start(); 
        System.out.println(t1.getState()); // RUNNABLE

        Thread.sleep(100); // Give time for t1 to run

        System.out.println(t1.getState()); // Likely TIMED_WAITING if sleep in run() is active

        t1.join(); // Main thread waits for t1 to finish

        System.out.println(t1.getState()); // TERMINATED
    }
}
```

---

### 📝 Key Observations:

- `Thread.getState()` helps track state transitions.
    
- Java **abstracts away** the RUNNING state into RUNNABLE.
    
- `Thread.sleep()` causes `TIMED_WAITING`.
    
- `join()` waits for a thread to die → **WAITING** or **TIMED_WAITING** (if timed join).
    
- Always handle `InterruptedException` with `try-catch` or `throws`.
    
