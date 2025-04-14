
---

## 📘 Notes: Creating Threads in Java

### ✅ **1. Using the `Thread` Class (Extending Thread)**

#### 🔹 Steps:

1. **Create a class** that extends the `Thread` class.
    
2. **Override the `run()` method** to define the task you want to execute in the new thread.
    
3. **Create an object** of the class.
    
4. **Call the `start()` method** on the object to begin the thread execution.
    

#### 📄 Example:

```java
class World extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 10000; i++) {
            System.out.println("World - " + Thread.currentThread().getName());
        }
    }
}

public class Main {
    public static void main(String[] args) {
        World w = new World(); // Creating object
        w.start(); // Starting thread

        for (int i = 0; i < 10000; i++) {
            System.out.println("Hello - " + Thread.currentThread().getName());
        }
    }
}
```

#### 🔎 Key Points:

- `Thread.currentThread().getName()` helps identify which thread is running.
    
- Threads run **independently and concurrently**, so output order is not guaranteed.
    
- Infinite loops can block the execution of further statements (causes unreachable code).
    

---

### ✅ **2. Using the `Runnable` Interface (Implementing Runnable)**

#### 🔹 Steps:

1. **Create a class** that implements `Runnable` interface.
    
2. **Override the `run()` method** with the task.
    
3. **Create an object** of the class.
    
4. **Pass the object** to a new `Thread` instance.
    
5. **Call the `start()` method** on the `Thread` object.
    

#### 📄 Example:

```java
class World implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 10000; i++) {
            System.out.println("World - " + Thread.currentThread().getName());
        }
    }
}

public class Main {
    public static void main(String[] args) {
        World w = new World(); // Object of Runnable
        Thread t1 = new Thread(w); // Passing Runnable to Thread
        t1.start(); // Start thread

        for (int i = 0; i < 10000; i++) {
            System.out.println("Hello - " + Thread.currentThread().getName());
        }
    }
}
```

#### 🔎 Key Points:

- More flexible approach (you can extend other classes too).
    
- Helps in separating **task (Runnable)** from **thread (Thread class)**.
    
- Same non-deterministic execution due to concurrency.
    

---

### 💡 Conclusion:

|Feature|Extending `Thread`|Implementing `Runnable`|
|---|---|---|
|Inheritance|Not possible to extend another class|Possible|
|Flexibility|Less flexible|More flexible|
|Thread creation|Direct object of class|Need to pass to `Thread` object|
|Reusability|Less reusable|More reusable|

---




# Questions

## why we have to Pass the object to a new `Thread` instance. . runnable interface?

### 🧠 The core idea:

When you **implement the `Runnable` interface**, your class **does not become a thread**—it just **defines the task** that a thread should perform.

To actually **run that task in a new thread**, you need to **pass your `Runnable` object to a `Thread` object**.

---

### 🚀 Here's what happens step by step:

#### ✅ Option 1: `extends Thread`

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running...");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t1 = new MyThread(); // thread created
        t1.start(); // thread starts, run() executes
    }
}
```

> In this approach, `MyThread` **is a thread** itself.

---

#### ✅ Option 2: `implements Runnable` – the reason you're asking about

```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Thread is running...");
    }
}

public class Main {
    public static void main(String[] args) {
        MyRunnable obj = new MyRunnable();   // Task created
        Thread t1 = new Thread(obj);         // Thread created, task passed
        t1.start();                          // Thread starts, calls obj.run()
    }
}
```

> Here, `MyRunnable` is **not a thread**, just a class that tells a thread **what to do**.  
> So, we pass it to a real thread object (`Thread t1 = new Thread(obj)`).

---

### 🔍 So why pass the object?

**Because the `Runnable` interface doesn't create a thread—it just provides the `run()` method.**

If you only create an object of `MyRunnable`, like:

```java
MyRunnable obj = new MyRunnable();
obj.run(); // This runs in the main thread, NOT a new thread!
```

It won't run concurrently. To run it in a **new thread**, you need:

```java
Thread t = new Thread(obj);
t.start(); // Now it runs in parallel!
```

---

### ✅ When to use Runnable?

- When your class **already extends another class** (Java allows only single inheritance).
    
- To **separate the task** (Runnable) from the **execution mechanism** (Thread).
    



