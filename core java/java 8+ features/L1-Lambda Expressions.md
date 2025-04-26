
## ☕ Java Lambda Expressions – Notes

---

### 🔍 Why This Is Important

- Till now, we’ve seen complex ways of working with **threads** using `Runnable` and **anonymous classes**.
    
- Lambda expressions make the code **shorter**, **cleaner**, and **easier to understand**, especially in **multithreading**.
    

---

### 🧵 Reminder: Ways to Create Threads

1. **By Extending `Thread` Class**
    
2. **By Implementing `Runnable` Interface**
    

Old (Verbose) Style:

```java
Runnable r = new Runnable() {
    public void run() {
        System.out.println("Hello");
    }
};
Thread t = new Thread(r);
t.start();
```

---

### 💡 Functional Interfaces

A **functional interface** is:

- An interface with **only one abstract method**.
    
- Can have **default** and **static** methods, but only **one unimplemented method**.
    

✅ Example:

```java
@FunctionalInterface
interface MyFunc {
    void doSomething();
}
```

**Runnable** is a functional interface:

```java
@FunctionalInterface
public interface Runnable {
    public abstract void run();
}
```

---

### ⚡ Lambda Expressions = Anonymous Functions

#### Syntax:

```java
(parameters) -> { body }
```

Example:

```java
Runnable r = () -> System.out.println("Hello from Lambda!");
```

🧠 Behind the scenes:

- It’s the **same** as creating an anonymous class, but in a **much shorter syntax**.
    
- Java infers the method you're implementing from the context (i.e., the interface you're assigning to).
    

---

### 🧪 Example: Simplifying with Lambda

Original long code:

```java
Runnable task = new Runnable() {
    public void run() {
        System.out.println("Running...");
    }
};
```

Lambda version:

```java
Runnable task = () -> System.out.println("Running...");
```

Start thread:

```java
Thread t = new Thread(task);
t.start();
```

Or combine all:

```java
new Thread(() -> System.out.println("Running...")).start();
```

---

### 🎓 Understanding with Custom Interface

```java
@FunctionalInterface
interface Student {
    String getBio(String name);
}
```

Using lambda:

```java
Student lawStudent = (name) -> name + " is a law student";
System.out.println(lawStudent.getBio("Ram")); // Output: Ram is a law student
```

Lambda allows removing:

- Interface implementation class
    
- Method name
    
- Return type (if it's obvious)
    
- Braces (if only one line)
    

---

### 🧬 Lambda Expression Simplification

|Condition|Can You Omit?|
|---|---|
|One parameter|Parentheses around parameter|
|One statement in body|Curly braces and `return`|
|Known return type|Type declaration|

**From:**

```java
(String name) -> {
    return name + " is a law student";
}
```

**To:**

```java
name -> name + " is a law student"
```

---

### 🧠 Think of it like this:

- Just like:
    
    ```java
    int i = 1;
    ```
    
    stores a value in an `int`, you can:
    
    ```java
    Runnable task = () -> System.out.println("Hello");
    ```
    
    to store a **Lambda expression** in a **functional interface** reference.
    

---

### ✅ When to Use Lambda Expressions?

- When using **functional interfaces** (interfaces with one method).
    
- Perfect for use cases like:
    
    - Threads (`Runnable`)
        
    - Event listeners
        
    - Stream APIs
        
    - Comparators
        
    - Callbacks
        

---

### 🔄 Summary

- Lambda expressions simplify code by removing boilerplate.
    
- They're used **in place of anonymous inner classes**.
    
- Only work with **functional interfaces**.
    
- Great for writing **concise and readable multithreaded** code.
    