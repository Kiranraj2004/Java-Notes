

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
