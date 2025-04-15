
## 🧵 **Creating Threads in Java: `Thread` vs `Runnable`**

### ✅ Two Ways to Create a Thread:

1. **By extending the `Thread` class**
    
2. **By implementing the `Runnable` interface**
    

---

### 🤔 **Which one to use and when?**

#### 🧩 Case 1: When your class **already extends another class**

- Java doesn't support multiple inheritance (i.e., a class **cannot extend two classes**).
    
- So, if your class is **already extending another class**, you **cannot** extend `Thread`.
    
- ✅ In this case, you **must implement `Runnable`** to create a thread.
    

#### 🧪 Example:

```java
class B {
    // Some base class logic
}

class A extends B implements Runnable {
    public void run() {
        System.out.println("Thread running in class A");
    }
}

public class Main {
    public static void main(String[] args) {
        A a = new A();
        Thread t = new Thread(a); // Pass the Runnable object to Thread
        t.start(); // Start the new thread
    }
}
```

---

#### 🧩 Case 2: When your class **does not extend any other class**

- In this case, you are **free to either**:
    
    - extend the `Thread` class directly, or
        
    - implement the `Runnable` interface.
        

> 🔹 **Recommendation**: Even if you're free to choose, **prefer `Runnable`** because:

- It **separates the task** (`Runnable`) from the thread management (`Thread`).
    
- Offers **better design flexibility** and **decoupling** of code.
    

---

### 📌 Summary

|Situation|What to use|
|---|---|
|Class already extends another class|Use `Runnable`|
|Class doesn't extend any other class|You can use either, but `Runnable` is preferred|
