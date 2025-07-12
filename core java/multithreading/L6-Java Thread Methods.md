

### 🧵 **Thread Methods Overview**

In this session, we'll revisit the official thread methods in Java. We'll clean up our workspace and dive into each method with examples.

---

### 1. **start() Method**

- **Explanation**: When you create a new thread (e.g., `myThread t1 = new myThread();`), the JVM automatically calls the `run()` method of that thread.
- **Example**:
  ```java
  class MyThread extends Thread {
      public void run() {
          System.out.println("Thread is running");
      }
  }

  public class Main {
      public static void main(String[] args) {
          MyThread t1 = new MyThread();
          t1.start(); // This will call the run() method
      }
  }
  ```

---

### 2. **run() Method**

- **Explanation**: The `run()` method contains the code that constitutes the new thread. It is overridden to define the thread's behavior.
- **Example**:
  ```java
  class MyThread extends Thread {
      public void run() {
          for (int i = 1; i <= 5; i++) {
              System.out.println(i);
          }
      }
  }

  public class Main {
      public static void main(String[] args) {
          MyThread t1 = new MyThread();
          t1.start();
      }
  }
  ```

---

### 3. **sleep() Method**

- **Explanation**: The `sleep()` method pauses the execution of the current thread for a specified amount of time. It throws an `InterruptedException`, so it must be handled with a try-catch block.
- **Example**:
  ```java
  class MyThread extends Thread {
      public void run() {
          for (int i = 1; i <= 5; i++) {
              System.out.println(i);
              try {
                  Thread.sleep(1000); // Sleep for 1 second
              } catch (InterruptedException e) {
                  System.out.println(e);
              }
          }
      }
  }

  public class Main {
      public static void main(String[] args) {
          MyThread t1 = new MyThread();
          t1.start();
      }
  }
  ```

---

### 4. **join() Method**

- **Explanation**: The `join()` method allows one thread to wait until another thread completes its execution.
- **Example**:
  ```java
  class MyThread extends Thread {
      public void run() {
          try {
              Thread.sleep(5000); // Sleep for 5 seconds
          } catch (InterruptedException e) {
              System.out.println(e);
          }
          System.out.println("Thread t1 finished");
      }
  }

  public class Main {
      public static void main(String[] args) {
          MyThread t1 = new MyThread();
          t1.start();
          try {
              t1.join(); // Main thread waits for t1 to finish
          } catch (InterruptedException e) {
              System.out.println(e);
          }
          System.out.println("Hello");
      }
  }
  ```

---

### 5. **setPriority() Method**

- **Explanation**: The `setPriority()` method sets the priority of a thread. Priorities range from `MIN_PRIORITY` (1) to `MAX_PRIORITY` (10), with `NORM_PRIORITY` (5) being the default.
- **Example**:
  ```java
  class MyThread extends Thread {
      public MyThread(String name) {
          super(name);
      }

      public void run() {
          for (int i = 0; i < 5; i++) {
              System.out.println(Thread.currentThread().getName() + " - Count: " + i);
              try {
                  Thread.sleep(100);
              } catch (InterruptedException e) {
                  System.out.println(e);
              }
          }
      }
  }

  public class Main {
      public static void main(String[] args) {
          MyThread t1 = new MyThread("Low Priority Thread");
          MyThread t2 = new MyThread("Medium Priority Thread");
          MyThread t3 = new MyThread("High Priority Thread");

          t1.setPriority(Thread.MIN_PRIORITY);
          t2.setPriority(Thread.NORM_PRIORITY);
          t3.setPriority(Thread.MAX_PRIORITY);

          t1.start();
          t2.start();
          t3.start();
      }
  }
  ```

---

### 6. **interrupt() Method**

- **Explanation**: The `interrupt()` method interrupts a thread that is sleeping or waiting. It throws an `InterruptedException`.
- **Example**:
  ```java
  class MyThread extends Thread {
      public void run() {
          try {
              Thread.sleep(1000); // Sleep for 1 second
          } catch (InterruptedException e) {
              System.out.println("Thread interrupted: " + e);
          }
          System.out.println("Thread is running");
      }
  }

  public class Main {
      public static void main(String[] args) {
          MyThread t1 = new MyThread();
          t1.start();
          t1.interrupt(); // Interrupt the thread
      }
  }
  ```

---

### 7. **yield() Method**

- **Explanation**: The `yield()` method pauses the current thread and allows other threads to execute. It is a hint to the scheduler.
- **Example**:
  ```java
  class MyThread extends Thread {
      public void run() {
          for (int i = 0; i < 5; i++) {
              System.out.println(Thread.currentThread().getName() + " is running");
              Thread.yield(); // Yield to other threads
          }
      }
  }

  public class Main {
      public static void main(String[] args) {
          MyThread t1 = new MyThread();
          MyThread t2 = new MyThread();
          t1.start();
          t2.start();
      }
  }
  ```

---

### 8. **setDaemon() Method**

- **Explanation**: The `setDaemon()` method marks a thread as a daemon thread. Daemon threads run in the background and do not prevent the JVM from exiting(terminating).
- **Example**:
  ```java
  class MyThread extends Thread {
      public void run() {
          while (true) {
              System.out.println("Hello World");
              try {
                  Thread.sleep(1000);
              } catch (InterruptedException e) {
                  System.out.println(e);
              }
          }
      }
  }

  public class Main {
      public static void main(String[] args) {
          MyThread t1 = new MyThread();
          t1.setDaemon(true); // Set as daemon thread
          t1.start();
          System.out.println("Main is done");
      }
  }
  ```

---

### 🔍 **Key Points**

1. **User Threads vs. Daemon Threads**:
   - **User Threads**: Perform the main work of the application.
   - **Daemon Threads**: Run in the background and do not prevent the JVM from exiting.

2. **Priority Hints**:
   - Setting thread priorities is a hint to the scheduler, not a strict rule.

3. **Interrupting Threads**:
   - Use `interrupt()` to wake up a sleeping or waiting thread.

4. **Yielding**:
   - Use `yield()` to give other threads a chance to execute.

---


### **basically**, a **daemon thread will terminate automatically when the main thread (and all other user threads) have finished**.

---

### 🔍 Why?

Because daemon threads are considered **"supporting/background"** threads.  
The JVM doesn't wait for them — it only waits for **user threads** to finish.

---

### ✅ JVM Exit Rule:

> 🔔 The **JVM exits** when **no user (non-daemon) threads** are running.  
> 🔚 At that moment, all **daemon threads are abruptly terminated** — even if they’re still running.

---

### 🔧 Example: Daemon dies with main

```java
public class DaemonTest {
    public static void main(String[] args) {
        Thread daemon = new Thread(() -> {
            while (true) {
                System.out.println("Daemon running...");
                try {
                    Thread.sleep(500);
                } catch (InterruptedException e) {}
            }
        });

        daemon.setDaemon(true); // Mark as daemon
        daemon.start();

        System.out.println("Main thread sleeping...");
        try {
            Thread.sleep(1000); // Main thread sleeps briefly
        } catch (InterruptedException e) {}

        System.out.println("Main thread ending");
        // Daemon will also stop here automatically
    }
}
```

### 🧾 Sample Output:

```
Main thread sleeping...
Daemon running...
Daemon running...
Main thread ending
```

> You may see a few "Daemon running..." messages, but after `main` ends, **JVM stops**, and the daemon is **terminated abruptly**.

---

### ❗ Key Point

- **Yes**, daemon thread _usually_ dies **when main thread dies**, **if no other user threads exist**.
    
- If **other user threads** are still running, **daemon threads continue** until those also finish.
    

---

### ✅ Confirm with Example:

```java
Thread t1 = new Thread(() -> {
    // user thread
    try { Thread.sleep(5000); } catch (Exception e) {}
    System.out.println("User thread done");
});

Thread daemon = new Thread(() -> {
    while (true) {
        System.out.println("Daemon running...");
        try { Thread.sleep(500); } catch (Exception e) {}
    }
});
daemon.setDaemon(true);

t1.start();     // user thread
daemon.start(); // daemon thread

System.out.println("Main done");
```

🧾 Output:

```
Main done
Daemon running...
Daemon running...
...
User thread done
```

> Here, even after `main` ends, daemon thread keeps running because `t1` (a user thread) is still alive.
