
---

### 📌 **Java Multithreading – Explanation**

#### 🔹 **Understanding the Basics**

- Initially, we didn’t dive deep into Java itself. Instead, we focused on **what happens inside the CPU**:
    
    - Concepts like **programs**, **processes**, **multitasking**, and **multithreading** were introduced.
        
    - Now, we're connecting those with **Java programs**.
        

#### 🔹 **Relating with Real Example**

- Whether it's MS Word or a `HelloWorld` program in Java — **both are programs**.
    
- When run, **they become processes**.
    
- A **process** can be divided into **multiple threads** to achieve multitasking.
    

---

### 🧵 **What is Multithreading in Java?**

- **Multithreading** = Concurrent execution of two or more threads.
    
- Used to **maximize CPU utilization**.
    
- Helps in building **efficient applications**.
    
- Java supports multithreading using the `java.lang` package.
    

---

### 💡 **Managed by JVM + OS**

#### 📍 In Single-Core Systems:

- **Only one thread executes at a time.**
    
- **JVM + OS** manage **thread switching** via **time-slicing**, creating an **illusion of concurrency**.
    

#### 📍 In Multi-Core Systems:

- **JVM distributes threads** across **multiple cores**.
    
- Enables **true parallelism**.
    

---

### 🔸 **Thread in Java**

- A **thread** is a **lightweight process** or **a small unit of execution**.
    
- Java supports threads using:
    
    - `Thread` class
        
    - `Runnable` interface
        

---

### 🔹 **Main Thread**

- When a Java program starts:
    
    - The **first thread that runs** is the **main thread**.
        
    - It **executes the `main()` method**.
        

---

### 🧪 **Code Example: Main Thread**

```java
public class Test {
    public static void main(String[] args) {
        System.out.println(Thread.currentThread().getName());
    }
}
```

#### 🧾 Output:

```
main
```

✅ This proves that the **main thread** is running by default.

---

### ✅ **Key Takeaways**

- Every Java program **starts with a single thread** – the main thread.
    
- **Multithreading** is not used unless explicitly implemented.
    
- JVM helps in scheduling threads in both single-core and multi-core environments.
    

---
