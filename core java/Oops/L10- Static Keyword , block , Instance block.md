
### 🔑 **Core Concepts of `static` in Java**

#### 1. **What `static` Does**

- Belongs to the **class**, not the instance.
    
- Shared across all objects.
    
- Saves memory — only **one copy** exists.
    

---

#### 2. **Where You Can Use `static`**

- Variables (`static int count`)
    
- Methods (`static void printSomething()`)
    
- Blocks (`static { // code }`)
    
- Nested classes (`static class Helper` — you'll get into this later)
    

---

#### 3. **Use Cases**

##### ✅ Static Variables

- Great for **counters**, like number of objects created.
    

```java
static int count = 0;
```

##### ✅ Static Methods

- Can be called **without creating an object**.
    
- Can't use non-static members directly.
    

```java
public static int max(int a, int b) {
    return a > b ? a : b;
}
```

##### ✅ Static Blocks

- Used for **static initialization logic**.
    

```java
static {
    // Runs once when class is loaded
    System.out.println("Class Loaded");
}
```

##### ✅ Utility Classes

- Example: `Math`, `Collections`, or your own `Utils` with reusable logic like `trimAndCapitalize()`.
    

##### ✅ Singleton Pattern

- Restrict a class to a **single instance**.
    
- Use `static` to provide global access.
    

```java
public class School {
    private static School instance = new School();
    private School() {} // private constructor

    public static School getInstance() {
        return instance;
    }
}
```

---

#### 4. **Rules to Remember**

- Static methods can't access non-static members **directly**.
    
- You can’t use `this` or `super` inside static context.
    
- `main()` is `static` because **JVM calls it directly without object** creation.





## ✅ What is a Static Block in Java?

A `static` block (also known as a **static initialization block**) is used to **initialize static variables or execute static code logic**.

### 📌 Syntax:

```java
class MyClass {
    static {
        // Code here runs once when class is loaded
        System.out.println("Static block executed");
    }
}
```

---

## 🔁 When Does a Static Block Execute?

- It executes **once**, and **only once**, when the class is **loaded into memory by the JVM** (i.e., during class loading).
    
- This happens **before**:
    
    - any object of the class is created
        
    - any static method is called
        
    - the `main()` method runs
        

---

## 🧠 Why Use Static Blocks?

|Use Case|Example|
|---|---|
|Complex static variable initialization|Reading config files, setting static maps/lists|
|Logging or debugging class load events|Printing logs|
|Loading native libraries or drivers|`System.loadLibrary("xyz");`|
|Validating static values at class loading|Checking static constants|

---

## 🧪 Example

```java
public class Example {
    static int x;
    static int y;

    static {
        System.out.println("Static block executed");
        x = 10;
        y = 20;
    }

    public static void main(String[] args) {
        System.out.println("Main method started");
        System.out.println("x = " + x + ", y = " + y);
    }
}
```

### 🔹 Output:

```
Static block executed
Main method started
x = 10, y = 20
```

---

## ⚙️ Multiple Static Blocks

- You can write **multiple** static blocks.
    
- They run **in the order they appear** in the class.
    

```java
class Demo {
    static {
        System.out.println("First static block");
    }
    
    static {
        System.out.println("Second static block");
    }

    public static void main(String[] args) {
        System.out.println("Main method");
    }
}
```

### Output:

```
First static block  
Second static block  
Main method
```

---

## 📛 Rules and Restrictions

|Rule|Explanation|
|---|---|
|✅ Allowed|Can access only **static variables and methods**|
|❌ Not allowed|Cannot access instance (`non-static`) variables directly|
|✅ Valid|Can use try-catch blocks|
|❌ Invalid|Cannot throw checked exceptions out of static blocks|

---

## 🔄 Static Blocks vs Instance Blocks

|Feature|Static Block|Instance Block|
|---|---|---|
|Runs When?|When class is loaded|When object is created|
|Runs How Often?|Once per class|Once per object|
|Accesses?|Only static members|Both static and instance|

---

## 🔍 Real-World Example: Loading JDBC Driver

```java
class DBConnection {
    static {
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            System.out.println("JDBC Driver Loaded");
        } catch (ClassNotFoundException e) {
            System.out.println("Driver not found");
        }
    }
}
```

Whenever the `DBConnection` class is loaded, the driver is loaded only once.

---

## ✅ Summary

- Static blocks are executed **once per class load**, even before the `main()` method.
    
- Best used for **static initialization logic** like setting up configs, loading drivers, initializing complex static data.
    
- Cannot access instance-level data or throw checked exceptions.
    




### Great question! ✅ Yes, in older versions of Java (prior to **Java 7**), it **was possible** to print something like **"Hello World"** using a `static` block **without a `main()` method**. But from **Java 7 onward**, this is **not allowed**.

---

## 🔴 From Java 7 Onward:

You **must** have a `main()` method to run the program. If the `main()` method is **missing**, the JVM throws:

```bash
Error: Main method not found in class MyClass
```

---

## ✅ Still, for learning purposes, here’s how it used to work:

```java
public class HelloWithoutMain {
    static {
        System.out.println("Hello World from static block!");
        System.exit(0); // Exit the program before JVM searches for main
    }
}
```

### 🟡 Output (in Java 6 or earlier):

```
Hello World from static block!
```

But in **Java 7+**, you get:

```
Error: Main method not found in class HelloWithoutMain
```

---

## 🔎 Why It Worked Before Java 7?

- JVM loaded the class and executed the `static` block before searching for `main()`.
    
- If `System.exit(0)` was called inside the static block, JVM never reached the point of searching for the `main()` method — so no error.
    

---

## ✅ Conclusion:

|Java Version|Can Print Without main()?|Notes|
|---|---|---|
|Java 6 or below|✅ Yes|Using `static` block + `System.exit(0)`|
|Java 7+|❌ No|JVM enforces presence of `main()` method|




### ✅ Instance Block in Java (a.k.a **Instance Initializer Block**)

An **instance block** is a block of code that runs **every time an object is created**, **before** the constructor runs.

---

### 🔹 Syntax:

```java
{
    // Instance block
    System.out.println("Instance block executed");
}
```

---

### 🧠 Key Points:

|Feature|Description|
|---|---|
|Runs When?|Every time an object is created|
|Runs Before?|**Before the constructor**|
|Can access instance members?|✅ Yes|
|Can be used for?|Repeated initialization logic for all constructors|
|Static allowed?|❌ No — static code not allowed here|

---

### 🔍 Example:

```java
public class InstanceBlockDemo {
    
    // Instance variable
    int x;

    // Instance initializer block
    {
        System.out.println("Instance block executed");
        x = 100;
    }

    // Constructor
    InstanceBlockDemo() {
        System.out.println("Constructor executed, x = " + x);
    }

    public static void main(String[] args) {
        InstanceBlockDemo obj1 = new InstanceBlockDemo();
        System.out.println("-----");
        InstanceBlockDemo obj2 = new InstanceBlockDemo();
    }
}
```

### 🔸 Output:

```
Instance block executed
Constructor executed, x = 100
-----
Instance block executed
Constructor executed, x = 100
```

---

### 🧱 Use Cases:

- **Shared logic** across multiple constructors
    
- Initializing **non-static instance variables** when logic is complex
    
- Logging or validation **before constructor runs**
    

---

### 🔄 Comparison:

|Feature|Static Block|Instance Block|
|---|---|---|
|Runs When?|Once when class loads|Every time object is created|
|Access static members?|✅ Yes|✅ Only instance members|
|Access instance members?|❌ No|✅ Yes|
|Order of execution|Class loading time|Before constructor|




### ❓ Can **static methods** be overridden in Java?

> **NO**, static methods **cannot** be overridden in the way instance methods are.

---

### ✅ You **can define** a static method with the **same name** in a subclass, but this is called **method hiding**, **not overriding**.

---

### 🔍 Why?

Because:

- Static methods are **class-level** (not object-level).
    
- They are **resolved at compile time**, not at runtime (which is required for polymorphism).
    

---

### 🧱 Example: Method Hiding

```java
class Parent {
    static void greet() {
        System.out.println("Hello from Parent");
    }
}

class Child extends Parent {
    static void greet() {
        System.out.println("Hello from Child");
    }
}

public class Test {
    public static void main(String[] args) {
        Parent p = new Child();  // Polymorphism-like
        p.greet();               // 🔴 Calls Parent's greet() — not Child's!
    }
}
```

### 🧾 Output:

```
Hello from Parent
```

Even though the object is of type `Child`, the **static method** call is resolved using the **reference type** (`Parent`), not the actual object.

---

### 🔁 If they were **instance methods**:

```java
class Parent {
    void greet() {
        System.out.println("Hello from Parent");
    }
}

class Child extends Parent {
    @Override
    void greet() {
        System.out.println("Hello from Child");
    }
}

public class Test {
    public static void main(String[] args) {
        Parent p = new Child();
        p.greet();  // ✅ Now calls Child's greet() — proper overriding
    }
}
```

### 🧾 Output:

```
Hello from Child
```

---

### 🚨 Summary:

|Feature|Instance Method|Static Method|
|---|---|---|
|Can be overridden?|✅ Yes|❌ No (hidden only)|
|Resolved at|Runtime|Compile time|
|Supports Polymorphism?|✅ Yes|❌ No|

---

Let me know if you want to test this with abstract classes or interfaces too!